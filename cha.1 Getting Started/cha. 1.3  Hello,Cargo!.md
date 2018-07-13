## Cargo,你好！
Cargo是Rust的构建系统和包管理器。大多数Rustacenas使用此工具管理他们的Rust项目，因为Cargo为你做了很多工作，例如构建代码，下载代码依赖的库，以及构建这些库。（我们称代码需要的库为依赖）

最简单的Rust程序，就像到目前为止我们写的"Hello,world!"程序，不需要任何依赖。因此，如果我们用Gargo构建"Hello,world!"项目，这只会
使用Cargo构建代码的功能。随着你编写更复杂的Rust程序，你将添加依赖，因此如果你使用Cargo创建一个项目，添加依赖将变得比较简单。

因为大多数Rust程序都使用Cargo，本书的剩下部分假设你也使用Cargo。如果你是使用官方的安装程序，我们在"安装"章节讨论过，Cargo会自带被安装。如果你安装Rust是通过
其他方式，在你的终端上输入下面的命令检查Cargo是否安装。

    $ cargo --version
如果你看到版本号，你有Cargo了。如果你看见一条错误信息，例如，command not found。查看一下安装文档以确定如何单独安装Cargo。

## 用Cargo创建一个项目
让我们使用Cargo创建一个新的项目并看看这与原始的"Hello,world!"项目有何不同。回到你的项目目录（或者任何你决定存放代码的地方）。然后，不管是什么操作系统，运行下面的命令：

    $ cargo new hello_cargo --bin
    $ cd hello_cargo
第一条命令创建了一个新的二进制可执行文件，称做hello_cargo。传给cargo new的--bin参数会创建一个可执行的应用（通常称做二进制），而不是一个库。
我们已经给项目取名为hello_cargo，并且Cargo会在同名目录下创建文件。

进入到hello_cargo目录，并列出所有的文件。你将看到，Cargo已经为我们创建好了2个文件和一个目录。它们是一个Cargo.toml文件和
位于src目录的main.rs文件。Cargo已经初始化好了一个新的Git仓库，连同一个.gitignore文件。

    ➜  projects cargo new hello_cargo --bin
         Created binary (application) `hello_cargo` project
    ➜  projects ls
    hello_cargo hello_world
    ➜  projects tree
    .
    ├── hello_cargo
    │   ├── Cargo.toml
    │   └── src
    │       └── main.rs
    └── hello_world
        ├── main
        └── main.rs
    
    3 directories, 4 files

    注意到：Git是常见的版本控制系统。你可以通过使用--vcs标志来改变cargo new使用一个不一样的版本控制系统或者不要版本控制系统。运行cargo new --help查看可用的选项。

用编辑器打开Cargo.toml。内容应该和清单1-2中的代码类似。

    文件名:Cargo.toml
    [package]
    name = "hello_cargo"
    version = "0.1.0"
    authors = ["gzuhlwang <2277581700@qq.com>"]
    
    [dependencies]
清单1-2：cargo new生成的Cargo.toml文件的内容

此文件是TOML格式，这是Cargo的配置格式。

第一行，[package],是章节开头，显示接下来的语句是配置一个包。随着我们向此文件添加更多的信息，我们将添加其他的章节（section）。

接下来的三行设置Cargo需要用于编译程序的配置信息：程序名称，版本以及作者。Cargo从你的计算机上获得你的姓名和邮件信息，因此如果信息不正确，现在可以
修改信息，然后保存。

最后一行，[dependencies],是一个章节的开始，用于罗列项目依赖。在Rust中，代码包被称为crate。对本项目，我们不需要任何其他的crate。
但我们将在第二章的第一个项目中使用依赖部分。

现在打开src/main.rs，看一看：

    文件名：src/main.rs
    fn main() {
        println!("Hello, world!");
    }
Cargo已经帮我们生成了"Hello,world!"程序，正如我们在清单1-1中编写的那个程序。到目前为止，我们上一个项目和Cargo生成的项目的区别是：
Cargo将代码放在的src目录里面以及在最高目录中有了配置文件Cargo.toml。

Cargo期待你的源文件位于src目录里。顶层项目目录只有README文件，许可信息，配置信息以及任何与代码不相关的一切。使用Cargo有助你组织你的项目。
There's a place for everything, and everything is in its place.

如果你创建好了一个项目，但不是使用Cargo，正如我们在Hello,world!项目中做的哪样，你可以将转换为一个使用了Cargo的项目。将项目代码移到src目录
并创建一个合适的Cargo.toml文件。


