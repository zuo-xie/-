### File

1. `Java.io.File`类代表文件名（路径和文件名）。
2. File类的常见构造方法：
    1. `public File(String pathname)`
        以pathname为路径创建File对象，如果pathname是相对路径，则默认的当前路径在系统属性user.dir中存储。
    2. `public File(String parent,String child)`
        以parent为父路径，child为子路径创建File对象。
3. File的静态属性`String separator`存储了当前系统的路径分隔符。

#### File 类的常用方法

方法名字 | 中文 | 相应属性
--|--|--
canRead()| 测试应用程序是否可执行文件的路径名表示的抽象 ==（文件是否可使用）== ||
 CanWrite()| 检查应用程序是否可以修改文件的抽象路径名记 ==（文件是否可以修改）== |
 CanRead()| 检查应用程序是否可以读取文件的抽象路径名记 ==（文件是否可以读取）==|
 exists()|检查文件或目录是否存在这种抽象路径名记 ==（文件是否存在）== |
 mkdirs()| 创建该目录下的抽象路径名命名，包括任何必要的但不存在父目录 ==（）== |
