## 世界，您好！

现在我们已经安装好Rust了，开始写我们的第一个程序。在学习一门新语言的时候写一个小程序将"Hello,World!"输出到屏幕是一种传统。因此，我们也不免俗。

    注意：本书假设读者对命令行有基本的熟悉。Rust不会对你编写，用的工具，或者代码位置做任何特定的要求，因此如果你偏向使用
    IDE，而不是命令行，理直气壮地用最爱地IDE都是可以的。很多IDE已经对Rust提供了不同程度的支持。具体细节需要查看IDE的文档。
    近期，Rust团队一直在关注实现非常棒的IDE支持，并且已经取得了进展。
    
## 创建一个项目目录
首先创建一个目录存放Rust代码。Rust并不关心你的代码存在何处。但是本书为了练习和项目，我们建议在主目录下创建一个项目目录，然后将所有的项目存到那里。

开一个终端，输入下面的命令来创建一个项目目录以及在项目目录下创建一个"Hello,World!"目录。

对于Linux和macOS，输入：

    $ mkdir ~/projects
    $ cd ~/projects
    $ mkdir hello_world
    $ cd hello_world
对于Windows CMD，输入：
    
    > mkdir "%USERPROFILE%\projects"
    > cd /d "%USERPROFILE%\projects"
    > mkdir hello_world
    > cd hello_world
对于Windows PowerShell，输入：

    > mkdir $env:USERPROFILE\projects
    > cd $env:USERPROFILE\projects
    > mkdir hello_world
    > cd hello_world
## 编写并运行一个Rust程序
接下来，创建一个新的源文件，我们给其命名为main.rs。Rust文件总是以.rs后缀结尾。如果文件名超过一个单词，使用下划线来分割它们。例如，使用hello_world.rs而不是
helloworld.rs。

现在打开刚刚创建的main.rs文件，然后输入清单1-1的代码。

文件名：main.rs

    fn main() {
        println!("Hello, world!");
    }

    //output
    Hello,world!
清单1-1：打印"Hello,world!"的程序

保存文件，回到终端窗口。在Linux或者macOS上，输入下面的命令进行编译以及运行（二进制）文件：

    $ rustc main.rs
    $ ./main
    Hello,world!
在Windows上，输入命令./main.exe而不是./main。
    
    > rustc main.rs
    > .\main.exe
    Hello,world!
不管你的操作系统是什么，字符串Hello,world!都应该打印到终端。如果你没有看到输出，回到"故障排查"章节寻求帮助的途径。

如果Hello,world!确实打印出来了，恭喜你！你已经正式完成了第一个Rust程序。这令你成为一名Rust程序员了！欢迎你！

## 剖析一个Rust程序
让我们仔细回顾一下"Hello,world!"程序刚刚发生了什么。这是首个疑惑点：

    fn main() {
    
    }
在Rust中，这几行定义了一个函数。main函数很特殊：在每一个可执行的Rust程序中，它总是第一执行的代码。第一行声明了一个函数名
为main，不带任何参数和返回值的函数。如果这里有参数，它们也只能位于括弧(和)中。

还有，注意到函数体被包裹在波形括号{和}中。Rust需要这些花括弧围绕所有的函数体。将{置于函数声明的同一行，在二者之间添加一个空格，这是
不错的编码风格。

在写作之际，一个被称作rustfmt的自动格式化工具正处于开发之中。如果你想在所有的Rust项目中坚持一种标准编码风格，rustfmt将以一种
特殊的方式格式化你的代码。Rust团队计划最终将其纳入标准的Rust发行版中，像rustc一样。因此，取决于你何时读到这本书，它可能已经被安装在
你的计算机上面了！更多细节请检查在线文档。

    笔者在学习这本书时，Rust团队已经将rustfmt纳入发行版了。下面是安装目录下面的工具：
    ➜  hello_world cd ~/.cargo/bin
    ➜  bin ls
    cargo     rls       rust-lldb rustdoc   rustup
    cargo-fmt rust-gdb  rustc     rustfmt
下面的代码在main函数中：
    
    println!("Hello,world!");
在这个小程序中，这一行做了所有的工作：它将文本打印到屏幕。这里有四个重要的细节值得注意。首先，Rust风格是缩进4个空格，而不是一个tab。

第二，println是一种Rust 宏。相反，如果它调用了一个函数，它将被输入为println（没有！）。我们将在附录D中更详细地讨论Rust宏。现在，你只需要知道，
使用！意味着你正在调用一个宏，而不是一个标准的（normal）函数。

第三，你看见"Hello,world!"字符串。我们将该字符串作为一种参数传给println!，然后字符串被打印到屏幕。

第四，我们用分号;结尾，这预示着该表达式结束了，而且下一个表达式马上开始。大多数Rust代码行都以分号结尾（？什么时候不呢？）。

## 编译和运行是分离的

你刚刚运行了创建的程序，因此让我们检查这个过程中的每一步。

在运行一个Rust程序之前，你必须使用Rust编译器将其编译，这是通过输入rustc命令以及给该命令传入源文件名实现的，就像这样：
    
    $ rustc main.rs
如果你有C/C++的知识背景，你将会注意到，这类似gcc或者clang。编译成功后，Rust会输出一个二进制可执行文件。

在Linux，macOS以及Windows上的PowerShell上，你可以在shell上输入ls命令来查看可执行文件，具体如下：

    $ ls
    main main.rs
在带CMD的Windows中，你可以输入以下的命令：
    
    $ dir /B %= the /B option says to only show the file names =%
    main.exe
    main.pbd
    main.rs
这显示源代码是以.rs作为后缀的，可执行文件（Windows上是main.exe，但在所有其他平台上是main），而且在使用CMD时，包含
调试信息的文件以.pbd作为后缀。在这里，你运行main或者main.exe，像这样：
    
    $ ./main # or .\main.exe on Windows
如果main.rs是你的"Hello,world!"程序，这一行将打印Hello,world!到终端上。

如果更熟悉一门动态语言，例如Ruby，Python，或者JavaScript，你可能不习惯于编译和运行一个程序在分离的步骤中完成。Rust是提前编译型语言。
这意味着你可以编译一个程序，将可执行文件给别人，他们甚至可以在不安装Rust就可以运行它。如果你给别人一个.rb,.py或者.js文件，他们需要安装对应的
Ruby，Python和JavaScript实现。但是在这些语言中，你只要一条命令来实现编译和运行你的程序。在语言设计中，一切都是平衡。

对简单的程序，仅仅用rustc来做编译是可以的，但随着项目变大，你想要管理所有的选项以及令其易于共享代码。接下来，我们将向你介绍Cargo工具，这会有助于你编写
真实世界的Rust程序。
