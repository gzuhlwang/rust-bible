# 变量和可修改性（mutability）

默认，变量是不可修改的（immutable）。这是Rust提供给程序员采用Rust提供的安全性和简单并发编写编写代码的众多说服力之一。

但是，你仍然可以让变量变得可修改（mutable）。

当一个变量是不可变的，一旦值和一个变量名绑定，你就不能修改那个值。为了示范，我们使用cargo new --bin variables在projects目录下创建一个新项目variables。

接着，在新的variables目录中，打开src/main.rs并且用下面的代码（还未编译）替换其中的代码：

文件名：src/main.rs

    fn main(){
    
        let x = 5;
        println!("The value of x is:{}",x);
        x=6;
        println!("The value of x is:{}",x);
    }

保存并运行（使用cargo run）。你应该会接收到一个如下的错误消息：

    error[E0384]: cannot assign twice to immutable variable `x`
     --> src/main.rs:5:9
      |
    3 |         let x = 5;
      |             - first assignment to `x`
    4 |         println!("The value of x is:{}",x);
    5 |         x=6;
      |         ^^^ cannot assign twice to immutable variable


本例子说明编译器是如何帮你寻找程序中的错误的。尽管编译错误很令人沮丧，但他们只说明你的程序还不能安全地做你想要它完成的功能。他们不能说明你不是一个好的程序员！
经验丰富的Rustaceans照样有犯编译错误。

错误信息显示，错误的原因是你**不能给不可修改的变量x分配两次**。因为你试图给一个不可修改的x变量分配第二个值。

当我们尝试改变一个值，而我们将前期其前指明为不可修改，我们就会得到编译时错误。因为这中情况会导致bug。

在Rust中，编译器会确保，当你声明一个值不能改变，它就真的不会改变。这意味着在你阅读和写代码时，你不必追踪一个值可能在哪儿以及如何改变的。因此，你的代码会很容易推理。

但可修改性非常有用。变量只是在默认情况是不可修改的。正如你在第二章中所做的那样，你可以通过在变量名前面添加mut来令它们变得可修改。除了允许该值是可改变的，mut给代码的未来阅读者传达一种意图，即
代码的其他部分将改变这个变量的值。

例如，让我们将src/main.rs中的代码改变成如下：

文件名:src/main.rs

    fn main(){
        
            let mut x = 5;
            println!("The value of x is:{}",x);
            x=6;
            println!("The value of x is:{}",x);
    }
    
当我们现在运行该程序，我们会得到:

    ➜  variables git:(master) ✗ cargo run
       Compiling variables v0.1.0 (file:///Users/data/projects/variables)
        Finished dev [unoptimized + debuginfo] target(s) in 1.65s
         Running `target/debug/variables`
    The value of x is:5
    The value of x is:6
    
当使用mut时，我们允许将x从5改变成6。在一些场景中，你希望一个变量是可修改的，因为这会让代码更方便编写，相较于它只有不可修改的变量。


除了防止bug，有很多trade-offs需要考虑。
# 变量和常量的区别

不能改变一个变量的值可能会让你想起大多数程序设计语言都有的另一个程序设计概念：常量。和不可修改的变量类似，常量是和一个变量名绑定的值，也不允许修改。但常量和变量（这里主要值不可修改的变量）还是有一些差异的。

首先，不允许mut和常量使用。常量默认就是——它们总是不可修改的。

声明常量使用的是const关键字，而不是let关键字，并且值的类型必须标注。我们将要在下一节"数据类型"中涉及类型和类型记号。
因此现在不要担心细节。只需要知道你必须注明类型。

可以在任何范围内声明常量，包括全局范围，这会使它们在代码中的其他部分需要知道它们的值时非常有用。

最后一个区别，常量只能被设置成一个常量表达式，而不能是一个函数调用或在运行时才能被计算出的任何其他值。

这里有一个常量声明的例子，其中常量名是MAX_POINTS且其值被置为100000。（对常数而言，Rust的命名约定是使用大写字母，在单词之间用下划线）：

    const MAX_POINTS:u32 = 100000;

对于程序运行的全生命，常量都是有效的。

# Shadowing

你可以用先前的变量名声明一个新的变量。新变量会遮蔽（shadow）上一个变量。Rustaceans常说，第二个变量遮蔽了第一个变量，这意味着第二个变量的值是使用该
变量的时候所显示的。我们通过使用相同的变量名以及重复使用let关键字来遮蔽一个变量，具体如下：

文件名：src/main.rs

    fn main(){
        let x=5;
        
        let x=x+1;
        
        let x=x*2;
        
        println!("The value of x is:{}",x);
    }
本程序首先给x绑定一个值5。接着通过重复let x=来遮蔽x，接收初始值并加1，因此x的值变成6。第三格let语句也遮蔽了x，给上一个值乘以2，最终x的值是12。
当我们运行程序时，它会输出下面的：

    ➜  variables git:(master) ✗ cargo run
       Compiling variables v0.1.0 (file:///Users/data/projects/variables)
        Finished dev [unoptimized + debuginfo] target(s) in 0.35s
         Running `target/debug/variables`
    The value of x is:12

遮蔽不同于将一个变量标记为mut，因为如果我们试图故意给一个未使用let关键字的变量重新分配一个值，会出现编译错误【因为变量默认是不可修改的】。
通过使用let，我们可以完成对一个值的一些转换，但完成这些转换之后，变量就不可修改了【如果要修改，还得在变量名前面添加mut关键字】。

mut和遮蔽的另一个不同之处是，因为使用let关键字，我们高效地创建了一个新的变量。我们可以改变值的类型但复用相同的名字。
例如，我们的程序要求用户显示在输入空格字符的时候，但我们真实想要将输入存为一个数：

    let spaces = "  ";
    let spaces = spaces.len();

本结构是允许的，因为第一个spaces变量是一个字符串类型，第二个spaces变量是一个全新的变量，碰巧和第一个同名。因此，遮蔽使我们免于提出不同的名字，
例如space_str和space_num。相反，我们可以复用更简单的spaces名字。但是，如果我们试图为这而使用mut，我们将得到编译错误：

    let mut spaces="    ";
    spaces = spaces.len();
错误显示不允许我们改变一个变量的类型：

    error[E0308]: mismatched types
     --> src/main.rs:9:9
      |
    9 |     spaces=spaces.len();
      |            ^^^^^^^^^^^^ expected &str, found usize
      |
      = note: expected type `&str`
                 found type `usize`

【注】9代表错误的代码行！

现在我们已经探寻了变量的工作方式，让我们看看更多的数据类型。