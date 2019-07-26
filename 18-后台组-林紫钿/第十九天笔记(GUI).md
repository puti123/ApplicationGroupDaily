[toc]
## GUI
创建图形化界面：
1.创建Frame窗体；   
2.对窗体进行基本设置：大小，布局，位置    
3.定义组件    
4.将组件通过窗体的add方法添加到窗体中；   
5.让窗体显示，通过setVisible(true)。
### Frame
- 构造方法：
```
Frame()//构造一个最初不可见的Frame实例
Frame(String title)//构造有标题的frame对象
```
- 方法摘要
```
setVisible(boolean b)//显示隐藏组键
setSize(x,y)//设置窗口大小
setLocation(x,y,顶点左边距，上边距)//设置本地位置
setBounds(x,y,width,hight)//移动组件并调整大小
```
- 布局:
流式布局：FlowLayout()//从左到右   
边界式布局：BorderLayout()//东南西北中     
网格式布局：GridLayout()  
卡片式布局：CardLayout()
### 事件监听机制
addWindowListener(WindowListener l)//添加指定的**窗口监听器**，接收窗口事件：WindowListener是接口其子类WindowAdapter是事件适配器，WindowAdapter已经实现了WindowListener接口    
void windowClosing(WindowEvent e)//在关闭窗口时被调用
####  Button按钮事件
```
void addActionListener(ActionListener l)//动作监听器
ActionListener也是一个接口该接口通过对void actionPerformed(ActionEvent e)方法的复写
```
#### 键盘事件
```
void addKeyLiatener(KeyListener l)
//KeyListener也是通过适配器KeyAdapter来调用处理方式
void keyPressed(KeyEvent e)//按下某个键时调用此方法
boolean isControlDown()//返回Control符是否被按下，可用来形成组合键
char getKeyChar()//返回关联字符
int getKeyCode()//返回键关联整数keyCode
consume();//屏蔽键,使不会按照此事件的源代码处理此事件，不会输入到该文本框
```
#### 鼠标事件
```
void addMouseListener(MouseListener l)//也是通过抽象适配器MouseAdapter
int getClickCount()//返回此事件关联的鼠标单击次数
void mouseEntered(MouseEvent e)//鼠标进入组件时被调用
void mousePressed(MouseEvent e)//鼠标按下时被调用
```
#### TextField(文本框)
- 构造方法：
```
TextFild()
TextField(int columns)//指定列
getText()//获取文本框内容

```
#### TextArea(文本区域)  
```
TextArea(int rows, int columns)//构造指定行列的文本区域
append()//追加
文本
setText()//设置文本区域内容
```

#### 对话框Dialog
相当于一个新的Frame窗口，也需要显示,设置，布局   
###### FileDialog
```
String getDiredctory()//获取文件对话框的目录
String getFile()//获取文件对话框选定的文件
```
#### Label(标签)
```
setText(String text)//设置指定文本标签
getText()//获取标签文本
```
#### 菜单(menu)和菜单条目(MenuItem)和MenuBar(菜单组件)
Menu为MenuItem的子类，设置好菜单后最后要将菜单组件MenuBar添加至Frame中
```
Menu add(Menu m)//将指定菜单添加进菜单栏
MenuItem add(MenuItem mi)//将指定菜单项添加到此菜单
```

