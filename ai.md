## Pytorch

### 1.关于Conv2d类和conv2d方法的理解：

​	前者是类，后者是方法，用法的区别是：

​	**Conv2d：**

​		先实例化：m = torch.nn.Conv2d(input_channel,output_channel,kernel,…，)

​		再调用对象里的方法：	output = m(input)

​	**conv2d:**

​	output = conv2d(input,…其它参数)

​	**二者的关系：**

​		conv2d是更底层的轮子，更准确来说，它所属于的类torch.nn.functional( )是一个更底层的类

​		Conv2d等属于torch.nn的类是由conv2d等功能封装好的类，也就是说，经典的卷积神经网络、循环神经网络、transformer这些层PyTorch都给封装好了，只需要用户传入几个参数实例化就可以。

​		但是对于一些非典型网络，就不能直接调用了，需要用conv2d或者Conv2d继续封装，比如本科毕设的基于物理规律的循环神经网络。



### 2.关于Pytorch中卷积操作的理解

​	卷积核的尺寸并不是简单的Hk × Wk，而是一个四维张量，形状为（out_channel，in_channel/groups默认为1，Hk，Wk），也就是说，有out_channel x in_channel这么多个二维卷积核，对输入的每一个in_channel对应一个卷积核，全部加一起（或者平均？）之后才生成一个输出特征图，想要输出多out_channel个特征图，就得对每一个out_channel再配**一组**卷积核。

​	conv2d方法里传入的weight参数就是一个四维张量，这个四维张量作用于传入的同样是四维的input，产生out put。所以传入的这一大组卷积核都要自己提前写好/生成好，反正就是得提前准备卷积核。

​	Conv2d类中，不需要自己提前准备好这个四维的卷积核组，只需要传入input_channel和out_channel，以及kernel_size，（还有groups）这个类就会自动生成一个服从正态分布的四维卷积核组。

​	![image-20221016155853683](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221016155853683.png)

并且这个卷积核组是可以通过学习来改变的，通过Conv2d.weight变量可直接访问。



