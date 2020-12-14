[toc]
### IO数据流
#### Java流输入/输出原理
![Java输入/输出流原理]()
- 在Java程序中，对于数据的输入/输出操作以 =="流"== (stream)方式进行；J2SDK提供了各种各样的 =="流"== 类，用以获取不同种类的数据；程序中通过标准的方法输入或输出数据。

#### 输入/输出流的分类
- Java.io 包中定义了多个流类型（类或者抽象类）来实现输入/输出功能；可以从不同的角度进行分类：
    - 按数据流的方向不同可以分成输入流和输出流。
    - 按处理数据单位不同可以分为字节流和字符流。
    - 按照功能不同可以分为节点流和处理流。
- J2SDK 所提供的所有流类型位于包java.io内都分别继承自以下4个抽象流类型

||字符流|字节流|
|--|--|--
输入流|InputStream|Reader|
输出流|OutputStream|Wirter

###### 节点流和处理流
- 节点流可以从一个特定的数据源（节点）读写数据。
- 处理流是“连接”在已存在的流（节点流或者处理流）之上，通过对数据的处理为程序提供更加强大的读写能力。

#### InputSteam
- 继承自InputSteam的流都是用于向程序输入数据，且单位为字节（8bit）：
    - 节点流：
        - FileInputSteam
        - PipedInputSteam
        - ByteArrayInputSteam
        - StringBufferInputSteam
    - 处理流：
        - FilterInputSteam
        - SequenceInputSteam
        - ObjectInputSteam
```
graph LR
InputSteam-->FileInputSteam
InputSteam-->PipedInputStem
InputSteam-->FilterInputSteam
InputSteam-->ByteArrayInputSteam
InputSteam-->SequenceInputSteam
InputSteam-->StringBufferInputSteam
InputSteam-->ObjectInputSteam
FilterInputSteam-->LineNumberInputSteam
FilterInputSteam-->DataInputSteam
FilterInputSteam-->BufferedInputSteam
FilterInputSteam-->PushbackInputSteam
```
###### InputSteam的基本方法
语法|意义|
--|--|
int read() throws IOException|读取一个字节并以整数形式返回(0~~255)，返回-1已到输入流的末尾。|
int read(byte[] buffer) throws IOException|读取一系列字节并存储到一个数组buffer，返回实际读取字节数，如果读取前已到输入流的末尾则返回-1|
int read(byte[] buffer,int offer,int length) throws IOException|读取length个字节，并存储在buffer，从offer开始读取。返回实际读取的字节数，如果读取带输入流末尾则返回-1|
void close() throws IOException|关闭流释放内存资源|

#### OutputSteam
- 继承OutputSteam的流是用于程序中输入数据，且数据单位为字节（8bit）：
    - 节点流
        - FileOutputSteam
        - PipedOutputSteam
        - ByteArrayOutputSteam
    - 处理流
        - FilteredOutSteam
        - ObjectOutputSteam
```
graph LR
OutputSteam-->FileOutputSteam
OutputSteam-->PipedOutputSteam
OutputSteam-->FilteredOutputSteam
OutputSteam-->ByteArrayOutputSteam
OutputSteam-->ObjectOuputSteam
FilteredOutputSteam-->DataOutputSteam
FilteredOutputSteam-->BufferedOutputSteam
FilteredOutputSteam-->PrintSteam
```

###### OutputSteam的基本语法
语法|意义|
--|--|
int write() throws IOException|向输出流写入应该字节数据，该字节数据为参数b的低8位。|
int write(byte[] buffer) throws IOException|将一个字符类型的数组中的数据写入输出流|
int write(byte[] buffer,int offer,int length) throws IOException|将一个字节类型的数组（buffer）中的指定位置offer开始的length个字节写入输出流|
void close() throws IOException|关闭流释放内存资源|
void flush() throws IOException|将输出流中缓冲的数据全部写出目的地|

#### Reader
- 继承自Reader的流都是用于向程序中输入数据，且数据的单位为字符（16bit）：
    - 节点流
        - CharArrayReader
        - PipedReader
        - StringReader
    - 处理流
        - BufferedReader
        - InputSteamReader（他的子类FileReader是节点流）
        - FilterReader

```
graph LR
Reader-->BufferedReader
Reader-->CharArrayReader
Reader-->InputStreamReader
Reader-->FilterReader
Reader-->PipedReader
Reader-->StringReader
BufferedReader-->LineNumberReader
InputStreamReader-->FileReader
FilterReader-->PushbackReader
```
###### Reader的基本语法
语法|意义|
--|--|
int read() throws IOException|读取一个字符并以整数形式返回（0~~255），如果返回-1已到输入流的末尾|
int read(byte[] buffer) throws IOException|读取一系列字符并存储到一个数组buffer，返回实际读取字符数，如果读取前已到输入流的末尾则返回-1|
int read(byte[] buffer,int offer,int length) throws IOException|读取length个字符，并存储在buffer，从offer开始读取。返回实际读取的字符数，如果读取带输入流末尾则返回-1|
void close() throws IOException|关闭流释放内存资源|


