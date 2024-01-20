#                                                     IO流

**文件**：存放数据的地方,位于磁盘中。(目录也被当做一个文件)

**输入流** ：将数据从磁盘中的文件读入到运行程序的内存中。

**输出流**： 将运行程序的内存的数据写入到磁盘中的文件中。

### 创建文件对象相关构造器和方法

- `File file = new File(String filePath);` //file只是个对象到目前为止，操作文件的对象

  `file.createNewFile();`//将文件写入到磁盘中

- `File file = new File(File parent,String child);`

  parent指的是目录。

- `File file = new File(String parent,String child);`

### 目录操作

- mkdir创建一级目录
- mkdirs创建多级目录   
- delete删除空目录或文件

### IO流原理

| 抽象基类 | 字节流       | 字符流 |
| -------- | ------------ | ------ |
| 输入流   | InputStream  | Reader |
| 输出流   | OutputStream | Writer |

- 字节流（8bit），易于处理二进制文件
- 字符流（按字符），易于处理文本文件

### InputStream

- ##### FileInputStream

  ```java
  int readData = 0;
  String filePath = "...";
  FileInputStream fileInputStream = null;
  try {
      fileInputStream = new FileInputStream(filePath);
      while((readData = fileInputStream.read() != -1){
          System.out.print((char)readData);
         //字节流每次读取一字节，当读到-1时表示结束
         //read()返回类型为int
      }
      }catch (IOException e){
       e.printStackTrace();   
           } 
   
  ```

### OutputStream

- FileOutputStream

  ```java
  public void writeFile(){
      FileOutputStream fileOutputStream = null;
      String str = "Hello";
      fileOutputStream = new FileOutputStream(filepath);//可以加上一个true参数，从而不覆盖之前写的
      fileOutputStream.write("a");//将"a"写入file中
      fileOutputStream.write(str.getBytes());//转换为byte数组
  }
  ```



**FileReader** 相关方法

- `new FileReader(File/String)`
- `read()`每次读取单个字符，到文件末尾会返回-1
- `read(char[])`每次读取多个字符到char数组中，并返回取到的字符数，如果到文件末尾，会返回-1

**FileWriter**相关方法

- `new FileWriter(File/String)`
- `new FileWriter(File/String,true)`
- `writer()`写入单个字符
- `writer(char[])`写入一个数组
- `writer(char[],off,len)`
- `writer(String)`
- `writer(String,off,len)`

FileWriter使用后，必须关闭（close）或者刷新（flush)

### 节点流和处理流

节点流可以从一个特定的数据源（存放数据的地方）读写数据。

处理流（包装流）是对节点流的包装，功能更加强大。可以消除不同节点流的实现差异，更加方便输入输出。

运用到了设计模式中的修饰器模式。 

- #### BufferedReader(字符流)

  关闭处理流，只需要关闭外层流，底层会帮助我们关闭内层流。‘

  `String readLine( )`是按行读取，当返回null,表示读取完毕。

  `new BufferReader(FileReader f)` 

- #### BufferedWriter

  `writer(String str)`

  `newLine()`插入一个和系统相关的换行

- #### BufferedInputStream

  是字节流，在创建BufferedInputStream时，会创建一个内部缓冲区数组

  继承父类后会继承一个InputStream对象。

- #### BufferedOutputStream

  `BufferedOutputStream(OutputStream out)`

  `BufferedOutputStream(OutputStream out,int size)`已将具有指定缓冲区大小的数据写入到指定底层的输出流。

## 对象流

序列化：在保存数据时，保存数据的值和数据类型

反序列化：恢复数据时，恢复数据的值和数据类型

需要实现Serializable接口（标记接口）

- #### ObjectOutputStream

  `writeBoolean()`

  `writerChar()`

  `writerDouble()`

  `writerObject()`

  ......

- #### ObjectInputStream

  读取(反序列化)的顺序需要和保存数据的(序列化)的顺序一致。

  关闭外层流即可。

  返回的值都是Object，需要显示转换。

## 转换流

- #### InputStreamReader

  