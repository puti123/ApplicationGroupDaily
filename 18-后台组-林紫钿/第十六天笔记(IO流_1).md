[toc]
# IO流
## 字符流
### Writer(写入字符流的抽象类)
- 基本方法：
 **(都会抛出异常throws IOException)**

1.写入数据
```
void write(char[] cbuf)//写入字符数组
void write(int c)//写入单个字符
void write(String str)//写入字符串
void write(String str,int off,int len)//写入字符串的某一部分
```
2.关闭流：
```
abstract void close()//关闭此流，但要先刷新
```
3.刷新
```
abstract void flush()//刷新该流的缓冲
```
- 基本的文件操作：
##### FileWriter子类
<1>创建一个FileWriter对象。该对象一被初始化就必须要明确操作的文件，而且该文件会被创建到指定的目录下，如果该目录下已有同名文件将被覆盖（**该步就是明确数据要存放的目的地**）
```
FileWtiter fw = new FileWriter("demo.txt");
```
<2>调用write方法，将字符串写入流中
```
fw.write("abc");
```
<3>刷新流对象中的缓冲中的数据(将数据刷到目的地中)
```
fw.flush();
```
<4>关闭流资源，但是关闭之前会刷新一次内部的缓冲中的数据
```
fw.close();
```
- 异常处理：最后要在finally中关闭流
- 文件的续写：
```
FileWriter(String fileName,boolean append)throws Exception
//append - 一个 boolean 值，如果为 true，则将数据写入文件末尾处，而不是写入文件开始处。
```
参考代码： day18.FileWriterDemo/     FileWriterDemo2(处理异常)/        FileWriterDemo3(文件续写)
### Reader(读取字符流)
- 基本方法： (也会抛出IOException异常)    
1.读取字符文件：
```
int read()//返回int，读取单个字符
 int read(char[] arr)//返回读取的字符数，将字符读入数组,读到末尾没有字符会返回-1
```
2.关闭
```
void close()//关闭流并释放所有关联资源，不刷新
```
##### FileReader
用来读取文件的便捷类
```
//创建一个文件读取流对象，和指定名称的文件相关联
FileReader fr = new FileReader("demo.txt");
//要保证该文件是已经存在的，如果不存在，会发生异常FileNotFoundException

//调用read()方法读取数据
fr.read()
```

参考代码： day18.FileReaderDemo/FileReadererDemo2(通过字符数组读取文件)/FileReaderTest     
综合代码：day18.CopyTest(注意异常处理方式和流关闭(必须两个都关))
## 字符流的缓冲区
缓冲区：提高流的操作效率
##### BufferedWriter类
构造方法:BufferedWriter(Writer out)
- 基本方法：
```
void close()//关闭流，但要先刷新它
void flush()//刷新该流的缓冲
```
 !!!注：只要用到缓冲区，就要记得刷新
```
void newLine()//写入一个行分隔符
```
参考：day18.BufferedWriterDemo
##### BufferedReader类
构造方法：BufferReader(Reader in)
```
重点方法：String readLine()//读取一行
//返回包含该行内容的字符串，不包含任何行终止符
```
参考：day.BufferReaderDemo/MyBufferReader
###### LineNumberReader子类
```
int getLineNumber()//获取当前行号
void setLineNumber()//设置当前行号
```
##### 装饰设计模式：
装饰类：定义类对已有的对象进行功能的增强，并提供加强功能。   
装饰类通常会通过构造方法接收被装饰的对象并基于被装饰的对象的功能，提供更强的功能
参考：day.MyBufferReader