#### Writer
- 继承自Writer的流都是用于程序中输出数据，且数据的单位为字符（16bit）：
    - 节点流
        - CharArrayWriter
        - PipedWriter
        - StringWriter
    - 处理流
        - BufferedWriter
        - OutputStreaWriter（其子类FileWrite属于节点流）
        - FilterWriter
```
graph LR
Writer-->BufferedWriter
Writer-->CharArrayWriter
Writer-->OutputStreamWriter
Writer-->FilterWriter
Writer-->PipedWriter
Writer-->StringWriter
OutputStreamWriter-->FileWriter
```
###### Writer的基本语法
语法|意义|
--|--|
int write(int c) throws IOException|向输出流写入应该字符数据，该字节数据为参数b的低16位。|
int write(byte[] cbuf) throws IOException|将一个字符类型的数组中的数据写入输出流|
int write(byte[] cbuf,int offer,int length) throws IOException|将一个字节类型的数组（buffer）中的指定位置offer开始的length个字节写入输出流|
void write(String string) throws IOException|将一个字符串中的字符写入输出流|
void write(String string,int offer,int length) throws IOException|将一个字符串从offer开始的length个字符写入到输出流|
void close() throws IOException|关闭流释放内存资源|
void flush() throws IOException|将输出流中缓冲的数据全部写出目的地|

### 节点流类型
类型|字符流|字节流|
--|--|--|
File（文件）|FileReader  FileWriter|FileInputStream  FileOutputStream|
Memory Array|CharArrayReader  CharArrayWriter|ByteArrayInputStream  ByteArrayOutputStream|
Memory String|StringReader  StringWriter||
Pipe（管道）|PipedReader  PipedWriter|PipedInputStream  PipedOutputStream|

##### FileInputStream和FileOutputStream的用法
```java
public static void main(String[] args) {
        try {
            int b = 0;
            FileInputStream in = null;
            FileOutputStream out = null;
            in = new FileInputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test.txt");
            out = new FileOutputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test01.txt");
            while((b = in.read()) != -1) {
                System.out.println((char)b);
                out.write(b);
            }
            in.close();
            out.close();
        } catch (FileNotFoundException e) {
            System.out.println("找不到");
        } catch (IOException e) {
            System.out.println("文件错误");
        }
        System.out.println("结束");
    }
```

##### FileReader的用法
```java
public static void main(String[] args) {
        try {
            FileReader fr = null;
            int c = 0;
            fr = new FileReader("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test.txt");
            int in = 0;
            while((c = fr.read()) != -1) {
                System.out.println((char) c);
            }
            fr.close();
        } catch (FileNotFoundException e) {
            System.out.println("找不到路径");
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("读取错误");
        }
    }
```

##### FileWriter的用法
```java
public static void main(String[] args) {
        FileWriter fw = null;
        try {
            fw = new FileWriter("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test.txt");
            //文件中的乱码是各个国家的语言
            for (int i = 0;i<5000;i++){
                fw.write(i);
            }
            fw.close();
        } catch (FileNotFoundException e) {
            System.out.println("找不到文件");
        } catch (IOException e) {
            System.out.println("出错");
        }
    }
```
> 如果使用FileInputStream 文件中输出乱码，原因是字节流只会输出1个字节而中文需要两个字节
> FileOutputStream和FileWriter：如果不存在则会创建一个新的文件

### 处理流类型
处理类型|字符流|字节流|
--|--|--|
Buffering|BufferedReader   BufferedWriter|BufferedInputStream   BufferedOutputStream|
Filtering|FilterReader  FilterWriter|FilterInputStream  FiletrOutputStream|
Converting between bytes and character|InputStreamReader  OutputStreamWriter||
Object Serialization||ObjectInputStream  ObjectOutputStream|
Data Conversion||DataInputStream  DataOutputStream|
Counting|LineNumberReader|LineNumberInputStream|
Peeking ahead|PushbackReader|PushbackInputStream|
Printing|PrintWriter|PrintStream|

#### 缓冲流
- 缓冲流要“套接”在相应的节点流之上，对读写的数据提供了缓冲功能，提高了读写的效率，同时增加了一些新的方法。
- J2SDK提供了四种缓冲流。
- 缓冲输入流支持其父类的mark和reset方法。
- BufferedReader。 提供了readLine方法用于读取一行字符串（以\r和\n分隔）
- BufferedWriter提供了newLine用于写入一个行分隔符。
- 对于输出的缓冲流，写出的数据会先在内存种缓存，使用flush方法将会使内存中的数据立刻写出。

