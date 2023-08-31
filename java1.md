## 记录1   javac编译-汉字编码问题

🚩2022.8.26

>  问题描述：javac编译Hello.java程序时出现错误，如下图



<img src=".\picture\image-20220826163334070.png" alt="image-20220826163334070" style="zoom:50%;" />

**问题分析&解决方法：**

​	DOS工作台默认汉字编码是GBK，而sublime默认汉字编码是utp-8

​	[java 错误: 编码GBK的不可映射字符 - Marydon - 博客园 (cnblogs.com)](https://www.cnblogs.com/Marydon20170307/p/15548013.html)



**其他方法**：

​	直接在sublime中修改Hello.java文件的编码格式：

​	**File  → Save with encoding  →  GBK（Chinese Simlified）** 即可，功能为以GBK编码方式保存java文件中的汉字

​	若Save with encoding里没有GBK格式，则需要以下措施：

* ctrl+shift+p  →  搜索install  →  选择Package Control:Install Package  →  跳出插件包选择界面  →  搜索convertToUTF8  →  选中，直接安装

  <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826201153027.png" alt="image-20220826201153027" style="zoom:50%;" />

（会跳出一个Package Control Messages文件，不用管它，直接关掉就可以）

* 再点击File选项，发现多出了**Set File Encoding to**和**Reload with Encoding**

* **Set File Encoding to**选项内第一项就是我们要的GBK编码格式

  <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826201431767.png" alt="image-20220826201431767" style="zoom:50%;" />





## 记录2：(sublime)Package Control安装问题

🚩2022.8.26

> 问题描述：在sublime中用快捷键ctrl+shift+p启动对话框后，在对话框中输入Install Package Control（一个控制包的包）出现如下显示问题：
>
> ​		an error occurred installing package control

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826163853378.png" alt="image-20220826163853378" style="zoom: 50%;" />



**问题分析**：

​	可能因为连接不到下载该包的网络，也可能因为sublime版本过低



**解决方法**：

​	上述介绍方法是点击下载的方法，也可以[手动下载该包](https://packagecontrol.io/Package%20Control.sublime-package)，然后将其部署到正确的文件夹中

* 1.在sublime中点击Preference选项  >  Browse Package 打开一个文件夹

* 2.打开这个文件夹的上一级文件夹

* 3.找到Installed Packages文件夹，将下载的包放到该文件夹内即可

* 4.重启sublime，使用快捷键ctrl+shift+p启动对话框，搜索Install Package即可看到Package Control：Install Package選項，如下圖

  ![image-20220826165137971](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826165137971.png)



> 又出现了新问题：
>
> 点击上面的选项，应该跳出**插件包选择界面**，如下图
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826173148471.png" alt="image-20220826173148471" style="zoom:50%;" />
>
> 但是却出现error：
>
> ​	Package Control 
>
> ​     There are no packages available for installation
>
> 也就**依然无法通过Package Control来安装工具包**



**问题分析**：

​	需自动下载**channel_v3.json**配置文件，但是又双叒叕是网络原因，导致无法下载



**解决方法：**

​	跟上面解决方法一样，无法自动下载，我们收[手动下载channel_v3.json](https://files-cdn.cnblogs.com/files/xiaojianwei/channel_v3.rar)并进行配置:

* 1.下载之后得到一个压缩包，将里面的channel_v3.json解压到任意一个文件夹里
* 2.在sublime里点击：**Preferences->Package Settings ->Package Control ->Settings-User**

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826174046854.png" alt="image-20220826174046854" style="zoom: 50%;" />

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826174443407.png" alt="image-20220826174443407" style="zoom:50%;" />

* 3.修改打开的这个配置文件：

  ​	加入”channel“这一项，内容是刚才放置channel_v3.json的绝对路径（win系统用/分隔即可）

* 4.重启sublime，就能出现**插件包选择界面**了！

  



## 记录3：知识点笔记

🚩2022.8.26

- **0016 Oldwang is studying java**：

> 1、如果要将文件名由Hello改为其它名字，则类名也要改否则会出现下面这种情况
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826203815502.png" alt="image-20220826203815502" style="zoom:50%;" />
>
> ​		类名是Hello，文件名为oldwang.java,报错
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826203850311.png" alt="image-20220826203850311" style="zoom:50%;" />
>
> ​		类名是Oldwang，文件名为oldwang.java,报错
>
> 2.类名首字母必须得大写，从而java文件名首字母也要大写，否则会出现以下情况：
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220826204155676.png" alt="image-20220826204155676" style="zoom:50%;" />



- **知识点笔记**：

> 1.“.java"文件为源文件， “.class”文件为字节码文件**（0016）**
>
> 
>
> 2.一个源文件中只能有一个public类，其他类的个数不限**（0017）**
>
> ​	若有多个类，编译后（javac）每个类都会生成一个class文件
>
> 
>
> 3.Java应用程序执行入口是main（）方法，它有固定的书写格式： public static void main(String[] args){...} 
>
> ​	如果源文件中包含一个public类，则文件名必须按该类命名！
>
> ​	**main()方法可以在非public类中！！public和非public类中可以同时拥有main（）方法！！！！**然后指定运行非public方法，这样入口方法就是非public的main()方法
>
> 4.类、方法的注释要以javadoc的方式来写**（0025）**
>
> 
>
> 5.tab可以使代码块整体右移，shift+tab整体左移
>
> 
>
> 6.编程规范：源文件汉字编码要使用utf-8编程方法（之前用GDK是为了配合在dos系统下进行编译，实际工作中GBK用的不多）
>
> 
>
> 7.**行尾风格**（自己平时用的）和**次行风格**
>
> 
>
> 8.<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220827172213714.png" alt="image-20220827172213714" style="zoom: 80%;" />
>
> 9.DOS，**Disk Operating System**,磁盘操作系统
>
> 
>
> 10.<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904152825679.png" alt="image-20220904152825679" style="zoom: 33%;" />（0045
>
> 
>
> 11.<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904152851783.png" alt="image-20220904152851783" style="zoom: 33%;" />（0046）
>
> 
>
> 12、ASCⅡ编码、Unicode编码、UTF-8编码 辨析：
>
> ​	![image-20220904160201964](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904160201964.png)
>
> ​	编码间转换的一个网址:[Unicode编码转换 - 站长工具 (chinaz.com)](https://tool.chinaz.com/Tools/Unicode.aspx)
>
> 13、**自动类型转换**是指：
>
> ​			**精度小**的数据类型自动转化为**精度大**的数据类型（在java中进行赋值或者运算时）
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904161954985.png" alt="image-20220904161954985" style="zoom:50%;" />
>
> ​			(byte,short)和char之间不会进行相互转换，但是三者间可以进行计算，计算之前首先转换为int类型
>
> ​			boolean不参与转换
>
> ​			当把精度（容量）大的数据类型赋值给精度（容量）小的数据类型时，**就会报错**  	（⭐如果加上**强制转换符**就不会报错了）
>
> 
>
> 14、**强制类型转换**细节：
>
> ​		char类型可以保存int的常量值，但不可以保存int类型的变量值
>
> ​														![image-20220904164533929](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904164533929.png)
>
> 
>
> 15、（0058）
>
> ​		将String类型转为基本数据类型时，**要确保String类型能够转换成有效的数据**，否则会在运行（java而不是javac）时出现**Unkonwn Source**错误，**抛出异常，程序终止**
>
> ​					<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904170654640.png" alt="image-20220904170654640" style="zoom:50%;" />
>
> ​			<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220904171050026.png" alt="image-20220904171050026" style="zoom: 50%;" />
>
> 
>
> 16、奇怪的自增运算符：
>
> ​			<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220905081906290.png" alt="image-20220905081906290" style="zoom:50%;" />
>
> ​	
>
> 17、**复合运算符**会进行类型转换
>
> ​			
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220905182915456.png" alt="image-20220905182915456" style="zoom:50%;" />
>
> 18、Java标识符命名**规则**和**规范**：
>
> ​			（凡是可以自己起名的都叫标识符，包括各类变量、方法、类等）
>
> **规则**：(必须遵守)
>
> 1. 由26个英文字母和 **_ ** 与  **$ **组成
>
> 2. 数字不可开头
>
> 3. 不可以直接使用**关键字**和**保留字**，但是可以包含它们（<font color=red>保留字</font>：现有java版本尚未使用，但以后版本可能会作为关键字使用）
>
>    保留字包括：byValue，cast，future，generic，inner，operator，outer，rest，var，goto，const等
>
> 4. 严格区分大小写，长度无限制
>
> 5. 不能包含空格
>
> **规范**：（最好遵守、显得专业）
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220905191745890.png" alt="image-20220905191745890" style="zoom:67%;" />
>
> 
>
> 19、java中没有无符号数，也就是unsigned
>
> ​		计算机中数字的运算，都是以补码的形式，也就是补码加法器**（但将运算结果转为十进制还需要转换为源码）**
>
> ​		所以**位运算符**（&  |  ^  ~  >>   <<   >>>）的运算对象也是**补码**
>
> 
>
> 20、运算符优先顺序：
>
>  										<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220905204703692.png" alt="image-20220905204703692" style="zoom: 67%;" />
>
> 
>
> 21、关于**switch**：
>
> ​		① switch后表达式的数据类型应该和case后常量的**类型一致**，或者是可以**自动转化**成相互比较的类型
>
> ​		② switch表达式中的返回值必须是：**byte，short，int，char，enumerate枚举，String类型**
>
> ​				不能是boolean，float，double这些
>
> ​		③case后的值**必须是常量**，不能是变量或者表达式
>
> 
>
> 22、**while(true) + break**  可以把循环的控制权完全交给break，while只提供循环的“动力”，不用管啥时候退出
>
> 
>
> 23.jvm的 **二维数组内存形式**
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220913142206388.png" alt="image-20220913142206388" style="zoom: 67%;" />
>
> 
>
> 24.二维数组的三种声明方式（int型数组举例）：
>
> ​	![image-20220913155340379](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220913155340379.png)
>
> 25.声明数组的注意事项：
>
> ​	一般可以用  int arr[] = new int[3]  这种形式
>
> ​	后面的3也可以不写，用具体的{xx,xx,xx}替代，如下图所示，CE不行，但D就可以
>
> ​		<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220914141611721.png" alt="image-20220914141611721" style="zoom:50%;" />
>
> 
>
>  26.field表示类的属性/成员变量，见到不要惊讶。
>
> 
>
> 27.这种对数组先声明再创建的方法是可以的
>
> ​				<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220916100544858.png" alt="image-20220916100544858" style="zoom:50%;" />
>
>  28.同数组一样，如果类中的属性不赋值，则有默认值：
>
> ​		int,short,byte,long的初始值为0，float,double的初始值为0.0，boolean初始值为false，String初始值为 null，char初始值为 \u 0000
>
> 
>
> 29.java中对于实参和形参的定义有点诡异：
>
> ​	方法定义时的参数叫做形参，方法调用时传入的参数叫做实参。
>
> ​	没有什么好诡异的，c++也这样叫，只不过把形参实参的分类与30条传值与传引用的分类搞混了！！！
>
> ​	java不会改变传入的参数！！  <font color ='red'>×××</font>
>
> ​	会的！，看30条解释！
>
> 
>
> 30.也许这一条能统一上一条的思想：
>
> ​	基本数据类型传入的直接就是值，相当于c++的传值（传拷贝）
>
> ​	引用数据类型传入的是地址，相当于c++的传引用<font color='blue'>又理解错了!!蓝色是最新的统一理解！！</font>
>
> ​	<font color='blue'>java只有传值，不管传什么东西进去，都不能改变这个东西本身！！传进去的只是一个副本！！！</font>
>
> ​	<font color='blue'>传基本数据类型就不用说了，如果传的是引用数据类型，实际上是地址的副本，在传入的方法中改变这个地址的副本，并不会原本的地址，但是可以改变地址指向的内容！！！</font>
>
> ```java
> public static void main(String[] args) {
>         int[] nums = {1,2,5,3,4,-1,6};
>         TreeNode root = TreeNode.buildTree(nums);
>         //对比
>         TreeNode.printLevelOrder(root);
>         flatten(root);
>         TreeNode.printLevelOrder(root);
>     }
> public static void flatten(TreeNode root) {
>     ArrayList<Integer> preOrderlist = new ArrayList<Integer>();
>     //存储先序遍历的结果
>     preOrder(root, preOrderlist);
>     //创建新的二叉树存储结果
>     if(root != null){
>         root = create(preOrderlist, 0);
>     }
> }
> 
> 上述代码，将root传入flatten并进行了修改，两次输出的结果并不会有差别，说明root = create(preOrderlist, 0);只是改变了flatten方法中的root的副本，并不会改变main中的root。
> ```
>
> ​	传入基本数据类型，就是不会改变
>
> ​	而传入引用数据类型（也就是自定义的类的对象），会影响到对象原型！！(错了！不会影响对象原型)但是不会影响到String类型（视频471），原因如下：
>
> ​		String的value数组是private final的，而且是存在常量池的，对value的修改无非两种：
>
> ​			想直接value[i]的值，final是同意的，但是private可不同意
>
> ​			那调用String内部的public方法总可以了吧，比如concat，看完以下代码就懂了
>
> ```java
> public class StringDetai {
>     public static void main(String[] args) {
> 
>         String a = "hello";
>         System.out.println
>             ("a的hashcode "+ a.hashCode() + 
>              "\na用过concat之后的hashcode " +
>              a.concat("abc").hashCode());
>     }
> ```
>
> ![image-20221104202544864](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221104202544864.png)
>
> ​			（可以理解为。value就是不可以改变的，因为它在常量池中独一份，你如果想要其它的value值，那你原来的value才不会配合你，你自己再去常量池找一个或者创建一个指向它吧！）
>
> ​			懂了把，用完concat之后返回的引用已经与原来不同了，也就是说如果想要把str传入某个方法中用concat，用完之后的确会改变传入的副本引用，但是方法外的原型引用并不会变。
>
> ​			实际上，永远不能改变传进去的东西的原型本身，传引用之所以能”改变“，改变的并不是该引用，而是该引用指向的其他内容。
>
> 31.java类中的方法重载：
>
> ​		方法名必须相同
>
> ​		形参类型/顺序/个数  至少有一样不同
>
> ​		方法返回类型 不能决定是不是重载（同时满足上面两个条件就是重载，否则不是重载）
>
> 
>
> 32.**可变参数**的参数可以当数组用（用参数名当数组名即可）
>
> ​	可变参数的本质其实就是数组
>
> ​	可变参数可以和普通类型参数一起放在形参列表，但必须保证**可变参数在最后**
>
> ​	一个形参列表中只能出现一个可变参数
>
> 
>
> 33.在java中的变量可分为两类：
>
> ​			属性（全局变量/成员变量）	和	局部变量（方法和代码块中定义的变量）
>
> ​	属性的作用域为整个类体，可以不赋值，直接使用（因为有默认值）
>
> ​	局部变量的作用域为它的代码块&方法，必须复制后再使用（因为没有默认值）
>
> ​	（代码块就是用大括号括起来的一段代码）
>
> ​	属性与局部变量可以重名（访问时遵循就近原则），但是同一方法中的两个局部变量不可以重名
>
> ​	属性/全局变量可以加修饰符，但是局部变量不可以加修饰符	
>
> 
>
> 34.java**（类的）构造器**的三个特点：
>
> ​	构造器其实就是一种由系统完成的特殊的方法
>
> ​	1.方法名和类名相同
>
> ​	2.没有返回值（不用写void！！）
>
> ​	3.在创建对象时，系统自动调用该类的构造器完成对象的初始化
>
> 
>
> 35..java**（类的）构造器**的使用细节：
>
> ​	1.构造器也可以重载，用以完成不同类型的初始化
>
> ​	2.一旦定义了自己的构造器，默认的构造器就被覆盖，无效了
>
> ​		Dog d = new Dog( ); 这句话也就不能用了
>
> ​		除非显示地在类里再定义一下
>
> ​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220918213100379.png" alt="image-20220918213100379" style="zoom:50%;" />
>
> 
>
> 36.javap 反编译工具：
>
> ​	使用流程：
>
> ​	.java原文件中有多个class，经javac编译后会生成多个.class文件
>
> ​	对任一个.class文件（字节码文件，也可以不写.class后缀名），都可以使用javap命令，比如  javap Dog.class，
>
> ​	就可以查看这个类的源文件（可以看到编写源文件时不显示的默认构造器）
>
> 
>
> 37.在类中用this访问构造器：
>
> ​		1.只能在一个构造器中访问另一个构造器，不能在普通方法中用this访问构造器
>
> ​		2.this(形参1，形参2，形参3)
>
> ​		3.只能放在构造器的第一句
>
> 
>
> 38.java包的命名规则：
>
>  - 只能包含数字、字母、下划线、点（分隔文件，比如com.公司名.项目名.业务模块名）
>  - 数字不能开头
>  - 报名不能是关键字或者保留字
>
> 
>
> 39.java常用包
>
> **java.lang**.*	基本包，默认引入，int、boolean、String、System等不用引入就可以使用的类（基本数据类型）和方法（如Math.abs()）,都属于这个包
>
> **java.util.***	java提供的工具包，如Scanner
>
> **java.net.***	网络包，用于网络开发
>
> **java.awt.***	做java界面开发的工具包，GUI
>
> 
>
> 40.引入包和类：
>
> ​	import java.util.Scanner  是引入了一个类，所以最后面不加星号
>
> ​	如果想引入某个包里的所有的类，要加*
>
> ​	比如：import java.util.*
>
> ​		(建议：**用到哪个类就导入哪个类**，不建议用*，因为导入太多了会导致程序运行变慢)
>
> 
>
> 41.Java访问修饰符：
>
> ​	用于控制对**类**、**方法**和**属性**的访问权限（只有默认和public才可以修饰类！！！）
>
> ​	public	对外公开（对**所有其它类**公开）
>
> ​	protected	对**类本身**、**同一个包中的类**、**子类**公开
>
> ​	默认级别	对**类本身**、**同一个包中的类**公开
>
> ​	private	只对**类本身**公开（如果子类和父类在一个包里，就可以访问父类的默认属性和方法了）
>
> ​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220921135304274.png" alt="image-20220921135304274" style="zoom:67%;" />
>
> ​	其实这样理解更加合理：
>
> ​		在其它包里只能访问public
>
> ​		在子类中只能访问public和protected（如果子类和父类在同一个包里，）
>
> ​		在同一个包内可以访问只有private不能访问
>
> ​		在一个类中全部都能访问
>
> 42.
>
> ​	**封装**：encapsulation,encap简写
>
> ​	封装其实就是一种类的定义规则，让类之外的其它方法只能通过该类提供的接口（方法）访问其属性，而不能直接访问属性
>
> ​	这就需要一定的规则来定义类：
>
> ​	1.属性私有化 private
>
> ​	2.公有的setXxx来验证要赋给xxx私有变量的值是否符合要求，如果符合要求，就赋给这个私有变量
>
> ​	3.公有的getXxx来对类的私有变量进行访问
>
> 
>
> 43.super（）和this（）其实机理一样：
>
> ​	二者都与类同名，所以都可以当作构造器使用
>
> ​	二者当构造器使用时，都只能在构造器中被调用，
>
> ​	且必须在构造器第一行，且二者在一个构造器中都只能出现一次
>
> ​	因为二者本质上没啥区别，所有一个构造器中不能同时出现this()和super()
>
> 
>
> 44.java中所有自定义的类都是Object类的子类
>
> ​	Object类是java.lang包中的一个类，与int，Byte，boolean都是同一级别的“基础设施”！
>
> 
>
> 45.方法覆盖/重写（不是重载！！！）的注意事项：
>
> ​	① 子类方法的形参列表和方法名称要和父类的完全一致，子类方法的返回类型要么跟父类相同，要么是父类的子类。
>
> ​	② 子类方法不能缩小父类方法的访问权限（权限从大到小为：public、protected、默认、private）
>
> 
>
> 46.多态分为：
>
> ​	1.方法多态
>
> ​	2.对象的多态：对象多态的前提是两个对象存在继承关系，根据谁继承谁可分为**向上转型**和**向下转型**：
>
> ​		向上转型不多说了，几个注意点参考韩顺平的pdf
>
> ​		向下转型总结一下：
>
> ​				定义方法：（前提，Dog和Cat都是Animal的子类）
>
> ​					语法：**子类类型  引用名 =  （子类类型）  父类引用 ；**（只能是父类引					用而不能是父类对象，比如Animal animal = new Animal();就是父类对					象）
>
> ​					Animal animal = new Cat() ;	（animal为父类引用）
>
> ​					Cat cat = (Cat) animal ；	正确
>
> ​					Dog dog = (Dog) animal ; 	错误	  （强制转换引用的类型）
>
> ​					上面对比说明父类的引用指向的必须是当前目标类型的对象（运行类型必					须是当前的目标类型）
>
> ​					不同于向上转型不能访问子类中的特有成员，向下转型后可以访问子类类					型中的所有成员（成员是成员变量和成员方法的统称，而不只是成员方					法）
>
> ​				（理解）：虽然animal和cat两个引用都指向一个Cat对象，装的成员都是
>
> ​					样的，但是该引用能不能调用其指向的成员中的方法其实是在编译过程中					决定的，如果编译类型（引用的类型）与指向对象的类型（运行类型）相					同，便可以调用其所有成员，如果编译类型是运行类型的父类，那就不能					调用该运行类型特有的成员，也就是说，等号左边决定引用的编译类型，					引用的编译类型也可以通过强制类型转换来改变，new 后面才是定义对象					的部分。
>
> ​			注意：向下转型都是在向上转型之后的，一般用于解决向上转型后不能访问子类特有成员的问题
>
> ​			**如果父类与子类有重名属性**，要看编译类型，也就是引用是什么类型（而不是从子类查到父类，因为属性没有重写）
>
> ​			如果向上转型，那就应该是父类的属性，如果向下转型，那就应该是子类的属性
>
> ​			<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220926135711704.png" alt="image-20220926135711704" style="zoom:50%;" />
>
> ​			<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220926135737947.png" alt="image-20220926135737947" style="zoom:50%;" />
>
> ​			（学到目前的浅显理解，不一定对，但目前来看逻辑融洽 2022.09.26）
>
> ​			对比方法和属性的不同规则可以感知到，java的引用不只是一个简单的指针，c++把内存分为栈和堆，而java把内存分为栈、堆还有方法区，这就决定了：c++的指针只是保存了指向栈中的位置，而java的引用包括一个指针（由栈指向堆）还有在堆中的一个”引用体“，里面有基本数据类型属性的对象，引用数据类型属性的指针和指向方法的指针。			所以对方法进行强制类型转化不仅仅是改变一个指针指向的类型，而是多个方面的：
>
> ​			1.将栈指向堆的指针的类型改为新的类
>
> ​			2.将类中的属性初始值改变（不管是基本数据类型还是引用类型）
>
> ​			3.改变指向方法的指针信息（指向运行类型在方法区中的方法）
>
> 47.**动态绑定机制**：（感觉跟前面内容差不多）
>
> ​		从子类往上查找方法的过程中，可能查到的方法里又有重名方法和重名属性：
>
> ​		1.当调用对象的方法时，该方法会和该对象的运行类型绑定，从运行类开始网上查找，如果里面还有方法，就继续从运行类往上找
>
> ​		2.重名属性在哪一类的方法里，就用该类对应的属性
>
> ​		很微妙，还是看韩老师给的举例，理解更透彻
>
> 
>
> 48. 非静态方法既可以直接访问（所属类的）静态数据成员 又可以访问非静态数据成员，
>
>     而静态方法只能直接访问（所属类的）静态数据成员，若要访问所属类的非静态数据成员，需要先实例化所属类
>
>     静态方法中，不能使用super和this关键字
>
>     [静态方法和非静态方法区别](https://zhuanlan.zhihu.com/p/258751142#:~:text=1 静态方法不能调用非静态的方法和变量.（ 非静态方法可以任意的调用静态方法%2F变量,） 2 不能使用this和super关键字（属于类级别，没有创建对象签不可用this%2Fsuper）)
>
> 49.static修饰的方法叫做静态方法		static修饰的变量（类中）叫做类变量（与成员变量相对）
>
> ​	
>
> 50. == 和 equals（）辨析：
>
>     equals只能判断引用数据类型是否相等
>
>     ​	只判断地址是否相同（因为是最简单的Object的方法，所以只能判断地址是否相等，其底层代码就是return（this==obj），可以看到它的底层原理也是由==实现的），子类中往往会重写该方法，用于判断内容是否相同（如**String**	**Integer、boolean都是Object的子类**！！！）
>
> 
>
>     ==既能判断引用数据类型，又能判断基本数据类型
>                     
>     ​	当判断基本数据类型时，只判断值是否相等即可，比如10==10.0 结果为true；
>                     
>     ​	当判断引用数据类型时，只判断地址是否相等（是Object类equals方法的底层逻辑）；
>                     
>     （String在==看来是引用数据类型，如果用==比较两个字符串的话会只看地址不看内容，所以判断两个字符串是否相同还是得用equals(）;
>
> 
>
> 51.int与Integer
>
> ​		int是基本数据类型
>
> ​		Integer是引用数据类型 （int的包装类）    一定不要搞混了！！！
>
> ​		可以Integer in = new Integer（100）；//手动包装
>
> ​		也可以Integer in = 100;   //自动包装
>
>  			无论是不是new生成的Integer变量，与int变量比较（==），只要值相等，结果就为true
>
> ​			Integer之间比较，如果是第一种生成方法，则==只比地址，equals（）比数值
>
> ​			如果是第二种生成方法，则在[-128，127]之间==比数值是否相等，如果有一个不在这个区间内，直接为false（如果两个都不在，那么new的对象不同，如果有一个在另一个不在，new的对象也不同。具体原因要看底层代码或者记录7 -- 包装类 -- Integer的创建小节的解释）
>
> 
>
> 52.哈希值主要是根据地址号来的，但不能完全将哈希值等价于地址（是由内部地址转化来的整数），HashCode可以看作java虚拟机上的地址，真正内存上的地址是内部地址。二者通过JVM转换。
>
> ​			Object提供HashCode方法主要是为了提高具有哈希结构的容器的效率
>
> ​			在后面的集合中，HashCode如果需要的话，也会重写（重写场景目前接触不多）
>
> 
>
> 53.toString方法
>
> ​	Object的toString方法默认返回  全类名（包名+类名）+@+十六进制形式的哈希值
>
> ​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220926204757637.png" alt="image-20220926204757637" style="zoom:67%;" />
>
> ​	子类往往会重写toString方法，用于返回对象的属性信息
>
> <img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220926205230514.png" alt="image-20220926205230514" style="zoom:67%;" />
>
> ​           	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220926205300634.png" alt="image-20220926205300634" style="zoom:67%;" />
>
> ​	当直接输出一个对象时，toString 方法会被默认的调用
>
> ​	举例：System.out.println(monster); //等价 monster.toString()  
>
> 
>
> 54.垃圾对象被回收，就是将这个对象从堆中清除
>
> ​	 垃圾对象就是没有没有任何引用的对象，回收由jvm的垃圾回收机制完成
>
> ​	 回收前，垃圾回收机制会先调用该对象的finalize方法（要么继承object的，要么该类重写的）
>
> ​	可以通过重写finalize，进行一些自己的业务逻辑代码（比如释放资源：数据库的连接，打开的文件等。。
>
> ​	对象变成垃圾后不是马上被回收的，jvm有自己的垃圾回收算法（GC算法）
>
> ​	如果想在代码中立即看到垃圾回收效果/finalize发挥作用，可用System.gc() 主动触发垃圾回收机制
>
> 
>
> 55.instanceof左边是对象，右边是类
>
> ​	用于判断左边对象的运行类是不是右边类或者其子类
>
> ​	看下面代码![image-20220930174853176](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220930174853176.png)
>
>  这个obj，虽然是个引用，但是它既有编译类型，又有运行类型<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20220930180138218.png" alt="image-20220930180138218" style="zoom:50%;" />，**所以，不要一提到引用就觉得是编译类型。而是引用都同时包含了两种类型，比如obj**
>
> ​	传入equals方法后，不管它的编译类型是啥，都被向上转型为Object祖宗类，（所以最后还要来一个向下转型才能使其访问Doctor类的属性）
>
> ​	但是它的运行类型不变，也就是说，不论向上还是向下转型，转的都是编译类型（仔细想想就是这么一回事）
>
> ​	obj运行类型不变，instanceof用的又是运行态，所以可以用来它的”真面目“；
>
>  还有一个点：		为什么最下面的return语句里都直接访问私有属性？
>
> ​	因为这是在本类里的方法啊！
>
> ​	要查看属性的话（除了在方法里this.），不管私有还是共有，都要先声明一个对象，所以并不是声明了对象就不能查看private属性了，而要看在什么样的类里声明的，是自己的类里还是子类里还是同一个包里的类。
>
> ​		（不想想当然以为只有在类中使用this才能访问私有属性！！！）
>
> ​		
>
>   **Object的getClass()方法返回的是运行时类**
>
>  56.对象/引用（反正就是表示对象的那个名字）
>
> ​	编译类型不能变
>
> ​	运行类型可以变
>
> ​	为什么会有编译类型可以变的假象？下面解释：
>
> ​	Cat时Animal的子类
>
> ​	Animal animal = new Cat();  //向上转型
>
> ​	Cat cat = (Cat) animal;
>
> ​	看起来好像animal的编译类型变了，但是看仔细些，真的变了吗？没有吧，**只是向下转型给了一个新变量，animal本身的编译类型并没有变啊**
>
> 
>
> 57. 关于静态变量（类变量）存放位置的不同说法：
>
>     jdk7、8之前存放在方法区
>
>     jdk8以后放在堆里
>
> 
>
>     类变量在类加载（不是new一个对象时，而是编译时就把类加载到方法区内）时生成
>
> 
>
> 58. 在Python3中，所有类都默认继承object，因此object是所有类的父类。这一点与Java是相同的。
>
>      但是Python中允许一个子类继承多个父类，而Java要求一个子类只能继承一个父类。
>
> 
>
> 59. python类方法中的self是怎么回事：
>
>     只有类中的方法才有self参数，python中的普通函数并不会有self参数
>
>     方法中的self参数，其实代表着该类的实例化的对象本身，是对这个对象本身的一个引用。
>
>     相当于java的this，只不过this不用传入
>
> 
>
> 60. python中的**isinstance( )**相当于**java中的instanceof( )**
>
>     不过前者有两个参数，即前者是否未后者或者其子类，用法为：
>
>     ​	isinstance( A，B),其返回值未bool型（A为对象，B为类）
>
>     后者用法为：A.instanceof(B)
>
> 
>
> 61.[python中的Iterable类和可迭代对象](https://cloud.tencent.com/developer/article/1441182)
>
> ​	涉及内容还有：__ iter __内置方法、iter()、next()方法
>
>  	注意：
>
> ​		要分清可迭代对象和迭代器（Iterator）
>
> ​		**可迭代对象**的本质是可以提供一个**迭代器**的对象，**但其本身并不是迭代器**
>
> ​		可迭代对象通过__ iter __ 方法向我们提供一个迭代器，也就是说，一个具有__ iter __ 方法的对象就是一个可迭代对象
>
> ​		iter( )方法其实就是获取可迭代对象的迭代器，语法为：
>
> ​		**obj_iter = obj.iter( )**		obj为一个可迭代对象
>
> ​		obj_iter已经不是一个obj类型的对象了，它是一个迭代器对象，也就是Iterator类型
>
> ​		当obj变为迭代器对象obj_iter后，便可以调用Iterator类的next( )方法，作用是返回迭代器指向位置的数据，语法为
>
> ​		**obj_iter.next( )**
>
> ​		也就是说，next( )是迭代器Iterator的方法而不是原来obj所属类的方法，所以它要在迭代器类中定义（python3中为__ next __ 方法，python2中为对象的next（self）方法）
>
> ​		python要求迭代器本身也是可迭代的（**也就是说迭代器对象本身也是可迭代对象**，下面截图的代码也就合理了），也就是说，迭代器类中也要有__ iter __方法（只要有iter方法就是可迭代对象），所以在我们自己写一个迭代器类的时候，不光要写next方法，还要写一个iter方法，方法要返回一个迭代器（可迭代类的iter也要返回一个迭代器），只要返回自身self就可以了。
>
> ![image-20221004181817940](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221004181817940.png)
>
> ​		这个得解释以下，这里的FibIterator即是一个可迭代类，又是一个迭代器（因为有 next），在for循环里首先把它当作一个可迭代对象，返回它的迭代器，也就是它自己，然后for循环自动调用迭代器的next方法，也就是它自己的next方法。
>
> ​		巧妙！太巧妙了！
>
> ​	
>
> ​		**循环for … in …的本质**
>
> ​		`for item in Iterable` 循环的本质就是先通过`iter()`函数获取可迭代对象`Iterable`的迭代器，然后对获取到的迭代器不断调用`next()`方法来获取下一个值并将其赋值给`item`，当遇到`StopIteration`的异常后循环结束。
>
> 
>
> 62. **JSON**（**J**ava**S**cript **O**bject **N**otation，JavaScript 对象表示法），是存储和交换文本信息的语法，类似 XML。
>
> ​	
>
> 
>
> ​	
>
> 
>
> ​	
>
> ​	
>
> ​	
>
> ​	
>
>  ​	
>
> 





















## 记录4：IDEA - IntelliJ IDEA

> ​	**IDEA**是一款集成开发环境（IDE），是IntelliJ IDEA的简称。是业界公认最好的java开发工具    （但收费）
>
> ​	IDEA是**JetBrains**公司的产品
>
> ​	除了 支持**java**开发，还支持**HTML,CSS,MySQL，Python**等



> ​	**Eclipse**是另一款用于java开发的IDE（可扩展）
>
> ​	是**IBM**公司的产品
>
> ​	开放源代码（2001年贡献给开源社区），所以免费不要钱



**使用技巧和经验和快捷键：**

> 1.设置字体：
>
> ​	代码字体：	file -> settings ->Editor -> Font 
>
> ​	整体字体：	file -> settings ->Appearance&Behavior -> Appearance ->using custom font:设置字体大小
>
> 
>
> 2.颜色主题调整：
>
> ​	file -> settings ->Editor -> color scheme
>
> 
>
> 3.字符编码设置：
>
> ​	离开了dos其实用的都是UTF-8,所以这里要设置为utf-8，步骤为：
>
> ​	file -> settings ->Editor -> File Encodings 
>
> ​	 可以设置Global Encoding 和Project Encoding
>
> 
>
> 4.**快捷键**
>
> ​	设置快捷键的路径：
>
> ​			file -> settings -> Keymap
>
> ​	常用快捷键：
>
> ​			**Ctrl+D**	删除整行（自己设置的）
>
> ​			**Ctrl+shift+D**	复制当前行（也是自己设置的）
>
> ​			**Alt + /**	代码自动补全
>
> ​			**ctrl + /** 添加注释和取消注释
>
> ​			**ctrl + shift + /**  	对选中内容添加/取消注释
>
> ​			**ctrl + alt+ L** 	快速格式化
>
> ​			**shift + f10**	快速运行程序
>
> ​			**alt  + insert**	生成构造器等（注意华为笔记本把Fn关掉才可以，否则就点成了F12）
>
> ​			**ctrl + H**	查看一个类的继承关系（需要把光标放在类名上）
>
> ​			**ctrl + B / ctrl + 左键单击**	定位到方法（需要把光标放在方法上）
>
> ​			**new 变量类型.var + 回车**	自动分配变量名
>
> ​			**alt+enter**	将光标法停在自动导入库
>
> 5.模板Template：
>
> ​	将常用的代码模板设置为快捷键，比如打**main**跳出来主函数，打**fori**跳出来循环，打**sout**跳出来System.out,println(  ),打**St**出来String；
>
> ​	查看存在的模板
>
> ​	file -> settings -> Editor -> Live Template
>
> 
>
> 6.断点调试：
>
> ​	在断点调试中，是运行状态，是以对象的运行类型来执行的
>
> ​	快捷键:
>
> ​	F7 跳入方法
>
> ​	shift+F8 跳出方法
>
> ​	F8 逐行执行，不跳入
>
> ​	F9 跳到下一个断点



## 记录5 面向对象高级部分

### 类变量和类方法

1.关于静态变量（类变量）存放位置的不同说法：

​		jdk7、8之前存放在方法区

​		jdk8以后放在堆里



2.静态方法和非静态方法：

​	（1）非静态方法既可以直接访问（所属类的）静态数据成员 又可以访问非静态数据成员，而静态方法只能直接访问（所属类的）静态数据成员，若要访问所属类的非静态数据成员，需要先实例化所属类

​	（2）静态方法中，不能使用super和this关键字

​	（3）类变量、类方法、普通方法都是随着类的加载而加载的，类变量存在堆/方法区中，而类方法和普通方法都存放在方法区。

​	（4）类方法中无this参数，而普通方法中会有隐含的this参数。

[静态方法和非静态方法区别](https://zhuanlan.zhihu.com/p/258751142#:~:text=1 静态方法不能调用非静态的方法和变量.（ 非静态方法可以任意的调用静态方法%2F变量,） 2 不能使用this和super关键字（属于类级别，没有创建对象签不可用this%2Fsuper）)



### 代码块

1.静态代码块 & 普通代码块

>  静态初始化和普通初始化都可以有多个，也可以同时存在

>  首先说明**类的加载**的三种情况：

​				创建对象实例

​				创建子类对象实例（所有父类对象都会被加载）

​				直接调用类的静态成员

​		类应该是只会加载一次

>  		静态代码块在加载类的同时被隐式调用，因为类只会加载一次，所以静态代码块只会调用一次
>
> ​		普通代码块只会在创建对象实例的时候被调用（更准确地说是运行构造器进行初始化时里面里面有隐含的执行普通代码块的部分），但是因为对象实例可以创建多个，所以普通代码块可以被调用多次



>  创建一个对象的调用顺序（只考虑该对象所在类中的调用顺序）：

​		创建一个对象首先得加载这个类，所以要**先调用静态代码块和静态属性初始化**

​		然后才使用构造器，但是因为构造器的最前面其实隐含了super()和普通代码块/普通变量初始化，**所以第二步要再调用普通代码块和普通变量初始化**，**最后调用构造方法**



>  创建一个对象的调用顺序（同时考虑对象父类所在类中的调用顺序）：	

​		加载当前类之前，得先加载该类的父类，所以**①先进行父类的静态代码块和静态属性的初始化**，然后**②进行当前类的静态代码块和静态属性的初始化**

​		因为构造器最前面是super(),也就是父类的构造器函数，父类的构造器函数中也有父类的普通代码块和普通属性初始化的代码，所以**③进行父类普通代码块和普通属性的初始化**，然后执行**④父类的构造方法**，

​		super()结束之后，才到了当前类的**⑤普通代码块和普通属性的初始化**,最后是**⑥当前类的构造方法**。

​	（attention：从这里能体会到，普通代码块和属性的初始化并不是跟创建对象绑定的，而是与构造器绑定的，这里父类并没有创建对象，而只是调用了父类的构造器方法。）



> 静态代码块智能调用静态城院，普通代码块可以调用任意成员

​		



### 单例设计模式

> 概念

​	采用一定的方法，保证某个类只存在一个对象实例，且该类要提供一个取得其对象实例的方法getInstance（）

> 实现方法：**饿汉式**和**懒汉式**

​	**饿汉式：**

​	只能有一个对象化实例，就不能随便new对象（new对象实际上就是调用构造器...暂时可以这么理解）

​	那么就得让构造器从public变为private

​	不能让其他类new对象，那对象谁来new啊？当然是自己，所以类中需要提供一个对象属性，由本类保管，不能随便让其他类访问，所以用private修饰

​	那么其它类怎么才能得到由该类保管的对象呢，就需要该类提供一个public的getInstance方法，return该类的对象属性。其它类需要直接调用getInstance方法，所以getInstance为static静态方法。又因为静态方法只能访问静态变量，所以对象属性也需要为static。

​	采用饿汉式单例设计模式，实现一个GirlFriend类：

```java
class GirFriend{
    //类中实现一个对象实例
    private static GirFriend gf = new GirlFriend()；
    //私有化构造器
    private GirlFriend(){};
    //提供一个getInstance方法
    public static getInstance(){
        return gf;
    }
    
}
```

​	**懒汉式：**

​		使用单例涉及模式的类一般都是比较占用资源的类，所以不能随便进行实例化。但是饿汉式不管用没用到该类的对象，都会先在类中实例化一个对象，容易造成资源的浪费。所以有懒汉式的单例涉及模式。

​		懒汉式并不会在加载类后就实例化一个对象，而是在其它类调用getInstance方法时，才会进行实例化，代码较饿汉式只有一点改动，如下：

```java
class GirFriend{
    //类中先定义一个对象引用，但并不会进行实例化
    private static GirFriend gf;
    //私有化构造器
    private GirlFriend(){};
    //提供一个getInstance方法
    public static getInstance(){
        if(gf == null){
            gf = new GirFriend();
        }
        return gf;
    }
    
}
```

​			从getInstance中的判断逻辑可以看出，懒汉式只会在第一次调用getInstance方法时实例化一个对象，之后再调用就不会创建了。

​	

​	**两种方法比较**：

​	饿汉式不存在线程安全问题，懒汉式存在线程安全问题：如果同时有多个线程调用getInstance方法，且都在只是进行判断逻辑，那么三个线程都会以为还没有实例化对象，就会同时创建三个实例化对象。

​	

​	**java.lang.Runtime就是经典的单例模式**



### final

> 与修饰符的搭配顺序
>
> 

​	public static final ...



> 可以修饰  （ 类 ， 方法 ， 属性 ， 局部变量 ）



​	修饰类，表示类**不可以被继承**了，语法：final class 类名{ ...}

​	

​	修饰方法，表示方法**不可以被子类重写**，语法 [权限修饰符] final  返回类型  类名{...}



​	修饰属性，表示属性**不可被修改**，也就是**常量**，（属性其实就是定义在方法外的变量，所以对比下面局部常量，final修饰的属性也可以成为**全局常量**）

​	修饰局部变量（只定义在方法里的变量），表示局部变量**不可被修改**，也就是**局部常量**



> 注意事项



​	1.常量和局部常量在习惯上**都要大写**

​	

​	2.final修饰的属性，也就是常量，在**定义时**，必须赋初值，并且以后都不能再修改：

​			定义常量时/构造器中/代码块中



​	3.如果final修饰的属性是静态的（static在final前），则初始化的位置只能是：

​			定义常量时/静态代码块中

​		不能在构造器中，因为这时候的常量是属于类的，在加载类的时候就得赋初值！



​	4.一般来说，若一个类已经是final类了，就没必要再将类中的方法修饰称final方法了



​	5.final不能修饰构造器



​	6.比较神奇的一点：

​			直接调用final static修饰的属性，不会加载该类，节省了内存空间。

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221025184903574.png" alt="image-20221025184903574" style="zoom: 50%;" />

​		比如这段代码，只会输出10000，而不会输出静态代码块里的语句，说明该类没被加载。（底层编译器做的优化）

​		这种特性可以用于在类中存储一个常量，而不调用类的其它功能，比如java中的**Math.PI**和**Math.E**，可以直接用，而不会加载Math这个类。

​		

​	7.包装类（指Integer，Double，Float，Boolean，String类）都是final类



### abstract—抽象类和抽象方法

> abstract修饰类和方法（只能）

​	abstract修饰类，即为抽象类；

​	abstract修饰方法，即为抽象方法；



> 语法

​	[访问修饰符] abstract class 类名{...}

​	[访问修饰符] abstract 返回类型 方法名（参数列表）;    	没有{}！！也就是没有方法体



> 用途

​	有时父类的某个方法还没有想好，那就先不写（方法体{}），只需要在该类之前加个abstract，让它变成抽象方法；该抽象方法所在类就变成了抽象类，也得在类前加修饰符abstract。

​	抽象类的更多价值在于设计，设计者设计好后，让子类继承并实现抽象类。

​	在框架和设计模式使用较多，考官爱问。



> 抽象类和抽象方法的关系

​	抽象类中不一定要包含抽象方法，但是抽象方法一定要在抽象类中。

​	抽象类本质上还是一个类，所以里面可以包含类的任何成分，并不是里面只能放抽象方法/什么也没有。



> 使用细节&注意事项

​	1.抽象类不能被实例化

​	2.如果一个类继承了抽象类，要么：1.实现该抽象类的所有抽象方法（即使只加一个{}也算实现了）									

​													 要么：2.也声明为abstract类。

​	3.抽象方法不能用private、final、static来修饰：

​			不能用private、final：都会影响子类的重写

​			不能用static：两种说法	①static属于类，需要能被调用，没有方法体自然不能被调用	②static修饰的方法属于父类，不能被子类重写。



### 模板（设计）模式

​		可以直接看视频，看一遍就可以，语言不好总结（Video401）



### 接口



> 初步理解：（V403f老韩讲的很好）

​		在接口的世界中，有三种thing：

​			接口Interface：定义了一些必须要实现的功能/方法（制作一种接口）

​					<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221025212024770.png" alt="image-20221025212024770" style="zoom: 67%;" />

​			implement 接口的”被控制类“：实现了接口定义的功能/方法（根据接口规范制作自己的”设备“）

​					<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221025212058908.png" alt="image-20221025212058908" style="zoom:50%;" />

​			将实现接口方法的”被控制类“作为方法传入参数的”控制类“：该方法可以调用传入的被控制类实现的”接口规定的方法“

​					<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221025212331256.png" alt="image-20221025212331256" style="zoom:50%;" />

​					（相当于computer给自己安装了一个usb接口，可以说是非常形象了）

​		**跑起来看看（接口使用流程）：**

​					<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221025212654846.png" alt="image-20221025212654846" style="zoom: 50%;" />

​	结果：

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221025212723615.png" alt="image-20221025212723615" style="zoom:50%;" />



​		通俗点讲，接口最大的作用就是**“统一方法名”**

> 接口Interface使用细节：

​	1.**接口中的抽象方法**可以不用abstract修饰（一般情况下就是不用的。）

​	接口中的抽象方法就是要实现类去重写的，所以必须是public的，故接口方法默认了就是public

​	比如，要在接口中实现一个public abstract void hi();方法，可以直接写成void hi();



​	2.**接口中的属性**需要满足三个条件：能被所有实现类访问public/不能被修改final/属于接口static，所以接口中的属性默认的修饰符是**public static final**

​	比如：int i =1  相当于 public static final int i =1；

​	接口中属性的访问方式：**接口名.属性名**

​	实现了接口的类也可以访问属性： **类名.属性名**	/	**类的实例化的对象名.属性**

​	3.在jdk7之前（包括jdk7），**接口里的方法**只能有抽象方法

​	在jdk8之后（包括jdk8），接口内除了抽象方法，还可以有默认方法（default代替public修饰）和静态方法（public static）



​	4.因为接口实际上是一个抽象类，所以**接口也不可以被实例化！！**

​	

​	5.接口**不能继承其它类**，但是可以继承**多个**别的接口

​			语法： 	interface A extends B，C{...}

​			至于为什么要接口继承接口，见下面接口的多态继承代码。



​	6.**接口的修饰符**只能是public或者没有（默认）



> <实现类：class 类名 implements 接口名>  的使用细节：



​	1.一个普通类实现接口，就必须把接口中所有的类都实现；

​		但是抽象类若要实现接口，就不用。



​	2.实现接口方法的类也可以有自己的属性和方法。



​	3.一个类可以实现多个接口（对比一个类只能继承一个父类）

​			class 类名 implements 接口1，接口2 {...}



> 接口vs继承（视频409）

​	当子类继承了父类，就自动的拥有父类的 功能

​	如果子类需要扩展功能，可以通过实现接口的方式拓展

​	可以这样理解：实现接口	是对java单继承机制的一种补充（python可以实现多继承）

```java
	class LittleMonkey extends Monkey implements Fishable,Birdable{...}
```

​	继承的价值在于：解决代码的复用性和可维护性

​	接口的价值在于：设计好各种规范，让其它类去实现这些方法。

​	**“接口在一定程度上实现代码解耦”**（接口规范性配合动态绑定机制  实现解耦），先记住！！



### （接口的多态）

> 接口类型的变量，可以指向实现了接口的类的对象实例

​		代码示例如下：

​		形式上类似于类的向上转型。

​		可以把接口interface看作实现类的父类，有向上转型，自然有向下转型，这样才能让编译类型是接口的实现类对象访问该类特有的方法。（可参考视频410，16min处老韩便利接口数组的操作）

```java
public class InterfacePolyParameter {
    public static void main(String[] args) {
        
        //接口类型的变量，可以指向实现了接口的类的对象实例
        IF if01 = new Monster();
        if01 = new Car();
        
        //
        AAA a = new BBB();
        a = new CCC();
    }
}


interface IF {}
class Monster implements IF{}
class Car implements IF{
```

​	

>  多态参数

​	在computer这种利用usb接口“控制“手机和相机的类中，控制方法（相当于给计算机安装的接口）work中传入的本应是一个”接口本身“。

​		<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221026232438256.png" alt="image-20221026232438256" style="zoom:50%;" />

​	但是在实际使用时我们传入的都是实现了接口功能f的实现类，如phone和camera

​		<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221026232948296.png" alt="image-20221026232948296" style="zoom:50%;" />

​	以上这种”行为“便是接口作为”多态参数“传入。

​	

> 多态数组

```java
public class InterfacePolyArr {
    public static void main(String[] args) {
        //多态数组 -> 接口类型数组
        Usb[] usbs = new Usb[2];
        usbs[0] = new Phone_();
        usbs[1] = new Camera_();
    }
}
interface Usb{}
class Phone_ implements Usb {}
class Camera_ implements Usb {}
```



> 多态传递

​		上面提到过，接口是可以继承接口的。

​		接口是其实现类的父类，那么接口的父接口便是该实现类的祖宗类：

​			1.也得实现祖宗类的抽象方法

​			2.祖宗类（父接口）的变量，也可以指向该实现类的对象。

```java
public class InterfacePolyPass {
    public static void main(String[] args) {
        
    IG ig = new Teacher();
    IH ih = new Teacher();
    }
}

//接口的父接口
interface IH {
    void hi();
}
//接口
interface IG extends IH{ }
//接口的实现类
class Teacher implements IG {
    @Override
    public void hi() {
    }
}
```



###  内部类

​	内容太多，建议直接看老韩的pdf







## 记录6 枚举和注释



### 文件头file header 设置

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221028154000848.png" alt="image-20221028154000848" style="zoom:50%;" />

​	图中绿色部分，叫做文件头，用来说明”代码的版权“之类的，project设置文件头之后，在生成的每一个.java文件中都会有一个文件头

​	设置过程：

​	File --> Settings --> Editor --> File and Code Templates -->找到Includes --> File Header 

​	然后自己编辑就好了



### 枚举类

> 枚举类的概念

​	枚举类就是把具体的对象一个一个列举出来的类



> 什么样的类需要设置成枚举类

​	比如现在定义一个季节类Season,因为季节只有四种，所以Season应该**只有（有限个）四个对象**；

​	而且这四个对象的一些特性是不允许修改的， 比如每个季节的特点desc,所以**枚举对象应该是只读的**。



> 枚举类的两种实现方式

​	1） 自定义实现枚举

​	2）使用enum关键字实现枚举



> 自定义实现枚举	（以Season类举例）



​		**枚举对象有限个**，要求其他类不能new，故构造器需要私有化private



​		故应**由类本身提供对象给外界**（public），所以应该在类中创建静态（static）Season对象。进一步优化，可以再加一个final修饰符，组成final static,这样会有底层优化，只加载对象不加载类。这时对象成了一个常量，所以对象名需要大写（常量的命名规范I）

​		public final staitc Season SPRING = new Season("春天"，”温暖“)；



​		**对象只读**，所以应该将Season类属性xxx对应的setXxx删掉，只保留getXxx

```java
class Season {//类
    private String name;//季节名称
    private String desc;//描述
    //定义了四个对象,
    public static final Season SPRING = new Season("春天", "温暖");
    public static final Season WINTER = new Season("冬天", "寒冷");
    public static final Season AUTUMN = new Season("秋天", "凉爽");
    public static final Season SUMMER = new Season("夏天", "炎热");
    //将构造器私有化
    private Season(String name, String desc) {
    this.name = name;
    this.desc = desc;
    }
    //去掉 setXxx 方法, 只保留getXxx方法
    public String getName() {
    return name;
    }
    public String getDesc() {
    return desc;
    }
 
}
```



> enum关键字实现枚举

	- 与自定义只有两个地方不同：

​	1）把class关键字换成enum关键字

​	2）定义对象的语法可以使用**”语法糖“**（语法糖简单理解：对语言功能没有影响，程序员更方便），具体变化体现在：

​				①public static final Season SPRING = new Season("春天", "温暖");	替换为	SPRING("春天","温暖")；

​				②定义对象的语言要放在类的最开始，其它的都靠后。

​				③定义的多个对象之间要用 *”，“* 隔开，而不是用分号隔开。

​	除了1）2）3）三个地方，其它都与自定义相同

​		

```java
enum Season02 {//类
    //定义对象，放在类的最开始,多个类用英文逗号隔开
    SPRING("春天", "温暖"),WINTER("冬天", "寒冷"),AUTUMN("秋天", "凉爽"),SUMMER("夏天", "炎热");
    //属性不能放在最开始了
    private String name;//季节名称
    private String desc;//描述
    
    //剩下的都一样
    //将构造器私有化
    private Season(String name, String desc) {
    this.name = name;
    this.desc = desc;
    }
    //去掉 setXxx 方法, 只保留getXxx方法
    public String getName() {
    return name;
    }
    public String getDesc() {
    return desc;
    }
 
}
```

	- 其它需要知道的：

​	1）使用enum关键字的枚举类，默认会继承**java.lang.Enum类**（因为java的单继承机制，所以enum定义的枚举类不可以再继承其他类，但可以实现接口），而且该枚举类是一个final修饰的不可继承类。（使用javap可以查看enum构造的Season2类的信息）

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221028164952803.png" alt="image-20221028164952803" style="zoom: 50%;" />

​	2）当SPRING("春天","温暖")不传入参数，也就是调用无参构造器时，小括号可以省略，写成SPRING;



### （java.lang.Enum类）

> **Enum类中的常用方法**
>
> ​	
>
> 以season02类为例，说明Enum类中的方法
>
> main方法中：
>
> Season02 autumn = Season02.AUTUMN;
>
> System.out.println(autumn.**方法名()**)
>
> System.out.println(Season02.**方法名()**)



1) **name()**

​		该方法给枚举对象使用	**autumn.name()**

​		得到枚举类的对象名称，也就是AUTUMN



​	2.**ordinal()**		翻译为序数/顺序的，依次的	[辨析]ordinary	普通的

​		该方法给枚举对象使用	**autumn.ordinal()**

​		返回该枚举对象的（生成）次序，编号从0开始，AUTUMN第三个生成，所以返回2



​	3.**values()** 

​		该方法属于枚举类，给枚举类使用	**Season02.values()**

​		并不包含在Enum的方法中，而是用enum关键字定义枚举类时，编译器给该枚举类加上的一个方法，可以参考上面的DOS截图

​		返回一个数组，里面装有该枚举类的所有对象,也就是  *{SPRING,WINTER,AUTUMN,SUMMER}*	

​		（注意：java数组使用{}包起来的，而不是像c++是用[]包起来的。python中[]包起来的是列表）



​	4.**toString()**

​	该方法给枚举对象使用	**autumn.toString()**

​	Enum类重写Object类的方法，返回该枚举对象的名字，也就是name()，这里返回AUTUMN



​	5.**valueOf(str)**

​	该方法给枚举类使用，传入字符串str

​	如果str是枚举类Season的一个对象的名字，那么返回该对象

​	否则(假如字符串为”HSP“)，报错   *IllegalArgumentException Create breakpoint: <font color="red">No enum constant com.hspedu.enum_.Season2.HSP</font>*

```java
String str = "AUTUMN";
Season02 autumn02 = Season02.valueOf(str);
```

​	

​	6.**compareTo()**

​	计算两个枚举类对象的序号的差，返回一个int值

```java
Season02 autumn = Season02.AUTUMN;
Season02 summer = Season02.SUMMER;

sout(autumn.compareTo(summer))  //输出-1，也就是AUTUMN的序号2-SUMMER的序号3

```



### 注解Annotation

> 注解  理解

​	1.也被称为**元数据**，用于修饰和解释	包、类、方法、属性、构造器、局部变量等数据信息

​	2.与注释比较：

​			二者都不影响程序逻辑，但是注解annotation可以被**编译或者运行**，<font color="red">相当于嵌入代码中的补充信息（不太理解）</font>

​	3.在javaSE中使用的比较简单，但在javaEE中注解占据了更重要的角色（用来配置应用程序的任何切面/代替javaEE旧版中所遗留的繁冗代码和XML配置）



> 分类

​	三个基本的Annotation：

​		@Override

​		@Deprecated

​		@SuppressWarnings

> @Override介绍

​	1.修饰某个**方法**，表示重写父类方法

​	2.没有@Override也可以，写了相当于加一份保险：

​		因为如果有@Override却没有构成重写，也就是父类不存在可以被重写的方法，编译器就会报错。

​	3.@Override的底层代码：

```java
//说明只能修饰方法，@Target是修饰注解的注解，也就是元注解
@Target(ElementType.METHOD)
//
@Retention(RetentionPolicy.SOURCE)

public @interface Override {
}
//@interface和interface关键字不同，后者表示接口类，前者表示注解类
```



> @Deprecated介绍

​	1.用于表示某个程序元素（包、类、方法、属性、字段、参数等）已经过时，但不代表不能用（只是会在源代码的数据元素上加上中划线，用于辨认）

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031170501545.png" alt="image-20221031170501545" style="zoom:50%;" />

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031170516542.png" alt="image-20221031170516542" style="zoom: 50%;" />

​	2.@Deprecated底层代码：

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
//说明可以修饰的数据元素有：构造器、字段FIELD、局部变量、方法、包、参数、类型
@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE})
//{}内什么都没有，代表不需要传入参数，直接在需要注解的数据元素前写一个@Deprecated就可以了

public @interface Deprecated {
}
```

​	3.为什么会有@Deprecated这一个注解/用途：

​		版本升级过度使用：新版本中仍然包括旧版本的数据元素，但是需要用户知道这个数据元素已经被新版本重新实现了，用户就可以去了解并使用新的实现方法



> @SuppressWarnings介绍

​	

​	1.用于**抑制编译器警告**，下面介绍什么是编译器警告：

​		<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031173616592.png" alt="image-20221031173616592" style="zoom: 50%;" />



​	右上角的黄色叹号以及右侧下拉条上的黄线就是编译器警告，并不会影响程序的运行，但是会”逼死强迫症“



2.用法：

​	可以用于类、方法**之前**，用于抑制对应的类、方法内的警告

​	也可以用于具体语句之前，用于精准抑制对该语句的警告



​	@SuppressWarnings({"属性1"，”属性2“，... ,"属性n"})

​		解释”属性“：警告类型有很多种，比如下面这种unchecked警告、rawtype警告和neverused警告

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031174303178.png" alt="image-20221031174303178" style="zoom: 50%;" />

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031174505878.png" alt="image-20221031174505878" style="zoom: 50%;" />

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031174553176.png" alt="image-20221031174553176" style="zoom: 67%;" />

​	属性就代表了需要屏蔽的警告类型，包括以下这么多：

```java
// all，抑制所有警告
// boxing，抑制与封装/拆装作业相关的警告
// //cast，抑制与强制转型作业相关的警告
// //dep-ann，抑制与淘汰注释相关的警告
// //deprecation，抑制与淘汰的相关警告
// //fallthrough，抑制与 switch 陈述式中遗漏 break 相关的警告
// //finally，抑制与未传回 finally 区块相关的警告
// //hiding，抑制与隐藏变数的区域变数相关的警告
// //incomplete-switch，抑制与 switch 陈述式(enum case)中遗漏项目相关的警告
// //javadoc，抑制与 javadoc 相关的警告
// //nls，抑制与非 nls 字串文字相关的警告
// //null，抑制与空值分析相关的警告
// //rawtypes，抑制与使用 raw 类型相关的警告
// //resource，抑制与使用 Closeable 类型的资源相关的警告
// //restriction，抑制与使用不建议或禁止参照相关的警告
// //serial，抑制与可序列化的类别遗漏 serialVersionUID 栏位相关的警告
// //static-access，抑制与静态存取不正确相关的警告
// //static-method，抑制与可能宣告为 static 的方法相关的警告
// //super，抑制与置换方法相关但不含 super 呼叫的警告
// //synthetic-access，抑制与内部类别的存取未最佳化相关的警告
// //sync-override，抑制因为置换同步方法而遗漏同步化的警告
// //unchecked，抑制与未检查的作业相关的警告
// //unqualified-field-access，抑制与栏位存取不合格相关的警告
// //unused，抑制与未用的程式码及停用的程式码相关的警
```

​	当然不用全都记住，一般情况下就用个all就完事了。

​	

​	3.源代码：

```java
//说明作用的对象，但是一般只有类、方法、语句
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)

//{}内有“String[] value();”,意思是要传入属性
//对比@Deprecated可以看出二者用法上的区别
public @interface SuppressWarnings {
	String[] value();
}
```



> 元注解

​		上面三种常用注解中也有注解，这些**修饰注解的注解**就叫做元注解。

​		有四种：@Target	@Retention	@Documented	@Inherited

​		（学习目的：知道有这么个东西存在，阅读源代码的时候知道是干嘛的就好）



​		@Target

​			用于说明该元注解修饰的注解的作用对象



​		@Retention

​			用于指定它修饰的注解可以保留到哪一个阶段，通过RetentionPolicy这一成员变量指定：

​				1）RetentionPolicy.SOURCE：编译器使用后就丢弃@Retention修饰的注释，不会保留到.class中（只在.java中出现）

​				2）RetentionPolicy.CLASS：编译器使用后不会丢弃，可以保留到.class中，但是当JVM运行该class文件时不会保留注释。

​				3）RetentionPolicy.RUNTIME:一直保留注释，JVM运行.class文件时也不会丢弃，<font color="red">程序可以 通过反射获取该注解</font>



​		@Documented

​			被@Documented修饰的注解，将被javadoc工具提取成文档。下面以Deprecated举例

​			这是jdk文档里String类中的一个方法，可以看到已过期字眼

​			点入该方法页面也可以看到保留的@Deprecated注解

![image-20221031181048414](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031181048414.png)

![image-20221031181112559](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031181112559.png)

​		

​		@Inherited

​			被@Inherited修饰的注解Annotation 修饰的类，将会把该注解Annotation继承给它的子类。





## 记录7 异常Exception



### 异常初认识

​	看下面这段代码：

```java
public class Exception01 {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = 0;
		int res = num1/num2;
        System.out.println("程序继续执行...");
    }
}
```

​		运行后会出现以下报错：![image-20221101150221598](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101150221598.png)

​		报错分析：

​		1）Exception in thread "main"表示出错的线程叫做main，这个在没使用多线程之前应该都是一样的。

​		2）java.lang.ArithmeticException 表示出错类型是Arithmetic，这一长串是Arithmetic的继承路径。

​		3）Create breakpoint： / zero 是指出错的具体原因，除以0了。

​		4）at com.hspedu.exception_.Exception01.main(Exception01.java:15)表示具体出错位置，括号外定位到具体方法main,括号内定位到具体java文件的哪一行。

​		而且发现，sout并没有输出，也就是说遇到Arithmetic报错后，程序就没有继续执行了。

​		但是这样其实并不好，以为在一些庞大的工程中这些错误都不是致命错误，如果因为这些错误导致程序停止运行是很不好的（比如相除的两个数是需要用户输出的，难道就因为用户输入了0没法除就导致整个程序瘫痪？不可能的），所以java设计者提供了**异常处理机制**来”忽略“这种错误。

​		如果程序员觉得一段程序可能出现运行时异常（后面会讲到为什么是运行时异常），就需要提前用异常处理机制对这段代码进行处理，防止其导致程序中断。

```java
public class Exception01 {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = scanner.nextInt();
        //try-catch异常处理机制，也叫做异常捕获机制
		try{
            int res = num1/num2;
        }catch(Exception e){
            e.printStackTrace();
            //System.out.println(e.getMessage());//输出异常信息
        }
        
        System.out.println("程序继续执行...");
    }
}
```

​		快捷方式，将int 热水 = num1/num2选中，ctrl+alt+t，选择6.try/catch,就会直接把这段代码包在try-catch里。

![image-20221101152026155](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101152026155.png)

​		虽然还是跟刚才一样报错，但是程序确继续执行了，说明：

​			1）try-catch机制能防止因运行异常造成的中断

​			2）红色报错部分是Exception类printStackTrace方法（由具体的ArithmeticException类又重写）的输出。

​		如果把e.printStackTrace()换成System.out.println(e.getMessage())，则会得到下面这样的输出。![image-20221101152520789](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101152520789.png)

​		说明getMessage()方法返回的是**具体错误原因的字符串**



​		由以上所有得到的启发：

​		1）具体的错误类型ArithmeticException这些也是类，它们继承了Exception类，实现了（重写了）getMessage()和printStackTrace（）这些方法。

​		2）try-catch中catch的中可以使用这些不同的方法来输出不同的提示内容，（在原理上）甚至可以不提示，直接忽略这种错误，也就是catch里什么都不写。也就是说，控制权在程序员。



### 异常体系图

> IDEA中的类图



<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031215528692.png" alt="image-20221031215528692" style="zoom:67%;" />

​		

​	如上便是java的类图：表示类之间继承关系的图

​	1）如何调出？

​			ctrl+b 进入 Throwable.java文件

​			在空白处单击右键 --> 点击Diagram --> 选择show diagram

​			会出现以下图片，因为该文件中只有Throwable类，所以初始只会显示Throwable类，绿色I标代表它实现了Serializable接口

![image-20221101143340324](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101143340324.png)

​			右键点击Throwable框，可以看到有show Implementation选项，点击它，就会跳出如下窗口。

![image-20221101143659758](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101143659758.png)

​			Implementation of  Throwable，这些都是Throwable的子类或者后代类，点击对应的类就会自动跳出该类的方框，自动显示该方框与原所选框内类（Throwable类）的关系。

​			这里就不调出所有的子类了，太多了，图片装不下，就挑一些常见的部分。

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221031215528692.png" alt="image-20221031215528692" style="zoom:67%;" />

​		可以看到：

​			1）异常事件可以分为两大类：Error和Exception。

​					Error，错误，表示虚拟机无法解决的严重问题，像JVM系统内部错误，资源耗尽等严重情况，具体的如：StackOverflowError、OutOfMemory错误。

​					Exception也就是没那么严重的错误，可以通过针对性的代码进行处理，又分为两大类：**运行时异常RuntimeError**和**编译时异常**

​							**编译时异常**是必须要处理的异常（IDEA里红色的部分中，大部分都是编译时异常，还有一些不是异常的报错，比如语法错误，！！！注意逻辑错误并不会报错！！！），否则没法通过编译。**运行时异常**一般是指编程时出现的逻辑错误，这类异常很普遍，如上面的Arithmetic错误，因为通过编译的程序其实就可以运行了，所以RuntimeError不是必须要处理的（这里的处理指的是中断程序并报错）。事实上，对于大型工程一般是需要“忽略”这些错误的，不能因为这些错误中断了程序，否则会影响运行效率。



### 五大常见运行时异常

​		从上面类的体系图可以看出，这五类都是RuntimeException的子类，继承关系为：

​		java.lang.Object → java.lang.Throwable →  java.lang.Exception → java.lang.RuntimeException → 具体的每一类运行时异常

​		这五类异常包括：

​		1）NullPointerException空指针异常

```java
public class NullPointerException_ {
    public static void main(String[] args) {
        String name = null;
        System.out.println(name.length());
    }
}
```

​			在需要用到对象的地方却只有null时，就会抱这种错误



​		2）ArithmeticException数字运算异常

```java
		除以0这种数字运算错误
```



​		3）ArrayIndexOutOfBoundsException数组下标越界异常

```
		就数组下标越界
```



​		4）ClassCastException类型转换异常

```java
public class ClassCastException_ {
    public static void main(String[] args) {
        A b = new B(); //向上转型
        B b2 = (B)b;//向下转型，这里是 OK
        C c2 = (C)b;//这里抛出 ClassCastException
    }
}
class A {}
class B extends A {}
class C extends A
```

​			向下转型时，转向的不是运行类型对应的编译类型



​		5）NumberFormatException数字格式不正确异常

```java
public class NumberFormatException_ {
    public static void main(String[] args) {
        String name = "韩顺平教育";
        //将 String 转成 int
        int num = Integer.parseInt(name);
        System.out.println(num);//1234
    }
}
```

​		当试图把字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。



### 编译异常

​	一般发生在网络，数据库或者文件操作的时候，常见有以下种类：

![image-20221101160023093](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101160023093.png)



### 异常处理

​	可分为**try-catch-finally**和**throws**异常处理机制

​	**try-catch-finally:**程序员在try的代码中捕获发生的异常，自行处理

​		1）如果没有发生异常，catch就不会执行，finally不管有没有异常都一定会执行，通常将释放资源的代码放在finally（有finally的话，肯定是在try-catch后执行finally，并且在后面的代码之前执行finally）

​		2）try-catch-finally能让程序继续执行的核心在catch,try-finall也可以直接用，但是这样在执行完finally后就不会继续往后执行了。try-catch也可以直接用

```java
try{
    ...
}catch(Exception e){
    ...
}finally{
    ...
}

//后面的代码
```

​	**throws**将发生的异常抛给上一级调用者（方法）来处理，最顶级的调用者就是JVM。![image-20221101180222173](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101180222173.png)

​	在除了JVM的任一级的调用者之间可以实现一个try-catch-finally，当异常反向传回该方法时就能被处理，程序继续执行。

​	但是如果这些调用者都不实现，最终到了JVM，JVM会**输出异常（Exception类printStackTrace方法）**，并且**退出程序**，也就是出现异常时默认的处理方式！！！

​	注意！main方法内如果没有出现try-catch-finally。默认就会在方法名之后加一个throws Exception，如下图（默认甩锅）![	](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101180843142.png)

​	但是其他要甩锅的方法必须显式声明throws（很不准确，后面讲throws细节的时候还会再讲！！）

> try-catch-finally使用细节：

​	 1）try里面可能有多条语句，但是在只有一个catch的情况下，出错语句后面的语句就不会执行了。

​	2）因为1），所以如果在try里有多个异常，那么只能处理第一个，后面的异常语句不会被执行。这时候就可以用多个try了：

​			前面讲过，try-catch-finally之所以能让程序继续执行，是因为catch的存在，实际上，一个catch就表示处理一个异常之后可以跳出try-catch-finally，如果有多个catch，就相当于有了处理多个异常的机会，具体过程理解如下：

​			①每一个catch的形参都会有一个异常类型，须遵守子类型在前，父类型在后的规则（因为异常出现会先匹配前面的 catch，把父类型留到最后包容性更强）

​			②在处理完一个异常之后，机会数都会减一，用过的catch下次就匹配不到了。catch次数过多也可以保证执行完try里的代码，但如果catch太少，机会数用完了，try里的代码就要提前结束了。

```java
//多个catch的示例代码
//在hsp的pdf内的第552页
```

​	3）finally一定要被执行，特别是碰到多个return的时候。![image-20221101190528261](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101190528261.png)

​	这种情况return 4，而不是3，说明finally一定要执行

​	![image-20221101190629034](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101190629034.png)

​			return4而不是3说明return ++i不是没执行，而是先执行了++i，然后再执行finally，如果finally中有return就执行finally的return，如果没有就返回来执行return。

![image-20221101190921787](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221101190921787.png)

​		这里先输出i=4，再输出3，说明finally中对常量的改变不会影响到catch中的常量，catch中会先把i存给temp。







> throws的使用技巧

​	1.当某方法不确定如何处理某种异常时，可以将它抛给调用它的方法。



​	2.throws后面的异常类型是可能产生的异常类型，也可以是该异常类型的父类。其实直接写一个Exception就可以了，因为它是所有编译异常和运行时异常的父类。



​	3.throws后面可以跟**多个异常类型**，用逗号隔开即可（感觉没有直接跟一个Exception好用）。



​	4.关于方法是否有默认throws：

​			**不管是main方法还是非main方法**，默认throws RuntimeException，f也可以显示声明要抛出的运行时异常；但是不会默认throws编译时异常。也就是说，如果某个方法调用的方法抛出了运行时异常，该方法可以不做任何处理，默认抛上去，如果该方法调用的方法抛出了编译时异常，那么该方法就必须做出处理（要么显示throws编译时异常/父类Exception，要么在方法里用try-catch-finallly）。



​	5.如果子类重写了父类的方法，而且这个方法有抛出，那么子类中重写的方法的抛出的异常的类型必须与父类异常类型相同或者是父类方法异常类型的子类。（这与子类方法不能缩小父类方法的访问权限的直觉是相反的）



### 自定义异常

​		

> 应用场景

​	当程序中出现的某种错误没有在Throwable的子类中，这个时候就可以自己设计异常类，用于描述该错误信息。



> 自定义的步骤

​	1.定义类，类名自己取（xxxException）,extends Exception/RuntimeException

​		如果继承Exception，属于编译异常

​		如果继承RuntimeException，属于运行时异常

​		大部分情况下，继承RuntimeException，因为运行时异常可以自动甩给上级调用函数，而编译异常要求调用该函数的上级函数也得显示声明throws或者try-catch-finally处理。

​		2.**在可能出现该异常的地方throw一个异常对象：**

​		系统自带的那些异常类型会自己”出现“，但是自定义的可不会自己出现，需要借助一个throw把异常对象抛给函数，函数再通过throws抛给上游调用函数。

​		所以可以理解为throw把异常对象抛给其所在的方法，throws把该方法中出现的异常抛给上级方法。（所以方法之间传递的其实也是异常对象）

​		看代码：

```java
public class CustomException {
    
    //throws AgeException可以没有，因为默认抛出RuntimeException是它的父类
  
    public static void main(String[] args) /*throws AgeException*/ {
        int age = 180; 
        //要求范围在 18 – 120 之间，否则抛出一个自定义异常
        if(!(age >= 18 && age <= 120)) {
            //这里我们可以通过构造器，设置信息
            throw new AgeException("年龄需要在 18~120 之间");
        }
        System.out.println("你的年龄范围正确.");
        }
}

class AgeException extends RuntimeException {
    public AgeException(String message) {//构造器
        super(message);
    }
}
```

​		3.关于传入的message：

​				传入的message其实就是getMessage()函数获得的内容（/by zero），也就printStackTrace()输出第一行最后的内容，在Exception类中，message是一个属性，在构造一个对象时必须传入。

​				系统自带的异常类型会自动构造一个异常类对象给方法，所以会根据情况自动传入一个message，比如/ by zero。而自定义的异常类型必须在throw的时候传入一个message，比如上例中的”年龄需要在18~120之间“。





> throw & throws辨析：

​	

​	其实上面已经差不多讲清楚了，这里补充几点然后总结一下。

|        | 位置       | 后面跟的东西 |
| ------ | ---------- | ------------ |
| throws | 方法声明处 | 异常类型     |
| throw  | 方法体中   | 异常对象     |





## 记录七 java常用类



### 包装类



> 什么是包装类？

​		Integer就是int的包装类

​		java有八种基本数据类型，对应八种包装类，如图：![image-20221102192101116](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221102192101116.png)

​		说明：

​		1）名字方面：除了Character和Integer，其它的都是首字母大写

​		2）黄色底的几个类都是Number的子类，其它两个是独立的类（Object的直接子类）。继承关系图对比如下：

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221102192647537.png" alt="image-20221102192647537" style="zoom:50%;" />

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221102192720405.png" alt="image-20221102192720405" style="zoom:67%;" />



> 装箱和拆箱

​		装箱：基本数据类型 --> 包装类

​		拆箱：包装类 --> 基本数据类型

​		

​		jdk5之前是手动拆箱和装箱

​		jdk5之后，就可以自动拆箱和装箱了

​		

​		手动和自动的对比见P567



>   关于包装类中的方法和字段：

​		不用全记下来，用到了就去查文档！！

​		但是可以看下熟悉，大概知道有哪几个功能，然后才能想到查。





> Integer的创建：

​		看下面一段代码，输出什么？

```java
public static void main(String[] args) {
    Integer i = new Integer(1);
    Integer j = new Integer(1);
    System.out.println(i == j); //False
    
    Integer m = 1; 
    Integer n = 1;
    System.out.println(m == n); //True
    
    Integer x = 128;
    Integer y = 128;
    System.out.println(x == y);//False
}
```

​		第一个false很明显因为不是同一个对象

​		但为什么第二个和第三个输出的结果反倒不一样呢？这得先搞清楚两种创建方法的区别了：

​		new Integer（...）是手动包装，肯定返回一个新对象；第二三种情况是自动包装，自动包装底层代码是valueOf代码，如下：![image-20221102203404327](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221102203404327.png)

​		IntegerCache是Integer类的一个静态成员内部类，其内有静态字段low，high和静态Integer数组cache，low为-128，high为127，cache数组有256个Integer对象，如果valueOf要创建的Integer数在-128和127之间，就直接返回cache中存的对象，不会执行下面的new Integer（）。

​		所以第二种情况下两个1返回的都是cache中存的同一个对象，第三种情况是new了两个新对象，==判断引用数据类型时只判断地址，所以。。。



> 需要注意的点:

​		只要==两侧有基本数据类型，判断的就是值是否相等。

```java
Integer i1 = 127;
int i2 = 127
System.out.println(i1 == i2)	//结果为True
```























### String

​	1）String类体系图

![image-20221103134408534](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221103134408534.png)

​	实现了三个接口：

​		Serializable接口，说明String类对象可以串行化，从而可以在网络中传递。

​		Comparable接口，说明String对象可以比较，至于怎么比较就看具体实现了。

​		CharSequence接口暂时不知道功能是啥。



​	2）有很多构造器，很多很多，熟悉常用的即可。

![image-20221103134258308](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221103134258308.png)

​	

​	3）String是final类，不能被其它类继承

​	4）String中的每一个字符都是使用**Unicode字符编码**，一个字符占两个字节（java中的char就是占两个字节）。字符存放在String类中的属性**private final char value[]**中，也就是value[]不可直接访问。

​		  value[]用final修饰，表示不可修改，不过不是里面的字符不可以修改，而是value数组的地址不可修改。



​	5）两种String创建方式的区别：

​		区别见P576

​		可能会困惑：常量池是什么？

​			就是方法区中放常量的地方。

```java
String s1 = "abc";
String s2 = new String("abc");
```

​		第一种创建方式返回一个来自常量池（中的String池）的字符串对象（**准确些叫字面量/直接量**，关于直接量的描述再java语法笔记），其value指向的是常量池中的字符数组char[]

​		第二种方式先在堆中创建一个String类的对象，再让其中的value属性指向常量池中的字面量字符串value指向的char[]，并不是指向常量池中的字符串字面量（也是字符串对象）；如果常量池中没有实现创建这么一个对象，那么会先创建常量池中的字面量对象，再创建堆中的。

​		**但是注意**，只有new String("abc")这种才会在池中也创建对象，因为“abc”这种表示方法其实就包含了创建一个字面量对象，然后将其引用给到变量。如果是new String()传入的是一个字符数组char[]，因为没有 “abc” 了，所以池中就不会创建一个字面量对象，而是直接在堆中创建一个String对象，它的value直接指向传入的char[]。

​		所以s1是指向常量池的，s2是指向堆的。所以下面这段代码也就可解释了。

```java
s2.equals(s1)  //True
s1.equals(s2)	//也可以，也是true（有些搞不懂）
s1 == s2	//False
```

​		<font color='red'>（有些搞不懂为什么常量池中的s1也有equals方法。。。）</font>

​		**（**解释：String池中的虽然是字面量，但其实它们也是String类的实例化对象，（至于new的堆中的对象的value指向，应该是指向了池中对应对象的value指向的char[]，而不是直接指向池中对象）

​			为什么要设置一个String常量池呢？虽然String并不是一个基本数据类型，但是它的使用频率同样高，频繁的重新分配String对象会耗费高昂的时间与空间代价，会极大影响程序性能。

​			所以可以看到java在实例化String常量时进行了一些优化，如上所述。为了配合使用，还专门为String设置了String字面量，这是其它的引用数据类型所没有的**）**

​		还有一个intern（）方法要注意，它返回new出来的String对象的常量池中的字符串对应的地址。

```java
String s1 = "abc";
String s2 = new String("abc");

System.out.println(s1 == s2.intern()); //True
System.out.println(s2 == s2.intern()); //False
```

​	上面的s2原来指向堆，intern()返回一个指向常量池的指针，但是s2本身还是指向堆，也就是说intern()操作**不是原地操作。**

​	但是，intern()返回的不一定是指向常量池的指针，该方法会先在常量池中寻找与s2的字符串“值”相同的字面量对象，如果找到了，该方法就返回指向该字面量的指针；如果找不到，就会在常量池中加入这么一个字面量❌（准确的说，并不是加入一个字面量，只是在常量池中加入了堆中对象的引用），返回的依然是常量池中的内容，即堆中s2的指针。看完下面例子就理解了：

```java
String a = "hello";
String b = "abc";
String c = a + b; //创建了四个对象：三个string,一个StringBuilder，如果不懂可以看6）
System.out.println(c == c.intern());

//输出 true
//原因: 用new String(char[])的方法创建String对象只会在堆中，常量池中并没有。调用intern()的时候，在池中找不到，所以复制了堆中对象的引用在池中，指向的还是c
```

> `intern()`方法在JDK1.6以后(不包括1.6)随着字符串常量池移到了堆空间，**整个实现也发生了变化，**主要体现在当字符串常量池中没有指定的字符串时，**JDK1.6会单独在字符串常量池创建一个对象**，而在JDK1.6以后(1.7 开始)，直接将堆内存的对象引用放入到了字符串常量池中。

更多例子：

```java
String a = "lizhi";
String b = "li";
String c = b + "zhi";
// 结果为false
System.out.println(a == c);

String a = "lizhi";
final String b = "li";
String c = b + "zhi";
// 结果为true
System.out.println(a == c);

原因：
//第一个：在编译期对象b是符号引用，无法确定，所以对象c也没法在编译期进行合并，只能运行时在堆中创建li对象然后通过append拼接zhi。
//第二个：对象b是一个常量，在编译期会被解析成常量值的一个本地拷贝存储到常量池中，这在编译期是可以确定
```



​	6）String之间的 “**+**”:

​	问：以下几种情况分别创建几个对象啊

```java
//创建一个对象（而不是三个）
String s1 = "hello" + "abc";

//创建两个对象
String s2 = new String("hello" + "abc");

//创建四个对象（而不是三个）
String a = "hello";
String b = "abc";
String c = a + b;
```

​	解答：

​	第一种情况：编译器会先把hello和abc合成helloabc再在常量池中创建

​	第二种情况：也是先合并，然后在常量池和堆中分别创建一个对象

​	第三种情况：先在常量池创建两个String对象，然后是将两个已经创建好的String对象相加，这时候编译器就不能直接加了，需要借助StringBuilder，步骤为：

​			先创建一个StringBuilder对象：**StringBuilder sb =new StringBuilder();**

​			StringBuilder中有value属性，一开始是空的，需要用append方法填充。

​			然后分别将a和b的值填进去：

​			**sb.append(a);		sb.append(b);**

​			最后用value创建一个String对象返回给c指针（包在toString里）

​			**String c = sb.toString();**

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230623181049842.png" alt="image-20230623181049842" style="zoom:50%;" />

​			new String("abc")既会创建堆中的对象，又会创建常量池中的对象！（因为需要它的value指向常量池中的对象value指向的char[]）

​			但是new String(char[])只会创建堆中的对象！！！！

​			在常量池中创建字面量对象有两种情况：
​				1.通过字面量创建String对象： String a = "makabaka"
​				2.调用intern()方法，如果常量池中没有，就会创建。 ❌ 实验过了，并没有（可能只对char创建的不管用？不懂）





> String类常用方法

​		equals(区分大小写)、equalsIgnoreCase(忽略大小写)、length（中文字符也只是算一个）、indexOf、lastIndexOf、trim（去除前后空格）

​		subString(int beginIndex)  //从beginIndex位置一直到最后，包括beginIndex

​		subString(int beginIndex,int endIndex)

```java
String str = new String("str");
String substr = str.substring(0,2);
System.out.println(substr);  //输出st

//说明不包含endIndex位置处的索引[beginIndex,endIndex)
```

​		charAt()

```java
//想取字符串中的某一位置数组，不能直接用str[index]，也不能直接用str.value[index](因为是私有)，只能用str.charAt(index)
```

​		toUpperCase、toLowerCase、toCharArray

​		concat拼接字符串

```java
//原地操作
String str = new String("hello");
str = str.concat(",").concat("gongxiaolong");
System.out.println(str); //hello,gongxiaolong
```

​		str.replace(A,B) 将str中**所有的**A用B替换

```java
//非原地操作，使用后该对象并不会变，所以需要一个新的对象接着返回的结果
String str = "aaa and bbb bbb bbb";
String strNew = str.replace("bbb","ccc");
sout(strNew)  //"aaa and ccc ccc ccc"
sout(str)	//"aaa and bbb bbb bbb"
```

​		**str.split("A")**用字符串A将str进行分割，分割后返回一个字符串数组非原地操作，如果A中有转义字符，需要用到\，详见P586

​		**str1.compareTo(str2)**

```java
//返回值：
//0：str1与str2长度与每一位都相等
//大于0：str1“大于”str2
//小于0：str1“小于”str2

//大小的比较规则：
//相同长度：逐位比较alphabatical，返回第一个不相同位的差值
//不同长度：先比较重合部分，按相同长度比较的规则
//		  如果重合部分相同，则返回str1长度 - str2长度
```



### StringBuffer

> String的问题

​		**String类中保存的value是不可以改变的**（因为value指向常量池，常量池不能变，value是final修饰的，也不能变）每次更新都需要重新开辟空间（常量池和堆中）（详细解释见记录3第30条）

​	因此java设计者还提供了**StringBuilder**和**StringBuffer**来增强String的功能。



> StringBuffer

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230623222018474.png" alt="image-20230623222018474" style="zoom:50%;" />

1. StringBuffer的数据存在其父类AbstractStringBuilder的成员变量char[] value里，所以在构造StringBuffer时需要声明大小，直接new StringBuffer()的话大小为16，new StringBuffer(String str)的话char[]的大小就为str.length()+16。

​		但是输出StringBuffer.length()的时候可不是输出char[]的容量，而是输出真正含有的字符的数量！



​	2.关于用null的String给StringBuffer的神奇现象

```java
String str = null;
StringBuffer sb = new StringBuffer();
sb.append(str);
//结果就是StringBuffer真的把“null”当作字符串存到了value里。
// 调用过程：StringBuffer类的append方法 --> (super.append) --> AbstractStringBuilder类的append方法 --> (发现str为null) --> AbstractStringBuilder类的appendNull方法

//再看下面这种情况：
StringBuffer sb1 = new StringBuffer(str);

//会抛出空指针异常，因为初始化首先要分配char[]的容量，需要str.length(),而str为null。
//public StringBuffer(String str) {
//        super(str.length() + 16);
 //       append(str);
 //   }
```



### StringBuilder

> 继承关系

​	与StringBuffer的继承关系完全相同

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221206205054844.png" alt="image-20221206205054844" style="zoom:67%;" />

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221206205121524.png" alt="image-20221206205121524" style="zoom:80%;" />



> 与StringBuffer关系

​	API与StringBuffer相同，**但是：**

​		StringBuffer线程安全，可用于多线程

​		StringBuilder线程不安全，只适用于单线程

​	那为什么还要有StringBuilder呢？自然有它的优势：

​		（杀鸡焉用牛刀）

​		StringBuilder是Buffer的一个简易替换，它的大多数实现都比Buffer要快，所以**字符缓冲区只被单个线程		使用**，最好用StringBuilder



> 为什么Buffer适用于多线程而Builder不适用？

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221206205925820.png" alt="image-20221206205925820" style="zoom:50%;" />

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221206205952310.png" alt="image-20221206205952310" style="zoom:50%;" />

​	如图，Buffer的方法都有synchronized关键字，而builder没有，也就是说前者有互斥处理，







### Math

​	静态方法，直接调用即可

​	见老韩pdf—P601/直接在idea中ctrl+b查看



> 注意：

​	Math.random() 返回的是一个[0,1)的浮点数，不包括1！！！看pdf上的例子，在表示int型随机数时要注意！！！

### Date/Calender/LocalDdate...

> 第一代日期类：Date

1、java.util.Date	而不是	 java.sql.Date

​		不要用错

2、workflow

```java
//无参构造器构造Date类的对象，然后才能用Date的方法，说明要用的方法不是属于类的，而是属于对象的
Date date = new Date(); 
sout(date); //输出示例：Fri Dec 09 20:06:18 CST 2022

//上面这个时间是默认的时间格式，我们可能看不习惯，需要转化为我们看得懂的形式
//需要使用到SimpleDateFormat这个类
//这个类也得先实例化，才能使用里面的方法,注意，实例化/初始化的时候就需要传入需要的格式参数，是一个字符串
SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E")
//然后使用sdf的format方法将看不懂的时间转化为String，注意：format传入的是date而不是date.getTime()，date.getTime狗都不用
String format_time = sdf.format(date) //输出实例：2022年12月09日 08:10:35 星期五
    
//sdf不光可以把Date型变量转化为String，也可以把“格式化”的String转化为Date。
String s = "1996 年 01 月 01 日 10:20:30 星期一";
Date parse = sdf.parse(s);
System.out.println("parse=" + sdf.format(parse)); //parse=1996年01月01日 10:20:30 星期一
```

sdf格式参数中y、M、d这些都是由特殊含义的，具体如下图：
![image-20221209201349160](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209201349160.png)



```java
//Date的另一种初始化方法，传入长整型，相当于getTime获得的那个数
Date date = new Date(21312442l);
sout(date) //输出：Thu Jan 01 13:55:12 CST 1970
```



> 第二代日期类：Calendar

![image-20221209204350069](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209204350069.png)

​	<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230625175723506.png" alt="image-20230625175723506" style="zoom:50%;" />

​	1.类继承图跟Date类一摸一样 ❌

​		并不是完全一样的 

​	2.为什么需要Calendar类？

​			Date类是格式化的类（直接打印就能输出整串时间信息），虽然可以看到年月日这些信息，但是没法单独打印出来。

​			Calendar类中fields特别多，这些字段就是分开的年、月、日等信息，可以单独打印，但Calendar类不是格式化的类，也就是说无法直接输出整串信息，但是可以在得到单独信息后自定义。

​			Date和Calendar没有谁好谁坏，只是满足不同需求而已。

3.使用方法：

```java
//Calendar的构造器是私有化的，所以提供了getInstance方法
Calendar c = Calendar.getInstance();

//获取字段用get方法
//传入参数还要加一个类名有些奇怪，但先记住
//千万不能直接c.YEAR或者Calendar.YEAR,因为Calendar类是抽象类，无法直接获取其字段，get里面有complete方法好像是完成这个抽象类的继承，然后再获取字段的。
System.out.println("年：" + c.get(Calendar.YEAR));
System.out.println("月：" + (c.get(Calendar.MONTH) + 1));// 这里为什么要 + 1, 因为 Calendar 返回月时候，是按照 0 开始编号
System.out.println("日：" + c.get(Calendar.DAY_OF_MONTH));
System.out.println("小时：" + c.get(Calendar.HOUR)); //hour是12进制，HOUR_OF_DAY是24小时进制
System.out.println("分钟：" + c.get(Calendar.MINUTE));
System.out.println("秒：" + c.get(Calendar.SECOND))；

```



> 第三代日期类：LocalDate、LocalTime、LocalDateTime

 	1.Date类被弃用：jdk1.1引入Calendar后就被启用了

​	2.Calendar类的缺点：1234![image-20221209212031723](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209212031723.png)

​	3.于是再JDK8加入了三个新的日期类

​	4、LocalDate只包含年月日

​			LocalTime只包括时分秒

​			LocalDateTime包括前两者

​			接口很复杂，所以功能强大<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209212652786.png" alt="image-20221209212652786" style="zoom: 33%;" />



​	5.使用方法：

```java
//构造器都是私有的，不能构造，也不需要构造，静态方法now类似于getInstance，直接使用它就可以返回一个格式化的对象
LocalDateTime ldt = LocalDateTime.now();//2022-12-09T21:37:30.893
LocalDate ld = LocalDate.now();//2022-12-09
LocalTime lt = LocalTime.now();//21:39:14.624

//也可以得到年月日这些字段信息，如下图：
//注意，这些方法不属于类，而属于对象，所以使用前应该先用now()获取一个对象
//注意：getMonth得到的是March这种英文字符串，getMonthValue得到的才是 345这种数字
```

![image-20221209214520955](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209214520955.png)

### System

> 老韩只介绍了System类的四个常用方法：

1.

```java
//1.退出当前程序，括号里的0表示退出的状态，一般正常退出都是0，更多状态请自行百度
System.exit(0)；
//2.arraycopy:复制数组元素，是Array.copyOf()的底层代码，不过数组拷贝一般用后者而不是前者
System.arraycopy(srcarr,srcStart,destarr,destStart,copyLen);
//如果copylen过长，并不会用null给补，而是会报错ArrayIndexOutOfBoundsException

//3.currentTimeMillens:返回当前时间距离 1970-1-1 的毫秒数
System.currentTimeMillens()
```





### Array

> array在java中表示数组，Array就是给数组用的类，里面包含一系列数组操作方法
>
> List是集合，后面再学
>
> 数组可以用**Array.asList(arr)**转化为集合，后面详细讲



> Arrays类有好多静态方法，这里不细讲，直接见老韩的pdf课件，下面是一个需要注意的事项：



1.sort排序包括自然排序（由小到大）和  定制排序

```java
Integer arr[]  = {-1,90,3,2,33,87};
//定制排序传入两个参数 （1）要排序的数组	(2)实现了Comparator接口的类，重写compare方法。可以直接用匿名内部类

Arrays.sort(arr,new Comparator(){
    				public int compare(Object o1,Object o2){
                        return (Integer)o1 - (Integer)o2;
                    }
				}
           )
```

 compare方法返回值的正负，会影响整个排序结果：o1 - o2就是默认的升序

​									   													o2 - o1就是降序



2.copyOf

```java
Integer arr[]  = {-1,90,3,2,33,87};
Integer arrNew[]  = Arrays.copyOf(arr,arr.length);
//参数说明：
//	第二个参数表示从第一个元素开始拷贝几个元素，0表示不拷贝，返回[],arr.length就表示都拷贝，如果传入一个负数就会产生异常:NegativeArraySizeException ；如果拷贝长度大于arr.length,多出来的几个会用null填充
```



3.asList

​	功能：将array转化为List，转化后的运行类型是ArrayList（是Arrays的一个内部类）

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221207183343772.png" alt="image-20221207183343772" style="zoom:50%;" />

```java
Integer[] ints = {9,3,3,2,2,4,3,9};
//用法1：传入数组
List asList = Arrays.asList(ints);	//结果为asList = [9,3,3,2,2,4,3,9]

//用法2：直接传入数组元素
List asList = Arrays.asList(2,3,4,5,6,1)；	//结果为asList = [2,3,4,5,6,1]
```



### BigInterger、BigDecimal

> BigInteger

​	存储大整数的类，大数传入一般用字符串的形式，且这种大数变量不能直接+-*/，而是要通过其内置的加减乘除方法

```java
//
BigInteger biginteger = new BigInteger("99999999999999933929923299999999999999999");
BigInteger biginteger2 = new BigInteger("999999999999999339299299");

BigInteger resAdd = biginteger.add(biginteger2);  //括号里也可以是long 和 int型变量
BigInteger resSub = biginteger.substract(biginteger2);	//括号里也可以是long 和 int型变量
BigInteger resMul = biginteger.multiply(biginteger2);  //括号里也可以是long 和 int型变量
BigInteger resDiv = biginteger.divide(biginteger2);  //括号里也可以是long 和 int型变量
```



> BigDecimal

​	传入、加减乘除的方法跟前面都一样，只有在除的时候可能出现无线循环/不循环小数，会报出ArithmeticException，解决方法如下：

```java
bigDecimal.divide(bigDecimal2, BigDecimal.ROUND_CEILING)；
//BigDecimal.ROUND_CEILING表示在分子精度上向上取整
   
```

 	讲解下四个ROUND参数，ceiling、floor是向上向下取整，考虑正负的

​												而down、up是只关心绝对值的

​	也就是说，当结果为正数的时候，二组作用就相同了；若为负数，则二组作用正好相反

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209185205350.png" alt="image-20221209185205350" style="zoom: 67%;" />

![image-20221209185220697](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209185220697.png)



## 记录八 集合

> 增强for循环的底层原理

​	底层其实也是iterator（增强for循环只适用于数组和集合类）

```java
List<Integer> list = new ArrayList();
Iterator<Integer> iterator = list.iterator();
for(Integer num:list){  // 在这一行打断点

}

// 断点会依次进入ArrayList的iterator方法和hasNext、next()方法，
// 这几个方法都是Iterator接口定义的方法，而List的”爷爷“是Iterable接口，其只是返回了一个iterator对象
// 所有这三个方法不是Iterable定义的而是Iterator定义的！！
public interface Iterable<T> {
    /**
     * Returns an iterator over elements of type {@code T}.
     *
     * @return an Iterator.
     */
    Iterator<T> iterator();
}
```

增强for循环所作的事情可以概括为：
	1.调用集合类实现的Iterable数组的iterator方法，返回一个Iterator对象

​	2.交替调用该对象的hasNext()和next()方法

所以下面这种代码是不对的

```java
List<Integer> list = new ArrayList();
Iterator<Integer> iterator = list.iterator();
for(Integer num:iterator){}

// 返回Iterator对象只是增强for循环所作的一部分！！所以上面完全不够！！
```



## java语法笔记：

### 增强for循环

​	用于简化遍历数组，通过下面对比可看出区别：

```java
int[] nums = {1,2,3};

//传统遍历方法
for(int i=0;i<nums.length;i++){
    sout(nums[i]);
}

//使用 增强for循环 进行遍历
for(int i:nums){
    sout(nums[i]);
}

//类似于python中的 for i in nums:

```



### fields和properties

​	![image-20221209190905391](C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20221209190905391.png)

​	IDEA的java类中的这两个组成成分容易搞混，解释下：

- fields，字段，就是指类中的属性，不管是私有的还是公有的，只要是属性，就算。
- properties,属性，有些类似于私人财产的意思，只要类中有getXXX或者setXXX，那么这个XXX就会被当作properties，甚至不用是fields中一个。(老韩视频487讲了，就不用再参考网上的说法了！)

###  字面量/直接量

​		[参考链接](http://c.biancheng.net/view/5732.html)

​	定义：java程序中通过源代码直接给出的值

​	只有三种类型可以指定直接量：基本数据类型/字符串/null类型

​	（null类型只有一个直接量，就是null，可以赋给任何引用类型的变量，表示该引用变量保存的地址为空）

​	（不同于null，其它类型的直接量只能赋给对应类型或者相近类型）

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230623175219070.png" alt="image-20230623175219070" style="zoom:50%;" />

​	（注意区分：直接一个小数表示的是double类型的直接量，在后面加上或者F才是float类型的直接量）



### surround with

<img src="C:\Users\15054\AppData\Roaming\Typora\typora-user-images\image-20230625185436247.png" alt="image-20230625185436247" style="zoom:50%;" />

一段代码想要被if/for/try_catch包在里面，可以用这个快捷键：
**ctrl + alt + t**



## 快捷键

> 显示所有的快捷键

ctrl + j



> 快速生成带迭代器的while

itit



> 包围代码块

ctrl + alt + t



> 类中快速添加getter/setter/constructor等

alt + insert



> 增强for循环

I

E

## 其它知识



	### javaEE和javaSE

javaSE，java Standard Edition，java标准版，适用于一般应用的开发

javaEE，java Enterprise Edition，java企业版，多用于企业级应用的开发，也叫J2EE

可以将javaSE看作javaEE的一个子集



​	



​	
