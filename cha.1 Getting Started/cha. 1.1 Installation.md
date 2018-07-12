## 安装

    第一步当然是安装Rust。我们将通过rustup来安装。rustup是管理Rust版本及其相应工具的命令行工具。下载需要能访问互联网。
    
    书中的例子是基于Rust 1.21.0。Rust的稳定性确保书中所有的例子能够在最新的Rust版本上编译。各版本之间的输出结果可能会不一样，因为Rust经常会改进错误消息和警告。
    
    命令行记号
    
    美元符号$表示每条命令的开始。不需要输入$。很多教程约定:$作为普通用户权限运行，#以管理员权限运行。不是以美元符号$开始的行一般显示前一个命令的输出结果。此外，PowerShell使用>作为命令的开始，而不是$。
    
## 在linux或者macOS上安装Rustup

如果你是用Linux或者macOS，那么开一个终端并输入下面的命令：

    $ curl https://sh.rustup.rs -sSF | sh

该命令会下载一个shell脚本并开始安装rustup工具，该工具会安装Rust最新的稳定版本。可能会提示你输入密码。如果安装顺利，会出现下面的信息：

    Rust is installed now. Great!
    
当然，如果你对使用curl URL | sh安装软件持怀疑态度，那么你可以下载，检查，并按自己的喜好运行脚本。

安装脚本会自动地添加Rust到系统的PATH变量中。如果你希望立马使用Rust而不是重启终端，在shell中运行下面的命令会将Rust添加到系统PATH中：

    $ source $HOME/.cargo/env

或者，你可以将下面的信息添加到～/.bash_profile文件中：

    $ export PATH="$HOME/.cargo/bin:$PATH"
    
此外，你需要一个链接器（linker）。有可能你的平台上已经安装了，但当你编译一个Rust程序并得到显示linker不能执行的错误时，你就得安装一个了。你可以安装C编译器，因为通常都会自带正确的linker。如何安装C编译器，可以查找对应操作系统平台的文档。一些常见的Rust包依赖于C，因此也需要一个C编译器。无论如何，安装一个C编译器都是值得的。

我用的是macOS，在安装的时候选择1。我安装成功后的rust版本是：

    ➜  ~ rustc -V
    rustc 1.27.1 (5f2b325f6 2018-07-07)
这是rust团队发布的最新的稳定版本。默认的安装目录是$HOME/.cargo/bin。


## 在Windows上安装Rustup
todo
## 不使用rustup，自定义安装

由于某些原因，如果你偏好不使用rustup，请前往[Rust的安装页面](https://www.rust-lang.org/zh-CN/install.html)寻求其他安装选项。

## 升级和卸载

通过rustup安装好Rust后，升级到最新的版本很简单。在你的shell中，运行如下的更新脚本：

    $ rustup update
要想卸载Rust和rustup，在shell中运行下面的卸载脚本：
    
    $ rustup self uinstall

## 故障排除(troubleshooting)

为了检查是否正确安装Rust，开一个shell并输入这一行：
    
    $ rustc --version
你应该可以看见最新稳定版的版本号，提交哈希以及提交日期。具体的格式如下：

    $ rustc x.y.z (abcabcabc yyyy-mm-dd)
如果你能看见这条信息，恭喜你Rust安装成功。如果你不能看见这条信息且用的是Windows，检查Rust是否在%PATH%系统变量中。如果这些都没错并且Rust仍然不能正常工作，你可以在很多地方得到帮助。
最简单的方式是Rust IRC 频道，你可以通过Mibbit访问它。其他非常棒的资源包括用户论坛和Stack Overflow。

## 本地文档

安装程序会在本地包含一份文档，因此你可以离线阅读。运行rustup doc会在浏览器中打开本地文档【亲测有效】。

你在任何时候不确定标准库中提供的类型或者函数是做什么的或者不清楚它的用法时，使用应用程序接口（API）文档来查看。






