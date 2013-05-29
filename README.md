PySLGalMaker
============

**描述：一个轻量级的galgame引擎，使用语言为python，依赖包为pygame**


**使用说明**

从github获取程序：

    git clone git@github.com:SeavantUUz/PySLGalMaker.git 
**注意**
* 通过修改script.sanae来书写剧本
* 把BGM放入BGM文件夹
* 背景图片放入BG文件夹
* 立绘放入PORTRAIT文件夹
* SYSTEM文件夹中负责存档界面以及离开按钮的定制，可自由修改
* 书写script.sanae需要按照一定的语法，后面会详述
* `python run.py`
* 如果对具体实现感兴趣，请参阅个人博客上的[关联文章](http://www.kochiya.me/2013/01/25/python%E5%88%B6%E4%BD%9Cgalgame%E5%BC%95%E6%93%8E.html)

**已实现语法**
- [ ] 背景显示语法
- [ ] 音乐指定语法
- [ ] 立绘显示语法
- [ ] 文本显示语法
- [ ] 选择枝语法
- [ ] 索引语法

**已知问题**
* 理论上，这个程序可以在Linux或者Windows下运行，事实上，最开始也做了这方面处理。但是后来部分，时间仓促没有添加，所以，windows下可能出现乱码问题。推荐的方法是，用vim等文本编辑器把字符编码转成gb2313，可能能解决。
* 本机测试时，存档功能表现很不稳定，暂时不知道问题出处。

**语法说明**  
读完下面语法后，建议读一读自带的script.sanae文件，里面是默认的剧本  
+ 索引  
    语法模式:数字  
    解释:  
      这是必填项，代表当前的索引。一般来说都只是个数字。这一版，相邻两帧只能是连续的数字---除了有选择按钮的帧。注意，索引必从0开始。  
    举例:      
    0  

+ 背景  
    语法模式：[background = 'xxx.xxx']  
    解释:  
      [],background,=为必填项，等号两旁可以有空格也可以没有，单引号括住图片的名字，图片请放在BG文件夹下。所有符号均为英文输入情况下的符号。这句话的作用是插入背景图片。图片的格式的话，常见的图片格式都能解析。大小会自动转成 800x600，最好不要用竖着的图片  
    举例:  
    [background = 'sanae.png']  

+ BGM  
    语法模式: [BGM = 'xxx.xxx']  
    解释：  
      要求同上，支持音乐格式，windows下为mp3和wav,Linux下为wav和ogg。这句话插入背景音乐，播放方式为无限循环。  
    举例：  
    [BGM = 'uuz.wav']  

+ 文本  
    语法模式: <xxxxxx>  
    解释:  
      文本，也就是一般gal的文字。尖括号的所有内容均会出现在文本框中。有上限，大致是120个字，支持两种形式:  
      * <风笳：今天天气哇哈哈>
      * <今天天气哇哈哈>
      对a这种形式，显示时，风笳会单独放在第一行，并加上：，表示说话人，剩下内容在第二行显示。而b的话，第一行留空，第二行显示。具体请查看script。有一个比较大的bug是：如果当前帧没有说话人，但是出现了：，那会造成一些问题,建议是文本中不出现 :  
    举例：  
    * <th13.5,th14，全面自机丢失>  

+ 选择枝  
    语法模式：    
    [choice]    
    xxxx->xxx   
    xxxx->xxx   
    [/choice]   
    解释：      
      这是出现选项按钮的写法，事实上，[choice]和[/choice]并不影响解析，也就是说，你写成：  
      xxxx->xxx  
      xxxx->xxx  
      也是完全可以的。但是为了保持脚本的易懂，推荐加上。当然，你自己定义为：  
      [b]  
      xxxx->xxx  
      xxxx->xxx  
      [/f]  
      都是可以的。  
    举例：  
    [choice]  
    选择卯之花->40  
    选择葵->50  
    选择佐奈->60  
    选择苏方->200  
    [/choice]  

+ 人物立绘  
    语法模式：{'图片名';1.(切割位置);2.(图片在屏幕上大小);3.(图片在屏幕上位置)}  
    解释：  
      最复杂的语法，需要有四个参数，切割位置指在原图上进行切割的右下角坐标。  
      支持多行解析  
      支持一次初始化传递之后的缺省传递  
      具体的请参看 script中的示例  
    举例：  
    * {'sanae.png';1.(600,600);2.(200,200);3.(200,200)}(初始化传入形式)
    * {'sanae.png';1.(600,600);2.(200,200);3.(200,200)
        'sanae1.png';1.(600,600);2.(300,300);3.(0,0)}(多行初始化传入形式)
    * {'sanae.png';2.(300,400)}(缺省出入形式)
    * {'sanae.png';}(移除sanae.png立绘)
    * {}(移除全部立绘)

如果有问题请联系:`axdiaoqi220@gmail.com`
请随意fork

License
-----------------------------
GPL