![img](https://img-blog.csdnimg.cn/20191019210408246.png#pic_center)



​	**其它参数讲解：**

​	**in_channels**、**out_channels**、**kernel_size**、**groups**(用于分组，一般设置为默认的1)用于生成随机初始化的卷积核组

​	**kernel_size**、**stride**、**padding**、**dilation**用于计算生成的图像的尺寸

​			（也就是说，生成图像的尺寸不能直接指定，反而是需要根据生成的尺寸来反向计算stride，padding这些，dilation一般为1）

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221016160205808.png" alt="image-20221016160205808" style="zoom:67%;" />

​	这几个参数既可以是一个int型变量，表示在H和W两个维度上相同，也可以是一个包含两个int的元组，表示在H和W上的两个维度

​	注意：dilation默认为1，表示kernel中的元素见没有间隔，为2才表示有一个间隔

​	**bias**表示是否要在每一个channel上生成的特征图上加一个偏差bias，默认为false，形状为长度是out_channels的一维tensor，这个参数也是可以学习的，可通过Conv2d.bias属性查看。

​	**padding_mode**表示padding的方式，包含'zeros'，'reflect'，'replicate'，'circular'四种方式，

​	默认zero，用0填充

​	reflect表示以矩阵边缘位对称轴，将矩阵中的元素对称的填充到最外围

​	replicate表示将矩阵的边缘复制并填充到矩阵的外围

​	circular就是循环,[按填充后尺寸   中心截取  输入图像尺寸上循环平铺的结果]([PyTorch Conv2d中的四种填充模式解析 - 简书 (jianshu.com)](https://www.jianshu.com/p/a6da4ad8e8e7))

​	**device**表示将实例化的卷积层对象放在哪个设备上使用



### 3.池化

#### 池化的目的是什么？

​	**特征降维**，降低计算资源的损耗

​	池化的思想来源于图像特征聚合统计，通俗理解就是**池化虽然会使得图像变得模糊但不影响图像的辨认跟位置判断**

​	一个形象比喻：1080p到720p

#### MaxPool2d类参数详解

​	具体链接见[官方文档]([MaxPool2d — PyTorch 1.12 documentation](https://pytorch.org/docs/stable/generated/torch.nn.MaxPool2d.html#torch.nn.MaxPool2d))

​	`torch.nn.MaxPool2d`

​	(***kernel_size***, ***stride**=None*, ***padding**=0*, ***dilation**=1*, ***return_indices**=False*, ***ceil_mode**=False*)

​	首先明确，池化操作不会改变特征的channel数，所以不用传入in_channel和out_channel两个参数。

​	then，池化就是按照一定规则在kernel_size窗口内产出一个值，规则固定，所以不存在可以学习的卷积核和bias。

​	与Conv2d类相同，不会直接传入input_tensor，而是先实例化之后再传入input。

​	input和output的形状之后H和W不同，batch_size和channel数都相同，如下图：

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221016170451495.png" alt="image-20221016170451495" style="zoom:67%;" /> 

​	**kernel_size**、**stride**、**padding**、**dilation**四个参数同样用于计算输出H和W

​	stride比较特殊，它的默认值不再是1了，而是kernel_size,意思就是最大池化操作不会让窗口区域重叠。

​	**没有padding_mode**，因为最大池化，取最大值，所以该类会自动在padding区域填充0。（maxpool2d方法会填充负无穷）

​	**ceil_mode**：在窗口区域移动到input图像边缘时，可能会因为窗口太大导致无法填满窗口，如果ceil_mode为true，则会对没填满的地方填上0，再选最大值，并输出给output

​		如果ceil_mode为false，也就是floor模式，则会直接舍弃没填满的区域，也就是说这一个区域不会产生output。

​	所以，ceil_mode会影响output的H和W。

​	其实ceil和floor很形象，分别代表天花板和地板，可以理解为，H和W是根据计算出来Hout和Hin向上取整还是向下取整。

​	**return_indices**：（暂时不是很懂）返回output的同时，返回每一个窗口区域内最大值的索引，后续对[`torch.nn.functional.max_unpool2d`](https://pytorch.org/docs/stable/generated/torch.nn.functional.max_unpool2d.html#torch.nn.functional.max_unpool2d)这个方法有用。



### 4.Normalization层

​	（归一化/正态化而不是正则化！！正则化应该是 regularization）翻译上有正态化和正则化，但其实正则化是不准确的，因为正则化通常表示机器学习中的一种权重惩罚方法，用来防止过拟合、提高泛化能力。

​	对图像处理应该用BatchNorm2d,输入输出形状相同，N x C x H x W。也就是说，不会改变输入形状。

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221016190125528.png" alt="image-20221016190125528" style="zoom:80%;" />

​	将所有的像素点值按照这个方法进行归一化

​	Ex和Var分别是方差，每一个channel求一个，所以数量有C个。

​	γ是权重，β是偏置，作用是对标准正态分布进行变化（变化方差和均值）。对每一个channel求一个，所以它的形状应该为C(跟Batch_size无关！！！)，可以通过属性`.weight`和`.bias`来查看

​	这两个参数不需要传入，BatchNorm类会自动生成这两个变量并赋给初始值1和0（类似于Conv2d中的卷积核，不用传入，同样的，这两个参数也是可以学习的，但还得看affine关键字是否为True）

​	**所有参数**

>  torch.nn.BatchNorm2d (***num_features*,** ***eps**=1e-05*, ***momentum**=0.1*, ***affine**=True*, ***track_running_stats**=True*, ***device**=None*, ***dtype**=None*)

​	**num_feature**:特征图的数量，就是channel，表明γ和β的个数。（RGB图片肯定是3）

​	 **momentum**=0.1，用于学习过程中更新γ和β参数

#### <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221016191301561.png" alt="image-20221016191301561" style="zoom:67%;" />

​		表示新观察到的xti（不是很理解）对参数更新所占的权重。

​	**affine**=True:控制γ和β是否可学习，默认为True，即可学习，false即不可学习。

​	**tracking_running_stats**：暂时不用了解

​	（剩下两个就不解释了）

### 5.DropOut

#### 目的

​	防止模型过拟合：

​	它强迫一个神经单元，和随机挑选出来的其他神经单元共同工作，达到好的效果。消除减弱了神经元节点间的联合适应性，增强了泛化能力。

​	【其它防止过拟合的手段】

​		1.用验证集（validation），当在验证集上效果变差时，提前终止训练

​		2.正则化：L1和L2加权，限制参数

​		3.ensemble手段，训练多个模型，联合判断。（但是这种方法训练成本太高了）

​		4.dropout

​		5.soft weight sharing（暂时不了解）

#### DropOut类

> torch.nn.DropOut2d(***p**=0.5*, ***inplace**=False*)

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221016213403595.png" alt="image-20221016213403595" style="zoom:50%;" />

​	给每一个2维特征图/一维tensorL（”历史原因“）一个概率p，使其置零

​	也就是说DropOut2d包含了DropOut1d的功能，当输入一个三维tensor后，会按照1d的规则识别每一个维度，而不是C,H,W。所以目前的2d还不支持不带batch的C,H,W三维数据的2d置零操作。

​	需要注意的是，DropOut的输入不是神经网络中流动的tensor，而是其它层中的参数，比如Conv2d层、全连接层中的参数。所以DropOut一般在定义其它层的时候会用。

​	（但我感觉其实DropOut2d并不常用，反而是针对每一个元素的DropOut最常用。遇到再说吧）



### 6.损失函数层

#### L1Loss

torch.nn.L1Loss(**size_average** = None , **reduce** = None , **reduction** = 'mean')  

> 注意：在使用import引入某一个类时，不能直接import torch.nn.类名，因为直接使用import是引用包的，应该用from torch.nn import 类名，比如：from torch.nn import L1Loss

size_average和reduce两个参数已经没用了，只用一个reduction参数便可以实现他们两个的功能

​	⭐首先说明，predict和target可以是任意形状，保证它们两个形状相同即可。在实例化L1Loss对象之后，再传入这两个参数，输出一个output

```python
#实例化这个类
loss = L1Loss()
#传入参数
output = loss(predict,target)
```



**reduction**：可以指定三个值，‘none’,'mean','sum'

​	none:只对所有元素进行|x-y|操作，输出output不是标量，而是一个与predict和target相同形状的tensor

​	mean：求所有元素|x-y|的sum，然后除以n，输出一个标量

​	sum：求所有元素|x-y|的sum，不用除以n，输出一个标量

​	

#### MSELoss

​	参数和规则与L1Loss完全相同，只不过把|x-y|换成了（x-y）^2



#### CrossEntropyLoss_交叉熵

​	torch.nn.CrossEntropyLoss()

​	首先说明输入输出：

​	![image-20221017172310032](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221017172310032.png)

Input，也就是predict的输入肯定是N,C或C

target可能是one_hot编码，则与输入形状相同

​			也可能只是一个正确的索引，则会少掉C这一维，即一维长度为N的tensor或标量

输出，如果reduction = ‘sum' 或者‘mean’，就是一个标量

​			如果reduction = ‘none’，则与Target形状相同（一般不用）

​	⭐参数：

​			只理解一个reduction就好，其它不用管f



### 7.PyTorch结构划分

torch

**初始化tensor的一些方法：**

torch.normal()正态分布   /   torch.randn()标准正态分布（mean=0,std=1）

torch.ones()  /  torch.zeros()

torch ones_like()  /  torch.zeros_like()

**有关网络构建**

torch.nn  

​	torch.nn.functional

​	torch.nn.Parameter

​	torch.nn.Conv2d等

​	torch.nn.init.normal_/randn_()  使用normal或者randn修改tensor的值

​	nn里还有损失函数 torch.nn.MSELoss()

**优化器**:

torch.optim

**激活函数**

torch.relu/torch.sigmoid等 

**其它功能函数：**

torch.max(a,b)

torch.min(a,b)

​		输出一个tensor，形状与a，b相同，其元素值为a，b中的max/min值

torch.norm(input, p=2)

​		求input的Lp范数



### 8.自定义loss/updater和pytorch自带loss/updater使用上的区别



>  d2l上有自定义的loss和updater，在反传时于pytorch自带的loss和updater在用法上有一些区别



**自定义的**：

```python
# 自定义的loss
def squared_loss(y_hat, y):  #@save
    """均方损失"""
    return (y_hat - y.reshape(y_hat.shape)) ** 2 / 2
# 自定义的sgd
def sgd(params, lr, batch_size):  #@save
    """小批量随机梯度下降"""
    with torch.no_grad():
        for param in params:
            param -= lr * param.grad / batch_size
            param.grad.zero_()
```

 求loss的时候保持了维度，相当于reduction = ’none‘

​		但是反向传播的时候又不能用向量求导，所以需要loss.sum().backward() 

sgd在更新梯度时候除以/batch_size，是因为loss.sum()，如果是loss.mean().backward()，就不用/batch_size了（自带的就是这样做的



**pytorch自带的：**

![image-20230317200547577](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230317200547577.png)

loss默认损失是mean，所以反向传播的时候直接 loss.backward()就可以

updater里的源代码肯定也没有除以batch_size



⭐d2l中train_ch3函数传入loss的理解：

​		可以看到该方法同时传入loss和updater，按照我们前面的思维惯性，这里传入的要么都是自定义的，要么都是pytorch自带的。

​		但在这里，传入的trainer是pytorch自带的，loss却不是按默认reduction=’mean‘,为什么？

​		![image-20230317201318025](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230317201318025.png)

​		看下train_ch3的源代码就知道了：

![image-20230317201253856](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230317201253856.png)

​		其实reduction = ’none‘就等价于d2l中自定义的square_loss，二者传入哪一个都可以，但是不能传入默认的mean（传入就不能随意切换mean和sum了

​		对它sum()就可以跟自定义的updater搭配，对它求mean就可以跟pytorch的updater搭配

## 各种网络

### 	Resnet

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230315192424313.png" alt="image-20230315192424313" style="zoom:50%;" />





# hugging face

## 1.raw_dataset的tokenize

>  raw_dataset可以用datasets模块加载

```python
from datasets import load_dataset

# 前面表示这个dataset的名字，后来就是config（dataset_server中的），也有的dataset没有config,那就不用写或者等于default
raw_datasets =  load_dataset("glue", "mrpc")

# 查看加载的这个数据集的结构
print(raw_dataset)
```

<img src=".\picture\屏幕截图 2023-09-14 220509.png" alt="屏幕截图 2023-09-14 220509" style="zoom:67%;" />

注意：这种方式加载所有的数据集，如果只是**查看某个大数据集中的某几条数据/查看数据集状态/在某数据集中进行查询**之类的操作，并不需要加载整个数据集，这时候才需要dataset_server



> tokenize的流程

​	🚩首先应该意识到，模型和任务类型应该是匹配起来的：

​		因为checkpoint能同时决定模型和tokenizer,也就是说，模型确定了，它对应的tokenizer就确定了，		   		tokenzier处理raw_dataset的方式是不一样的，对应着某一种固定的任务。即，**在hugging face中**，每一种		模型都对应着一种下游任务

​		又比如，判断两个句子关系的模型，会传入token_type_ids，而其他任务不会传入这个，所以并不是随便一		个模型都能适应于其他nlp任务的

​	也就是说，llama2大模型用于QA和chat_completition，可能并不适用于情感判断这些下游任务



​	🚩开始讲解：

​	拿到了数据集，我们就知道要做的任务是哪一种了，可以到hugging face官方网站上根据任务类型查询相关的模型，并将模型名字字符串给到checkpoint。

​	然后根据checkpoint得到tokenizer(和model

​	用于不同任务的tokenizer传入的参数（比如几个句子）是不一样的，这样应该搞清楚

​	根据raw_dataset结构和tokenizer用法，写一个tokenize_function

```python
# 根据checkpoint加载tokenizer
from transformers import AutoTokenizer
checkpoint = "bert-base-uncased"
tokenizer = AutoTokenizer.from_pretrained(checkpoint)

# 在这一步，无论raw_dataset的结构是什么样的，都可以进行
# map的作用就是将raw_dataset的每一条都扔给tokenize_function处理
tokenized_datasets = raw_datasets.map(tokenize_function, batched=True)

# 根据raw_dataset结构和tokenizer用法，写一个tokenize_function
def tokenize_function(example):
    # padding这里应该是按照默认的longest,不然后面的input_ids不会不一样
    return tokenize(example["sentence1"], example["sentence2"], truncation=True)

# 这里的batched=True并不是直接返回分好的batch_size为1000的数据集，而是将未处理的数据分为batch送给tokenize_function,而不是一条条的处理，处理好后再把所有的batch合并起来，这样做只是为了提高处理速度！！

```

​	得到的tokenized_datasets如图，我们需要的只是蓝色部分，红色部分的sentence1/2和idx其实已经不需要了。

![](.\picture\image-20230914230720236.png)



> 从tokenized_datasets中提取需要的数据

​	上面可以看出，tokenized_datasets并不是我们最终需要的直接传入模型的数据，一方面它包含了train/val/test的所有数据，另一方面它包含sentence1/2和idx这些用不到的信息

```python
# 抽取出train和test的数据
train_samples = tokenized_datasets["train"]
test_samples = tokenized_datasets["test"]

# 剔除不需要的列
train_samples = {k: v for k, v in train_samples.items() if k not in ["idx", "sentence1", "sentence2"]}
test_samples = {k: v for k, v in test_samples.items() if k not in ["idx", "sentence1", "sentence2"]}

# 查看前八个训练样本的input_idx的长度
[len(x) for x in train_samples["input_ids"][:8]]
输出： [50, 59, 47, 67, 59, 50, 62, 32]
```



> "DataLoader"

​	这一步是为了发挥DataLoader的作用，但是batch_size不需要在这里传入，而是在TrainingArguments类的对象里传入Trainer()   

​	batch_size和data collator传入Trainer后，Trainer对象将数据划分为一个个的"未封装"batch,然后将它们一个个交给data collator处理，所以data collator的作用就是**不管给他多少的数据，都把它封装为长度相同的一个batch!!!**   ![](.\picture\image-20230915061724174.png)

​	注意看，上面写的是**a** batch!!

​	为什么还要WithPadding呢？

​		上面的前八个可以看到长度不同，如果每一个input[ids]只是被单独用于一句话的推理，那么它自身就是所有		数据，保持自己的长度就可以了，但是现在要进行的是训练，不止是自己了，所有的都要保持相同的长度。

​	这里DataCollatorWithPadding不会显示的传入

```python
from transformers import DataCollatorWithPadding

# 用于生成data_collator对象
data_collator = DataCollatorWithPadding(tokenizer=tokenizer)

# 试一下data_collator的效果（实际在hugging face框架内我们不会手动用collator，而是将其传入Trainer对象
batch = data.collator(train_samples[:8])
{k:v.shape for k, v in batch.items()}

输出：
{'attention_mask':torch.Size([8, 67]),
 'input_ids':torch.Size([8, 67]),
 'labels':torch.Size([8]),
 'token_type_ids':torch.Size([8, 67])
}
# 这里将传入的八个图像全部存入一个batch中了
```

## 2.使用Trainer进行训练

> 五个基本参数

- model:必须是包含后处理模块的，比如model = AutoModelForSequenceClassification.from_pretrained(checkpoint,  num_labels=2)

- args:

  ```python
  from transformers import TrainingArguments
  training_args = TrainingArguments(output_dir="test_trainer", evaluation_strategy="no") 
  # 指定存放模型checkpoint的文件夹，这个也算是超参数，其他超参数都有默认值，可以默认也可以指定
  # evaluation_strategy表示多久查看一次训练结果，no是从不查看，还有steps和epoch两个参数
  # 超参数的默认值详见：https://huggingface.co/docs/transformers/v4.33.0/en/main_classes/trainer#transformers.TrainingArguments
  ```

- train_dataset：由tokenize处理完的数据（一般通过map,效率比较高，但不一定非得用map）

- test_dataset：同上

- data_collator：好像也是非必要

- compute_metrics = compute_metrics

  ```python
  import numpy as np
  import evaluate
  from datasets import load_metric
  
  # 可以自定义
  metric = evaluate.load("accuracy")
  # 也可以加载数据集自带的评价标准
  metirc = load_metric("glue", "mrpc")
  
  # 然后装入下面这个函数，写法比较固定，不必深究为什么，就是先解包然后用metric
  def compute_metrics(eval_pred):
      logits, labels = eval_pred
      predictions = np.argmax(logits, axis=-1)
      return metric.compute(predictions=predictions, references=labels)
  ```

  ![image-20230915065035687](.\picture\image-20230915065035687.png)

- tokenizer：非必要



> 非常简单的训练过程



```python
from transformers import Trainer

# 先实例化
trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=small_train_dataset,
    eval_dataset=small_eval_dataset,
    compute_metrics=compute_metrics,
)

# 然后训练
trainer.train()
```