```java
public static void main(String[] args) {
        try {
            FileInputStream fis = new FileInputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test01.txt");
            BufferedInputStream bis = new BufferedInputStream(fis);
            int c = 0;
            System.out.println(bis.read());
            System.out.println(bis.read());
            //标记此输入流中的当前位置
            bis.mark(0);
            for (int i = 0;i<10 && (c=bis.read())!=-1;i++) {
                System.out.println((char)c+" ");
            }
            System.out.println();
            //重新定位该流在时间的 mark方法的位置上呼吁这个输入流
            bis.reset();
            for (int i = 0;i<=10 && (c=bis.read())!=-1;i++) {
                System.out.println((char)c+" ");
            }
            bis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
```java
public static void main(String[] args) {
        try {
            BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\text.txt"));
            BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\text02.txt"));
            String s= null;
            for (int i = 1;i<=100;i++) {
                s = String.valueOf(Math.random());
                bw.write(s);
                bw.newLine();
            }
            bw.flush();
            while ((s = br.readLine()) != null) {
                System.out.println(s);
            }
            bw.close();
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

#### 转换流
- InputStreamReader 和 OutputStreamWriter 用于字节数据到字符数据之间的转换。
- InputStreamReader 需要和 InputStream “套接”。
- OutputStreamWriter 需要和 OutputStream “套接”。
- 转换流在构造方法中指定其编码集合。
```java
public static void main(String[] args) {
        try {
            InputStreamReader isr = new InputStreamReader(System.in);
            //使用可以读行的方法
            BufferedReader br = new BufferedReader(isr);
            String s= null;
            //读一行字符串
            s = br.readLine();
            while (s!=null) {
                if (s.equalsIgnoreCase("exit")) break;
                System.out.println(s.toUpperCase());
                s = br.readLine();
            }
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
```java
public static void main(String[] args) {
        try {
            OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test.txt"));
            //写入一个字符串
            osw.write("xzj is not good");
            //返回此类输入流的编码名称
            System.out.println(osw.getEncoding());
            //关闭输出流
            osw.close();
            //后面加true 字符串会接着往下添加
            osw = new OutputStreamWriter(new FileOutputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test.txt",true),"ISO8859_1");
            osw.write("asd");
            System.out.println(osw.getEncoding());
            osw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

#### 数据流
- DataInputStream 和 DataOutputStream 分别继承自InputStream 和 OutputStream，它属于处理流，需要套接在InputStream 和 OutputStream类型的节点上。
- DataInputStream 和DataOutputStream提供了可以存取与机器无关的Java原始类型数据（int，Double）的方法。
```java
public static void main(String[] args) {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        DataOutputStream dos = new DataOutputStream(baos);
        try {
            dos.writeBoolean(true);
            dos.writeDouble(2.024455);
            //这里的toByteArray未理解
            ByteArrayInputStream bais = new ByteArrayInputStream(baos.toByteArray());
            System.out.println(bais.available());
            DataInputStream dis = new DataInputStream(bais);
            System.out.println(dis.readBoolean());
            System.out.println(dis.readDouble());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
> 必须按照数据的输出顺序来进行输入（先写先读）

#### 打印流（print流）
- PrintWriter和PrintStream 都属于输出流，分别针对字符和字节。
- PrintWriter和PrintStream提供了重载的print。
- Println方法用于多种数据类型的输出。
- PrintWriter和PrintStream的输出操作不会抛出异常，用户通过检测错误状态获取错误信息。
- PrintWriter和PrintStream有自动的`flush()`方法
```java
public static void main(String[] args) {
        try {
            String s = null;
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            FileWriter fw = new FileWriter("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test.txt",true);
            PrintWriter ps = new PrintWriter(fw);
            while((s = br.readLine()) != null) {
                if (s.equalsIgnoreCase("exit")) break;;
                System.out.println(s.toUpperCase());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

#### Object流
- 直接将Object写入或读出。
```java
public static void main(String[] args) {
        T t = new T();
        t.i = 100;
        T t1 = null;
        try {
            FileOutputStream fos = new FileOutputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test01.txt");
            ObjectOutputStream oos = new ObjectOutputStream(fos);
            oos.writeObject(t);
            oos.flush();
            oos.close();

            FileInputStream fis = new FileInputStream("C:\\Users\\Administrator\\Desktop\\文档图片文件夹\\test01.txt");
            ObjectInputStream ois = new ObjectInputStream(fis);
            t1 = (T) ois.readObject();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        System.out.println(t1.d+" "+t1.i);
    }
}
class T implements Serializable {
    int i = 0;
    double d = 2.3;
}
```