[toc]
## 字节流
### OutputStream(输出流)
##### FileOutputStream
- 基本方法:
写入：
```
void writer(int b)//将指定字节写入输出流
void write(byte[] b)//从指定byte数组写入输出流中
---
eg.
FileOutputStream fos = new FileOutputStream("fos.txt");//重复写入在后面加true.
fos.write("abc".getBytes)//或者fos.write(buf数组);
//不用刷新，直接写入流中，与字符流的区别在于：比如中文需要两个字节，字符流需要拿到两个字节存入缓冲区后去获取编码表。
```
##### FileInputStream(输入流)
- 基本方法：获取：
```
int available()//返回实际可读字节数
int read()//读取一个数据字节
int read(byte[] b)//从输入流中获取b.length长度的数据读入byte数组中
//读取已达末尾返回-1
```
参考：day19.FileStream 
## 字节流的缓冲区
##### BufferedOutputStream
```
BufferedOutputStream(OutputStream out )//记得刷新
```
 ##### BufferedInputStream
 参考：day19.MyBufferedInputStream(原理)
```
BufferedInputStream(InputStream in)
```
###### 读取转换流(字节流-->字符流)
** InputStreamRead：字节流通向字符流的桥梁 **
```
InputStreamReader(InputStream in)//in为节流文件
```
转换后可以去使用BufferedReader中的方法：readLine();newLine();
```
eg.
BufferedReader bufr = new BufferedReader(new InputStreamReader(System.in));//键盘录入
```
！！！System类中的out(标准输出流)返回PrintStream； in(标准输入流)返回InputStream
###### 写入转换流
OutputStream：字符流通向字节流的桥梁。记得刷新

```
BufferedWriter bufw = new BufferedWriter(new OutputStreamWriter(System.out));
```
参考：day19.TransStream(转换流)/Systemfo/Exception(异常日志)
##### 流的基本操作规律
<1>明确源和目的   
源：输入流(InputStream,Reader)    
目的：输出流(OutputStream,Writer)  
<2>操作的数据是否是纯文本   
是：字符流    
否：字节流   
<3>当体系明确后再明确要使用哪个具体对象   
通过设备来区分：  
源设备：内存，硬盘，键盘   
目的设备：内存，硬盘（文件），控制台   


eg1.将一个文本中数据存储到另外一个文件中，复制文件    
<1>明确体系：   
**源**：(因为是源所以使用读取流)InputStream,Reader   
是不是操作文本文件：是，Reader   
是否提高效率：是，加入Reader中的缓冲区BufferedReader  
**目的**：OutputStream Writer
是否是纯文本：是，Writer
<2>明确设备：
硬盘上的一个文件，对象Reader：FileReader   
存储到另外一个文件：FileWrite对象：BufferedWriter


eg2.将键盘录入的数据保存到一个文件中   
<1>源：InputStream, Reader  
-->纯文本：Reader(BufferedReader)  
-->设备：键盘。对象：System.in(字节流)  
-->将字节流System.in转换Reader读取转换流InputStreamReader  
-->提高效率BufferedReader  
<2>目的：OutputStream,Writer  
-->纯文本：Writer  
-->设备：硬盘，一个文件FileWriter  
-->提高效率
## File类
用来将文件或文件夹封装成对象；文件和目录路径名的抽象表示形式
- 构造方法：
File(String pathname)创建对象  
File(File parent(父目录),  String child(子目录)    
- File的常见方法：  
<1>创建：
```
boolean createNewFile();//在指定位置创建文件，如果该文件已经存在，则不创建,返回false
boolean mkdir()//创建目录(只能创建一级目录)
boolean mkdirs()//创建目录，可以创建多级目录
static File createTempFile(String prefix(前缀),String suffix(后缀,可以为null，将使用.tmp)
```
<2>删除:
```
boolean delete()//删除文件或目录
void deleteOnExit()//在虚拟机终止时，删除指定文件或目录
```
<3>判断：
```
boolean canExecute()//判断文件是否能执行
int compareTo(File pathname)//比较文件名
boolean exists()//判断文件是否存在
boolean isFile()//判断是否是文件
boolean isDirectory()//判断是否是目录
//判断目录和文件之前必须先判断是否存在
boolean isHidden()//判断文件是否是一个隐藏文件
boolean isAbsolute()//判断是否为绝对路径名
```
<4>获取：
```
String getName()//获取文件或目录名称

File getAbsolutePath()//返回绝对路径名形式File类对象
String getAbsolutePath()//返回绝对路径名字字符串

String getPath()//返回路径名字字符串
String getParent()//返回此路径的父目录名字字符串

long lastModified()//返回文件最后一次修改的时间

long length()//返回指定路径表示的文件的长度

boolean renameTo(File dest)//重命名文件

static File[] listRoots()//列出可用的系统根目录

String[] list()//返回指定目录的文件和目录，调用list方法的file对象必须封装了目录，且存在
String[] list(FilenameFilter filter)//文件名过滤
//FilenameFilter接口：通过boolean accept(File dir, String name)的判断来判断是否满足过滤器文件和目录
```
参考：day20.fileDemo/fileDemo2/fileDemo3/JavaFilst(列出目录下所有内容--递归，带层次)/RemoveDir(删除一个带内容目录--递归；不放回收站)