## 构建和运行一个Cargo项目
现在，我们来看看用Cargo构建和运行"Hello,world!"程序的区别。在hello_cargo目录下输入下面的命令构建你的项目：

    $ cargo build
       Compiling hello_cargo v0.1.0 (file:///Users/data/projects/hello_cargo)
        Finished dev [unoptimized + debuginfo] target(s) in 1.75s
这条命令创建了一个可执行文件target/debug/hello_cargo(或者在Windows上是target\debug\hello_cargo.exe)，而不是在你当前目录。
你可以用下面的命令运行该可执行文件：

    $ ./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows
    Hello,world!
如果一切顺利，Hello,world!应该打印到终端。首次运行cargo build也会致使Cargo在顶层目录创建一个新的文件Cargo.lock。该文件
会追踪项目中真实的依赖版本。本项目没有依赖，因此文件比较稀疏。你将永远不需要手动改变此文件。Cargo会为你管理其内容。

本机运行：
    ➜  hello_cargo git:(master) ✗ ls
    Cargo.lock Cargo.toml src        target
    ➜  hello_cargo git:(master) ✗ cat Cargo.lock
    [[package]]
    name = "hello_cargo"
    version = "0.1.0"

我们只用cargo build构建了一个项目并用./target/debug/hello_cargo运行，但是我们也可以使用cargo run在一个命令中编译代码并运行生成的
可执行文件。

    $ cargo run
        Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
         Running `target/debug/hello_cargo`
    Hello, world!
//本机
    
    ➜  hello_cargo git:(master) ✗ cargo run
        Finished dev [unoptimized + debuginfo] target(s) in 0.07s
         Running `target/debug/hello_cargo`
    Hello, world!

注意到：本次我们没有看到输出结果中显示Cargo正在编译hello_cargo的信息。Cargo清楚文件没有发生改变，因此它只会运行二进制文件。如果你修改了
源文件，Cargo将会在运行之前再次构建项目，因此你会看到下面的输出：
    
    ➜  hello_cargo git:(master) ✗ cargo run
       Compiling hello_cargo v0.1.0 (file:///Users/data/projects/hello_cargo)
        Finished dev [unoptimized + debuginfo] target(s) in 1.40s
         Running `target/debug/hello_cargo`
    Hello, world!

Cargo也提供了一个命令，即cargo check。这个命令会快速地检查你的代码以保证能编译但不会产生一个可执行文件：

    ➜  hello_cargo git:(master) ✗ cargo check
        Checking hello_cargo v0.1.0 (file:///Users/data/projects/hello_cargo)
        Finished dev [unoptimized + debuginfo] target(s) in 0.72s

为什么你会不想要一个可执行文件呢？通常，cargo check比cargo build更快。因为它跳过了产生可执行文件的步骤。如果你在编写代码的同时一直在检查你的工作，
使用cargo check将加速该过程。就其本身而言，很多Rustacean定期运行cargo check，因为他们需要确保编写程序能够编译。接着他们运行cargo build，当他们准备使用可执行程序时。

总结一下到目前为止我们学习的有关Cargo的内容：
    
    我们可以使用cargo build或者cargo check来构建一个项目
    我们可以使用cargo run来一次性地完成构建和运行
    构建结果不再和源码保存在一样的目录，Cargo将其存放在target/debug目录。  
    
使用Cargo的一个附加好处是：不管你在用哪一个操作系统，命令都是一样的。因此，就此而言，我们不再为Linux和macOS相对的Windows提供特定的指令。
## 为发布而构建（Building for Release）

当你的项目最终准备发布时，你可以使用cargo build --release优化编译。这条命令在target/release下将创建一个可执行文件，而不是
在target/debug。优化将令你的Rust代码运行地更快，但延长了编译程序的时间。这就是为什么有两个不同的profile的原因：一个用于开发，另一个用于构建最终的程序。
如果你想要测代码的运行时间，务必运行cargo build --release并且用target/release中的可执行文件来做benchmark。

## 有关Cargo的一些约定

简单的项目，Cargo不能提供超过仅仅使用rustc的巨大价值，但随着你的程序变得愈发错综复杂，Cargo会证明自身的价值之处。复杂的项目由多个crate构成，令Cargo来
协调构建更加简单。

纵然hello_cargo项目非常简单，它也使用了你将在Rust职业生涯中使用的大量真实工具。事实上，为了在已有的项目上工作，你可以用以下
的命令来检查使用Git的代码，换到项目目录，并构建：
    
    $ git clone someurl.com/someproject
    $ cd someproject
    $ cargo build

有关Cargo的更多信息，请查看你文档。
## 本章小结

你已经开启非常棒的Rust之旅的开局！ 本章，你学习了如何：

    使用rustup安装Rust的最新稳定版
    更新到更新的Rust版本
    本地打开安装的文档
    编写并直接使用rustc运行一个"Hello,world!"程序
    使用Cargo的约定创建并运行一个新项目
todo

因此，下一章，我们将构建一个guessing游戏程序。如果你想通过学习Rust中常见的编程概念是怎么工作来开始，看第三章，然后再回到第二章。