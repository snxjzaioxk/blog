---
layout: post
title: "python速成"
lesson: 3
category: 教程
---

- 关于 Python     Python 的优点    学习 Python 的注意事项
- 环境搭建     一些平台提供的 Python 版本
- 使用 pip 安装第三方库
- 基本语法     注释    基本数据类型     一切皆对象    数字运算    数据类型判断    基本输入输出    字符串    创建数组     使用 list    使用 NumPy    使用 array    输入输出     格式化输出    split() 函数    文件读写    控制流程     循环结构    选择结构    异常处理    内置容器    编写函数     默认参数    类型标注
- 装饰器
- 常用内置库
- 从例题对比 C++ 与 Python     声明常量    声明前向星结构体和其它变量    Dijkstra 算法    主函数    完整代码
- 参考文档
- 参考资料和注释

- Python 是一门 解释型 语言：Python 不需要编译和链接，可以在一定程度上减少操作步骤。
- Python 是一门 交互式 语言：Python 解释器实现了交互式操作，可以直接在终端输入并执行指令。
- Python 易学易用：Python 提供了大量的数据结构，也支持开发大型程序。
- Python 兼容性强：Python 同时支持 Windows、macOS 和 Unix 操作系统。
- Python 实用性强：从简单的输入输出到科学计算甚至于大型 WEB 应用，都可以写出适合的 Python 程序。
- Python 程序简洁、易读：Python 代码通常比实现同种功能的其他语言的代码短。
- Python 支持拓展：Python 会开发 C 语言程序（即 CPython），支持把 Python 解释器和用 C 语言开发的应用链接，用 Python 扩展和控制该应用。

- 目前主要使用的 Python 版本是 Python 3.7 及以上的版本，Python 2 和 Python 3.6 及以前的 Python 3 已经 不被支持，但仍被一些老旧系统与代码所使用。本文将 介绍较新版本的 Python。如果遇到 Python 2 代码，可以尝试 2to3 程序将 Python 2 代码转换为 Python 3 代码。
- Python 的设计理念和语法结构 与一些其他语言的差异较大，隐藏了许多底层细节，所以呈现出实用而优雅的风格。
- Python 是高度动态的解释型语言，因此其 程序运行速度相对较慢，尤其在使用其内置的 for 循环语句时。在使用 Python 时，应尽量使用 filter、map 等内置函数，或使用 列表生成 语法的手段来提高程序性能。

- Windows：也可以在 Microsoft Store 中免费而快捷地获取 Python。
- macOS/Linux：通常情况下，大部分的 Linux 发行版中已经自带了 Python。如果只打算学习 Python 语法，并无其它开发需求，不必另外安装 Python。 注意 在一些默认安装（指使用软件包管理器安装）Python 的系统（如 Unix 系统）中，应在终端中运行 python3 打开 Python 3 解释器。1

- 传入的参数有 2 个：maxsize 和 typed，如果不传则 maxsize 的默认值为 128，typed 的默认值为 False。
- 其中 maxsize 参数表示的是 LRU 缓存的容量，即被装饰的方法的最大可缓存结果的数量。如果该参数值为 128，则表示被装饰方法最多可缓存 128 个返回结果；如果 maxsize 传入为 None 则表示可以缓存无限个结果。
- 如果 typed 设置为 True，不同类型的函数参数将被分别缓存，例如，f(3) 和 f(3.0) 会缓存两次。

1. Python Documentation
1. Python 官方中文教程
1. Learn Python3 In Y Minutes
1. Real Python Tutorials
1. 廖雪峰的 Python 教程
1. GeeksforGeeks: Python Tutorials

1. 2. Python 解释器—Python 3 文档 ↩
1. Unicode 指南—Python 3 文档 ↩

## Python 速成

## 关于 Python

Python 是一门已在世界上广泛使用的解释型语言。它提供了高效的高级数据结构，还能简单有效地面向对象编程，也可以在算法竞赛。

### Python 的优点

*   Python 是一门 **解释型** 语言：Python 不需要编译和链接，可以在一定程度上减少操作步骤。
*   Python 是一门 **交互式** 语言：Python 解释器实现了交互式操作，可以直接在终端输入并执行指令。
*   Python **易学易用**：Python 提供了大量的数据结构，也支持开发大型程序。
*   Python **兼容性强**：Python 同时支持 Windows、macOS 和 Unix 操作系统。
*   Python **实用性强**：从简单的输入输出到科学计算甚至于大型 WEB 应用，都可以写出适合的 Python 程序。
*   Python **程序简洁、易读**：Python 代码通常比实现同种功能的其他语言的代码短。
*   Python **支持拓展**：Python 会开发 C 语言程序（即 CPython），支持把 Python 解释器和用 C 语言开发的应用链接，用 Python 扩展和控制该应用。

### 学习 Python 的注意事项

*   目前主要使用的 Python 版本是 Python 3.7 及以上的版本，Python 2 和 Python 3.6 及以前的 Python 3 已经 [不被支持](https://devguide.python.org/versions/#unsupported-versions)，但仍被一些老旧系统与代码所使用。本文将 **介绍较新版本的 Python**。如果遇到 Python 2 代码，可以尝试 [`2to3`](https://docs.python.org/zh-cn/3/library/2to3.html) 程序将 Python 2 代码转换为 Python 3 代码。
*   Python 的设计理念和语法结构 **与一些其他语言的差异较大**，隐藏了许多底层细节，所以呈现出实用而优雅的风格。
*   Python 是高度动态的解释型语言，因此其 **程序运行速度相对较慢**，尤其在使用其内置的 `for` 循环语句时。在使用 Python 时，应尽量使用 `filter`、`map` 等内置函数，或使用 [列表生成](https://www.pythonforbeginners.com/basics/list-comprehensions-in-python) 语法的手段来提高程序性能。

## 环境搭建

参见 [Python 3](https://oi.wiki/tools/compiler/#python-3)。或者：

*   Windows：也可以在 Microsoft Store 中免费而快捷地获取 Python。
    
*   macOS/Linux：通常情况下，大部分的 Linux 发行版中已经自带了 Python。如果只打算学习 Python 语法，并无其它开发需求，不必另外安装 Python。
    
    注意
    
    在一些默认安装（指使用软件包管理器安装）Python 的系统（如 Unix 系统）中，应在终端中运行 `python3` 打开 Python 3 解释器。[1](https://oi.wiki/lang/python/#fn:ref1)
    

此外，也可以通过 venv、conda、Nix 等工具管理 Python 工具链和 Python 软件包，创建隔离的虚拟环境，避免出现依赖问题。

作为一种解释型语言，Python 的执行方式和 C++ 有所不同，这种差异在使用 IDE 编程时往往得不到体现，因此这里需要强调一下运行程序的不同方式。

当在命令行中键入 `python3` 或刚刚打开 IDLE 时，你实际进入了一种交互式的编程环境，也称「REPL」（「读取 - 求值 - 输出」循环），初学者可以在这里输入语句并立即看到结果，这让验证一些语法变得极为容易，我们也将在后文中大量使用这种形式。

但若要编写完整的程序，你最好还是新建一个文本文件（通常后缀为 `.py`），然后在命令行中执行 `python3 filename.py`，就能够运行代码看到结果了。

### 一些平台提供的 Python 版本

注意

本表格在本文撰写时（2025/01/15）时有效，建议前往相关平台重新查证。

目前国内关于 **源码** 的镜像缓存主要是 [北京交通大学自由与开源软件镜像站](https://mirror.bjtu.edu.cn/python/) 和 [华为开源镜像站](https://repo.huaweicloud.com/python/)，可以到那里尝试下载 Python 安装文件。

## 使用 `pip` 安装第三方库

Python 的生命力很大程度上来自于丰富的第三方库，编写一些实用程序时「调库」是常规操作，`pip` 是首选的安装第三方库的程序。自 Python 3.4 版本起，它被默认包含在 Python 二进制安装程序中。

`pip` 中的第三方库主要存储在 [Python 包索引（PyPI）](https://pypi.org/) 上，用户也可以指定其它第三方库的托管平台。使用方法可参照 [pypi 镜像使用帮助 - 清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/) 等使用帮助。你可以在 [MirrorZ](https://mirrorz.org/list/pypi) 上获取更多 PyPI 镜像源。

使用清华大学开源镜像站安装一个包

<table><tbody><tr><td></td><td><div><pre><code tabindex="0">pipinstall-ihttps://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple&lt;some-package&gt;
</code></pre></div></td></tr></tbody></table>

## 基本语法

Python 的语法简洁而易懂，也有许多官方和第三方文档与教程。这里仅介绍一些对 OIer 比较实用的语言特性，你可以在 [Python 文档](https://docs.python.org/zh-cn/3/) 和 [Python Wiki](https://wiki.python.org/moin/) 等网页上了解更多关于 Python 的教程。

### 注释

加入注释并不会对代码的运行产生影响，但加入注释可以使代码更加易懂易用。

<table><tbody><tr><td></td><td><div><pre><code><span># 用 # 字符开头的是单行注释</span>

<span>"""</span>
<span>跨多行字符串会用三引号</span>
<span>（即三个单引号或三个双引号）</span>
<span>包裹，但也通常被用于注释</span>
<span>"""</span>
</code></pre></div></td></tr></tbody></table>

加入注释代码并不会对代码产生影响。我们鼓励加入注释来使代码更加易懂易用。

### 基本数据类型

#### 一切皆对象

在 Python 中，你无需事先声明变量名及其类型，直接赋值即可创建各种类型的变量：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>x</span> <span>=</span> <span>-</span><span>3</span>  <span># 语句结尾不用加分号</span>
<span>&gt;&gt;&gt; </span><span>x</span>
<span>-3</span>
<span>&gt;&gt;&gt; </span><span>f</span> <span>=</span> <span>3.1415926535897932384626</span><span>;</span> <span>f</span>  <span># 实在想加分号也可以，这里节省了一行</span>
<span>3.141592653589793</span>
<span>&gt;&gt;&gt; </span><span>s1</span> <span>=</span> <span>"O"</span>
<span>&gt;&gt;&gt; </span><span>s1</span>  <span># 在 Python 中双引号和单引号的作用相同</span>
<span>'O'</span>
<span>&gt;&gt;&gt; </span><span>b</span> <span>=</span> <span>'A'</span> <span>==</span> <span>65</span>  <span># 'A' 和 65 不是一个数据类型，所以不相等</span>
<span>&gt;&gt;&gt; </span><span>b</span>  <span># True, False 首字母均大写</span>
<span>False</span>
<span>&gt;&gt;&gt; </span><span>True</span> <span>+</span> <span>1</span> <span>==</span> <span>2</span> <span>and</span> <span>not</span> <span>False</span> <span>!=</span> <span>0</span>  <span># Python 中的表达式中大多使用单词，但是也支持符号</span>
<span>True</span>
</code></pre></div></td></tr></tbody></table>

但这不代表 Python 没有类型的概念，实际上解释器会根据赋值或运算自动推断变量类型，你可以使用内置函数 `type()` 查看这些变量的类型：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>x</span><span>)</span>
<span>&lt;class 'int'&gt;</span>
<span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>f</span><span>)</span>
<span>&lt;class 'float'&gt;</span>
<span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>s1</span><span>)</span>  <span># 请注意，不要给字符串起名为 str，否则 str 对象会被篡改</span>
<span>&lt;class 'str'&gt;</span>
<span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>b</span><span>)</span>
<span>&lt;class 'bool'&gt;</span>
</code></pre></div></td></tr></tbody></table>

[**内置函数**](https://docs.python.org/zh-cn/3/library/functions.html) 是什么？

在 C/C++ 中，很多常用函数都分散在不同的头文件中，但 Python 的解释器内置了许多实用且通用的函数，你可以直接使用而无需注意它们的存在，但这也带来了小问题，这些内置函数的名称多为常见单词，你需要注意避免给自己的变量起相同的名字，否则可能会产生奇怪的结果。

正如我们所看到的，Python 内置有整数、浮点数、字符串和布尔类型，可以类比为 C++ 中的 `int`，`float`，`string` 和 `bool`。但有一些明显的不同之处，比如没有 `char` 字符类型，也没有 `double` 类型（但 `float` 其实对应 C 中的双精度），如果需要更精确的浮点运算，可以使用标准库中的 [decimal](https://docs.python.org/zh-cn/3/library/decimal.html) 模块，如果需要用到复数，Python 还内置了 `complex` 类型（而这也意味着最好不要给变量起名为 `complex`）。 可以看到这些类型都以 `class` 开头，而这正是 Python 不同于 C++ 的关键之处，Python 程序中的所有数据都是由对象或对象间关系来表示的，函数是对象，类型本身也是对象：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>int</span><span>)</span>
<span>&lt;class 'type'&gt;</span>
<span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>pow</span><span>)</span>  <span># 求幂次的内置函数，后文会介绍</span>
<span>&lt;class 'builtin_function_or_method'&gt;</span>
<span>&gt;&gt;&gt; </span><span>type</span><span>(</span><span>type</span><span>)</span>  <span># type() 也是内置函数，但有些特殊，感兴趣可自行查阅</span>
<span>&lt;class 'type'&gt;</span>
</code></pre></div></td></tr></tbody></table>

你或许会觉得这些概念一时难以理解且没有用处，所以我们暂时不再深入，在后文的示例中你或许能慢慢体会到，Python 的对象提供了强大的方法，我们在编程时应当优先考虑围绕对象而不是过程进行操作，这会让我们的代码显得更加紧凑明晰。

#### 数字运算

有人说，你可以把你系统里装的 Python 当作一个多用计算器，这是事实。 在交互模式下，你可以在提示符 `>>>` 后面输入一个表达式，就像其他大部分语言（如 C++）一样使用运算符 `+`、`-`、`*`、`/`、`%` 来对数字进行运算，也可以使用 `()` 来进行符合结合律的分组，读者可以自行试验，在这里我们仅展示与 C++ 差异较大的部分：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span></pre></div></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>5.0</span> <span>*</span> <span>6</span>  <span># 浮点数的运算结果是浮点数</span>
<span>30.0</span>
<span>&gt;&gt;&gt; </span><span>15</span> <span>/</span> <span>3</span>  <span># 与 C/C++ 不同，除法永远返回浮点 float 类型</span>
<span>5.0</span>
<span>&gt;&gt;&gt; </span><span>5</span> <span>/</span> <span>100000</span>  <span># 位数太多，结果显示成科学计数法形式</span>
<span>5e-05</span>
<span>&gt;&gt;&gt; </span><span>5</span> <span>//</span> <span>3</span> <span># 使用整数除法（地板除）则会向下取整，输出整数类型</span>
<span>1</span>
<span>&gt;&gt;&gt; </span><span>-</span><span>5</span> <span>//</span> <span>3</span> <span># 符合向下取整原则，注意这与 C/C++ 不同</span>
<span>-2</span>
<span>&gt;&gt;&gt; </span><span>5</span> <span>%</span> <span>3</span> <span># 取模</span>
<span>2</span>
<span>&gt;&gt;&gt; </span><span>-</span><span>5</span> <span>%</span> <span>3</span> <span># 负数取模结果一定是非负数，这点也与 C/C++ 不同，不过都满足 (a//b)*b+(a%b)==a </span>
<span>1</span>
<span>&gt;&gt;&gt; </span><span>x</span> <span>=</span> <span>abs</span><span>(</span><span>-</span><span>1e4</span><span>)</span>  <span># 求绝对值的内置函数</span>
<span>&gt;&gt;&gt; </span><span>x</span> <span>+=</span> <span>1</span>  <span># 没有自增/自减运算符</span>
<span>&gt;&gt;&gt; </span><span>x</span>  <span># 科学计数法默认为 float</span>
<span>10001.0</span>
</code></pre></div></td></tr></tbody></table>

在上面的实践中可以发现，除法运算（`/`）永远返回浮点类型（在 Python 2 中返回整数）。如果你想要整数或向下取整的结果的话，可以使用整数除法（`//`）。同样的，你也可以像 C++ 中一样，使用模（`%`）来计算余数，科学计数法的形式也相同。

特别地，Python 用 `**` 即可进行幂运算，还通过内置的 `pow(a, b, mod)` 提供了 [快速幂](https://oi.wiki/math/binary-exponentiation/) 的高效实现。

<table><tbody><tr><td></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>3</span> <span>**</span> <span>4</span> <span># 幂运算</span>
<span>81</span>
<span>&gt;&gt;&gt; </span><span>2</span> <span>**</span> <span>512</span>
<span>13407807929942597099574024998205846127479365820592393377723561443721764030073546976801874298166903427690031858186486050853753882811946569946433649006084096</span>
<span>&gt;&gt;&gt; </span><span>pow</span><span>(</span><span>2</span><span>,</span> <span>512</span><span>,</span> <span>int</span><span>(</span><span>1e4</span><span>))</span> <span># 即 2**512 % 10000 的快速实现, 1e4 是 float 所以要转 int</span>
<span>4096</span>
<span>&gt;&gt;&gt; </span><span>2048</span> <span>**</span> <span>2048</span> <span># 在IDLE里试试大整数？</span>
<span>&gt;&gt;&gt; </span><span>0.1</span> <span>+</span> <span>0.1</span> <span>+</span> <span>0.1</span> <span>-</span> <span>0.3</span> <span>==</span> <span>0.</span>  <span># 和 C/C++ 一样需要注意浮点数不能直接判相等</span>
<span>False</span>
</code></pre></div></td></tr></tbody></table>

#### 数据类型判断

对于一个变量，可以使用 `type(object)` 返回变量的类型，例如 `type(8)` 和 `type('a')` 的值分别为 `<class 'int'>` 和 `<class 'str'>`。

#### [基本输入输出](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html)

Python 中的输入输出主要通过内置函数 `input()` 和 `print()` 完成，`print()` 的用法十分符合直觉：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>a</span> <span>=</span> <span>[</span><span>1</span><span>,</span><span>2</span><span>,</span><span>3</span><span>];</span> <span>print</span><span>(</span><span>a</span><span>[</span><span>-</span><span>1</span><span>])</span>  <span># 打印时默认末尾换行</span>
<span>3</span>
<span>&gt;&gt;&gt; </span><span>print</span><span>(</span><span>ans</span><span>[</span><span>0</span><span>],</span> <span>ans</span><span>[</span><span>1</span><span>])</span>  <span># 可以输出任意多个变量，默认以空格间隔</span>
<span>1 2</span>
<span>&gt;&gt;&gt; </span><span>print</span><span>(</span><span>a</span><span>[</span><span>0</span><span>],</span> <span>a</span><span>[</span><span>1</span><span>],</span> <span>end</span><span>=</span><span>''</span><span>)</span>  <span># 令 end='', 使末尾不换行</span>
<span>1 2&gt;&gt;&gt;</span>
<span>&gt;&gt;&gt; </span><span>print</span><span>(</span><span>a</span><span>[</span><span>0</span><span>],</span> <span>a</span><span>[</span><span>1</span><span>],</span> <span>sep</span><span>=</span><span>', '</span><span>)</span>  <span># 令 sep=', '，改变间隔样式</span>
<span>1, 2</span>
<span>&gt;&gt;&gt; </span><span>print</span><span>(</span><span>str</span><span>(</span><span>a</span><span>[</span><span>0</span><span>])</span> <span>+</span> <span>', '</span> <span>+</span> <span>str</span><span>(</span><span>a</span><span>[</span><span>1</span><span>]))</span>  <span># 输出同上，但是手动拼接成一整个字符串</span>
</code></pre></div></td></tr></tbody></table>

`input()` 函数的行为接近 C++ 中的 `getline()`，即将一整行作为字符串读入，且末尾没有换行符。

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>s</span> <span>=</span> <span>input</span><span>(</span><span>'请输入一串数字: '</span><span>);</span> <span>s</span>  <span># 自己调试时可以向 input() 传入字符串作为提示</span>
<span>请输入一串数字: 1 2 3 4 5 6</span>
<span>'1 2 3 4 5 6'</span>
</code></pre></div></td></tr></tbody></table>

#### 字符串

Python 3 提供了强大的基于 [Unicode](https://docs.python.org/zh-cn/3/howto/unicode.html#unicode-howto) 的字符串类型，使用起来和 C++ 中的 `string` 类似，一些概念如转义字符也都相通，除了加号拼接和索引访问，还额外支持数乘 `*` 重复字符串，和 `in` 操作符。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span></pre></div></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>s1</span> <span>=</span> <span>"O"</span>  <span># 单引号和双引号都能包起字符串，有时可节省转义字符</span>
<span>&gt;&gt;&gt; </span><span>s1</span> <span>+=</span> <span>'I-Wiki'</span>  <span># 为和 C++ 同步建议使用双引号 </span>
<span>&gt;&gt;&gt; </span><span>'OI'</span> <span>in</span> <span>s1</span>  <span># 检测子串很方便</span>
<span>True</span>
<span>&gt;&gt;&gt; </span><span>len</span><span>(</span><span>s1</span><span>)</span>  <span># 类似 C++ 的 s.length()，但更通用</span>
<span>7</span>
<span>&gt;&gt;&gt; </span><span>s2</span> <span>=</span> <span>""" 感谢你的阅读</span>
<span>... </span><span>欢迎参与贡献!</span>
<span>"""   # 使用三重引号的字符串可以跨越多行</span>
<span>&gt;&gt;&gt; </span><span>s1 + s2 </span>
<span>'OI-Wiki 感谢你的阅读\n欢迎参与贡献!'</span>
<span>&gt;&gt;&gt; </span><span>print(s1 + s2)  # 这里使用了 print() 函数打印字符串</span>
<span>OI-Wiki 感谢你的阅读</span>
<span>欢迎参与贡献!</span>
<span>&gt;&gt;&gt; </span><span>s2[2] * 2 + s2[3] + s2[-1]  # 负数索引从右开始计数，加上 len(s)，相当于模 n 的剩余类环</span>
<span>'谢谢你!'</span>
<span>&gt;&gt;&gt; </span><span>s1[0] = 'o'  # str 是不可变类型，不能原地修改，其实 += 也是创建了新的对象</span>
<span>Traceback (most recent call last):</span>
  File <span>"&lt;stdin&gt;"</span>, line <span>1</span>, in <span>&lt;module&gt;</span>
<span>TypeError</span>: <span>'str' object does not support item assignment</span>
</code></pre></div></td></tr></tbody></table>

Python 支持多种复合数据类型，可将不同值组合在一起。最常用的 `list`，类型是用方括号标注、逗号分隔的一组值。例如，`[1, 2, 3]` 和 `['a','b','c']` 都是列表。

除了索引，字符串还支持_切片_，它的设计非常精妙，格式为 `s[左闭索引:右开索引:步长]`：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>s</span> <span>=</span> <span>'OI-Wiki 感谢你的阅读</span><span>\n</span><span>欢迎参与贡献!'</span>
<span>&gt;&gt;&gt; </span><span>s</span><span>[:</span><span>8</span><span>]</span>  <span># 省略左闭索引则从头开始</span>
<span>'OI-Wiki '</span>
<span>&gt;&gt;&gt; </span><span>s</span><span>[</span><span>8</span><span>:</span><span>14</span><span>]</span>  <span># 左闭右开设计的妙处，长度为 14-8=6，还和上一个字符串无缝衔接</span>
<span>'感谢你的阅读'</span>
<span>&gt;&gt;&gt; </span><span>s</span><span>[</span><span>-</span><span>4</span><span>:]</span>  <span># 省略右开索引则直到结尾</span>
<span>'与贡献!'</span>
<span>&gt;&gt;&gt; </span><span>s</span><span>[</span><span>8</span><span>:</span><span>14</span><span>:</span><span>2</span><span>]</span>  <span># 步长为2</span>
<span>'感你阅'</span>
<span>&gt;&gt;&gt; </span><span>s</span><span>[::</span><span>-</span><span>1</span><span>]</span>  <span># 步长为 -1 时，获得了反转的字符串</span>
<span>'!献贡与参迎欢\n读阅的你谢感 ikiW-IO'</span>
<span>&gt;&gt;&gt; </span><span>s</span>  <span># 但原来的字符串并未改变</span>
<span>'OI-Wiki 感谢你的阅读\n欢迎参与贡献!'</span>
</code></pre></div></td></tr></tbody></table>

在最新的 Python 3 版本中，字符串是以 Unicode 编码的，也就是说，Python 的字符串支持多语言。[2](https://oi.wiki/lang/python/#fn:ref2)在 Python 中，可以对一个 Unicode 字符使用内置函数 `ord()` 将其转换为对应的 Unicode 编码，逆向的转换使用内置函数 `chr()`。C/C++ 中 `char` 类型也可以和 对应的 ASCII 码互转。

如果想把数字转换成对应的字符串，可以使用内置函数 `str()`，反之可以使用 `int()` 和 `float()`，你可以类比为 C/C++ 中的强制类型转换，但括号不是加在类型上而是作为函数的一部分括住参数。

Python 的字符串类型提供了许多强大的方法，包括计算某字符的索引与出现次数，转换大小写等等，这里就不一一列举，强烈建议查看 [官方文档](https://docs.python.org/zh-cn/3/library/stdtypes.html#text-sequence-type-str) 熟悉常用方法，遇到字符串操作应当首先考虑使用这些方法而非自力更生。

### 创建数组

从 C++ 转过来的同学可能很迷惑怎么在 Python 中创建数组，这里就介绍在 Python 开「数组」的语法，需要强调我们介绍的其实是几种 [序列类型](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator-types)，和 C 的数组有着本质区别，而更接近 C++ 中的 `vector`。

#### 使用 `list`

列表（`list`）大概是 Python 中最常用也最强大的序列类型，列表中可以存放任意类型的元素，包括嵌套的列表，这符合数据结构中「广义表」的定义。请注意不要将其与 C++ STL 中的双向链表 [`list`](https://oi.wiki/lang/csl/sequence-container/#list) 混淆，故本文将使用「列表」而非 `list` 以免造成误解。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span>
<span>23</span>
<span>24</span>
<span>25</span>
<span>26</span>
<span>27</span>
<span>28</span>
<span>29</span></pre></div></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>[]</span>  <span># 创建空列表，注意列表使用方括号</span>
<span>[]</span>
<span>&gt;&gt;&gt; </span><span>nums</span> <span>=</span> <span>[</span><span>0</span><span>,</span> <span>1</span><span>,</span> <span>2</span><span>,</span> <span>3</span><span>,</span> <span>5</span><span>,</span> <span>8</span><span>,</span> <span>13</span><span>];</span> <span>nums</span>  <span># 初始化列表，注意整个列表可以直接打印</span>
<span>[0, 1, 2, 3, 5, 8, 13]</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>[</span><span>0</span><span>]</span> <span>=</span> <span>1</span><span>;</span> <span>nums</span>  <span># 支持索引访问，支持修改元素</span>
<span>[1, 1, 2, 3, 5, 8, 13]</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>append</span><span>(</span><span>nums</span><span>[</span><span>-</span><span>2</span><span>]</span><span>+</span><span>nums</span><span>[</span><span>-</span><span>1</span><span>]);</span> <span>nums</span>  <span># append() 同 vector 的 push_back()，也都没有返回值</span>
<span>[1, 1, 2, 3, 5, 8, 13, 21]</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>pop</span><span>()</span>  <span># 弹出并返回末尾元素，可以当栈使用；其实还可指定位置，默认是末尾</span>
<span>21</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>insert</span><span>(</span><span>0</span><span>,</span> <span>1</span><span>);</span> <span>nums</span>  <span># 同 vector 的 insert(position, val)</span>
<span>[1, 1, 1, 2, 3, 5, 8, 13]</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>remove</span><span>(</span><span>1</span><span>);</span> <span>nums</span>  <span># 按值移除元素（只删第一个出现的），若不存在则抛出错误</span>
<span>[1, 1, 2, 3, 5, 8, 13]</span>
<span>&gt;&gt;&gt; </span><span>len</span><span>(</span><span>nums</span><span>)</span>  <span># 求列表长度，类似 vector 的 size()，但 len() 是内置函数</span>
<span>7</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>reverse</span><span>();</span> <span>nums</span>  <span># 原地逆置</span>
<span>[13, 8, 5, 3, 2, 1, 1]</span>
<span>&gt;&gt;&gt; </span><span>sorted</span><span>(</span><span>nums</span><span>)</span>  <span># 获得排序后的列表</span>
<span>[1, 1, 2, 3, 5, 8, 13]</span>
<span>&gt;&gt;&gt; </span><span>nums</span>  <span># 但原来的列表并未排序</span>
<span>[13, 8, 5, 3, 2, 1, 1]</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>sort</span><span>();</span> <span>nums</span>  <span># 原地排序，可以指定参数 key 作为排序标准</span>
<span>[1, 1, 2, 3, 5, 8, 13]</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>count</span><span>(</span><span>1</span><span>)</span>  <span># 类似 std::count()</span>
<span>2</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>index</span><span>(</span><span>1</span><span>)</span>  <span># 返回值首次出现项的索引号，若不存在则抛出错误</span>
<span>0</span>
<span>&gt;&gt;&gt; </span><span>nums</span><span>.</span><span>clear</span><span>();</span> <span>nums</span>  <span># 同 vector 的 clear()</span>
</code></pre></div></td></tr></tbody></table>

以上示例展现了列表与 `vector` 的相似之处，`vector` 中常用的操作一般也都能在列表中找到对应方法，不过某些方法如 `len()`,`sorted()` 会以内置函数的面目出现，而 STL 算法中的函数如 `find()`,`count()`,`max_element()`,`sort()`,`reverse()` 在 Python 中又成了对象的方法，使用时需要注意区分，更多方法请参见官方文档的 [列表详解](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#more-on-lists)。下面将展示列表作为 Python 的基本序列类型的一些强大功能：

Python 支持多种复合数据类型，可将不同值组合在一起。最常用的 `list`，类型是用方括号标注、逗号分隔的一组值。例如，`[1, 2, 3]` 和 `['a','b','c']` 都是列表。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span></pre></div></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>lst</span> <span>=</span> <span>[</span><span>1</span><span>,</span> <span>'1'</span><span>]</span> <span>+</span> <span>[</span><span>"2"</span><span>,</span> <span>3.0</span><span>]</span>  <span># 列表直接相加生成一个新列表</span>
<span>&gt;&gt;&gt; </span><span>lst</span>  <span># 这里存放不同的类型只是想说明可以这么做，但这不是好的做法</span>
<span>[1, '1', '2', 3.0]</span>
<span>&gt;&gt;&gt; </span><span>3</span> <span>in</span> <span>lst</span>  <span># 实用的成员检测操作，字符串也有该操作且还支持子串检测</span>
<span>True</span>
<span>&gt;&gt;&gt; </span><span>[</span><span>1</span><span>,</span> <span>'1'</span><span>]</span> <span>in</span> <span>lst</span>  <span># 仅支持单个成员检测，不会发现「子序列」</span>
<span>False</span>
<span>&gt;&gt;&gt; </span><span>lst</span><span>[</span><span>1</span><span>:</span><span>3</span><span>]</span> <span>=</span> <span>[</span><span>2</span><span>,</span> <span>3</span><span>];</span> <span>lst</span>  <span># 切片并赋值，原列表被修改</span>
<span>[1, 2, 3, 3.0]</span>
<span>&gt;&gt;&gt; </span><span>lst</span><span>[::</span><span>-</span><span>1</span><span>]</span>  <span># 获得反转后的新列表</span>
<span>[3.0, 3, 2, 1]</span>
<span>&gt;&gt;&gt; </span><span>lst</span> <span>*=</span> <span>2</span><span>;</span> <span>lst</span>  <span># 数乘拼接</span>
<span>[1, 2, 3, 3.0, 1, 2, 3, 3.0]</span>
<span>&gt;&gt;&gt; </span><span>del</span> <span>lst</span><span>[</span><span>4</span><span>:];</span> <span>lst</span>  <span># 也可写 lst[4:] = []，del 语句不止可以用于删除序列中元素</span>
<span>[1, 2, 3, 3.0]</span>
</code></pre></div></td></tr></tbody></table>

以上示例展现了列表作为序列的一些常用操作，可以看出许多操作如切片是与字符串相通的，但字符串是「不可变序列」而列表是「可变序列」，故可以通过切片灵活地修改列表。在 C/C++ 中我们往往会通过循环处理字符数组，下面将展示如何使用 [「列表推导式」](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions) 在字符串和列表之间转换：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span># 建立一个 [65, 70) 区间上的整数数组，range 也是一种类型，可看作左闭右开区间，第三个参数为步长可省略</span>
<span>&gt;&gt;&gt; </span><span>nums</span> <span>=</span> <span>list</span><span>(</span><span>range</span><span>(</span><span>65</span><span>,</span><span>70</span><span>))</span>  <span># 记得 range 外面还要套一层 list()</span>
<span>[65, 66, 67, 68, 69]</span>
<span>&gt;&gt;&gt; </span><span>lst</span> <span>=</span> <span>[</span><span>chr</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>nums</span><span>]</span>  <span># 列表推导式的典型结构，[exp for var in iterable if cond]</span>
<span>&gt;&gt;&gt; </span><span>lst</span>  <span># 上两句可以合并成 [chr(x) for x in range(65,70)]</span>
<span>['A', 'B', 'C', 'D', 'E']</span>
<span>&gt;&gt;&gt; </span><span>s</span> <span>=</span> <span>''</span><span>.</span><span>join</span><span>(</span><span>lst</span><span>);</span> <span>s</span> <span># 用空字符串 '' 拼接列表中的元素生成新字符串</span>
<span>'ABCDE'</span>
<span>&gt;&gt; list(s)  # 字符串生成字符列表</span>
<span>['A', 'B', 'C', 'D', 'E']</span>
<span>&gt;&gt;&gt; </span><span># 如果你不知道有 s.lower() 方法就可能写出下面这样新瓶装旧酒的表达式</span>
<span>&gt;&gt;&gt; </span><span>''</span><span>.</span><span>join</span><span>([</span><span>chr</span><span>(</span><span>ord</span><span>(</span><span>ch</span><span>)</span> <span>-</span> <span>65</span> <span>+</span> <span>97</span><span>)</span> <span>for</span> <span>ch</span> <span>in</span> <span>s</span> <span>if</span> <span>ch</span> <span>&gt;=</span> <span>'A'</span> <span>and</span> <span>ch</span> <span>&lt;=</span> <span>'Z'</span><span>])</span>  
<span>'abcde'</span>
</code></pre></div></td></tr></tbody></table>

下面演示一些在 OI 中更常见的场景，比如二维「数组」：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span>
<span>23</span>
<span>24</span>
<span>25</span>
<span>26</span>
<span>27</span>
<span>28</span></pre></div></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>vis</span> <span>=</span> <span>[[</span><span>0</span><span>]</span> <span>*</span> <span>3</span><span>]</span> <span>*</span> <span>3</span>  <span># 开一个 3*3 的全 0 数组</span>
<span>&gt;&gt;&gt; </span><span>vis</span> 
<span>[[0, 0, 0], [0, 0, 0], [0, 0, 0]]</span>
<span>&gt;&gt;&gt; </span><span>vis</span><span>[</span><span>0</span><span>][</span><span>0</span><span>]</span> <span>=</span> <span>1</span><span>;</span> <span>vis</span>  <span># 怎么会把其他行也修改了？</span>
<span>[[1, 0, 0], [1, 0, 0], [1, 0, 0]]</span>
<span>&gt;&gt;&gt; </span><span># 先来看下一维列表的赋值</span>
<span>&gt;&gt;&gt; </span><span>a1</span> <span>=</span> <span>[</span><span>0</span><span>,</span> <span>0</span><span>,</span> <span>0</span><span>];</span> <span>a2</span> <span>=</span> <span>a1</span><span>;</span> <span>a3</span> <span>=</span> <span>a1</span><span>[:]</span>  <span># 列表也可以直接被赋给新的变量</span>
<span>&gt;&gt;&gt; </span><span>a1</span><span>[</span><span>0</span><span>]</span> <span>=</span> <span>1</span><span>;</span> <span>a1</span>  <span># 修改列表 a1，似乎正常</span>
<span>[1, 0, 0]</span>
<span>&gt;&gt;&gt; </span><span>a2</span>  <span># 怎么 a2 也被改变了</span>
<span>[1, 0, 0]</span>
<span>&gt;&gt;&gt; </span><span>a3</span>  <span># a3 没有变化</span>
<span>[0, 0, 0]</span>
<span>&gt;&gt;&gt; </span><span>id</span><span>(</span><span>a1</span><span>)</span> <span>==</span> <span>id</span><span>(</span><span>a2</span><span>)</span> <span>and</span> <span>id</span><span>(</span><span>a1</span><span>)</span> <span>!=</span> <span>id</span><span>(</span><span>a3</span><span>)</span>  <span># 内置函数 id() 给出对象的「标识值」，可类比为地址，地址相同说明是一个对象</span>
<span>True</span>
<span>&gt;&gt;&gt; </span><span>vis2</span> <span>=</span> <span>vis</span><span>[:]</span>  <span># 拷贝一份二维列表</span>
<span>&gt;&gt;&gt; </span><span>vis</span><span>[</span><span>0</span><span>][</span><span>1</span><span>]</span> <span>=</span> <span>2</span><span>;</span> <span>vis</span>  <span># vis 会被批量修改</span>
<span>&gt;&gt;&gt; </span><span>[[</span><span>1</span><span>,</span> <span>2</span><span>,</span> <span>0</span><span>],</span> <span>[</span><span>1</span><span>,</span> <span>2</span><span>,</span> <span>0</span><span>],</span> <span>[</span><span>1</span><span>,</span> <span>2</span><span>,</span> <span>0</span><span>]]</span>
<span>&gt;&gt;&gt; </span><span>vis2</span>  <span># 但 vis2 是切片拷贝还是被改了</span>
<span>&gt;&gt;&gt; </span><span>[[</span><span>1</span><span>,</span> <span>2</span><span>,</span> <span>0</span><span>],</span> <span>[</span><span>1</span><span>,</span> <span>2</span><span>,</span> <span>0</span><span>],</span> <span>[</span><span>1</span><span>,</span> <span>2</span><span>,</span> <span>0</span><span>]]</span>
<span>&gt;&gt;&gt; </span><span>id</span><span>(</span><span>vis</span><span>)</span> <span>!=</span> <span>id</span><span>(</span><span>vis2</span><span>)</span>  <span># vis 和 vis2 不是一个对象</span>
<span>True</span>
<span>&gt;&gt;&gt; </span><span># vis2 虽然不是 vis 的引用，但其中对应行都指向相同的对象</span>
<span>&gt;&gt;&gt; </span><span>[</span><span>id</span><span>(</span><span>vis</span><span>[</span><span>i</span><span>])</span> <span>==</span> <span>id</span><span>(</span><span>vis2</span><span>[</span><span>i</span><span>])</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>3</span><span>)]</span>
<span>[True, True, True]</span>
<span>&gt;&gt;&gt; </span><span># 回看二维列表自身</span>
<span>&gt;&gt;&gt; </span><span>[</span><span>id</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>vis</span><span>]</span>  <span># 具体数字和这里不一样但三个值一定相同，说明是三个相同对象</span>
<span>[139760373248192, 139760373248192, 139760373248192]</span>
</code></pre></div></td></tr></tbody></table>

其实有一个重要的事实，Python 中赋值只传递了引用而非创建新值，你可以创建不同类型的变量并赋给新变量，验证发现二者的标识值是相同的，只不过直到现在我们才介绍了列表这一种可变类型，而给数字、字符串这样的不可变类型赋新值时实际上创建了新的对象，故而前后两个变量互不干扰。但列表是可变类型，所以我们修改一个列表的元素时，另一个列表由于指向同一个对象所以也被修改了。创建二维数组也是类似的情况，示例中用乘法创建二维列表相当于把 `[0]*3` 这个一维列表重复了 3 遍，所以涉及其中一个列表的操作会同时影响其他两个列表。更不幸的是，在将二维列表赋给其他变量的时候，就算用切片来拷贝，也只是「浅拷贝」，其中的元素仍然指向相同的对象，解决这个问题需要使用标准库中的 [`deepcopy`](https://docs.python.org/3/library/copy.html)，或者尽量避免整个赋值二维列表。不过还好，创建二维列表时避免创建重复的列表还是比较简单，只需使用「列表推导式」：

<table><tbody><tr><td></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>vis1</span> <span>=</span> <span>[[</span><span>0</span><span>]</span> <span>*</span> <span>3</span> <span>for</span> <span>_</span> <span>in</span> <span>range</span><span>(</span><span>3</span><span>)]</span>  <span># 把用不到的循环计数变量设为下划线 _ 是一种惯例</span>
<span>&gt;&gt;&gt; </span><span># 但在 REPL 中 _ 默认指代上一个表达式输出的结果，故也可使用双下划线</span>
<span>&gt;&gt;&gt; </span><span>vis1</span>
<span>[[0, 0, 0], [0, 0, 0], [0, 0, 0]]</span>
<span>&gt;&gt;&gt; </span><span>[</span><span>id</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>vis1</span><span>]</span>  <span># 具体数字和这里不一样但三个值一定不同，说明是三个不同对象</span>
<span>[139685508981248, 139685508981568, 139685508981184]</span>
<span>&gt;&gt;&gt; </span><span>vis1</span><span>[</span><span>0</span><span>][</span><span>0</span><span>]</span> <span>=</span> <span>1</span>
<span>[[1, 0, 0], [0, 0, 0], [0, 0, 0]]</span>
<span>&gt;&gt;&gt; </span><span>a2</span><span>[</span><span>0</span><span>][</span><span>0</span><span>]</span> <span>=</span> <span>10</span>  <span># 访问和赋值二维数组</span>
</code></pre></div></td></tr></tbody></table>

我们未讲循环的用法就先介绍了列表推导式，这是由于 Python 是高度动态的解释型语言，因此其程序运行有大量的额外开销。尤其是 **for 循环在 Python 中运行的奇慢无比**。因此在使用 Python 时若想获得高性能，尽量使用列表推导式，或者 `filter`,`map` 等内置函数直接操作整个序列来避免循环，当然这还是要根据具体问题而定。

#### 使用 NumPy

什么是 NumPy

[NumPy](https://numpy.org/) 是著名的 Python 科学计算库，提供高性能的数值及矩阵运算。在测试算法原型时可以利用 NumPy 避免手写排序、求最值等算法。NumPy 的核心数据结构是 `ndarray`，即 n 维数组，它在内存中连续存储，是定长的。此外 NumPy 核心是用 C 编写的，运算效率很高。不过需要注意，它不是标准库的一部分，可以使用 `pip install numpy` 安装，但不保证 OI 考场环境中可用（参见文首 [Python 版本](https://oi.wiki/lang/python/#%E4%B8%80%E4%BA%9B%E5%B9%B3%E5%8F%B0%E6%8F%90%E4%BE%9B%E7%9A%84-python-%E7%89%88%E6%9C%AC)）。

下面的代码将介绍如何利用 NumPy 建立多维数组并进行访问。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span>
<span>23</span>
<span>24</span>
<span>25</span>
<span>26</span>
<span>27</span>
<span>28</span>
<span>29</span>
<span>30</span>
<span>31</span></pre></div></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>import</span><span>numpy</span><span>as</span><span>np</span>  <span># 请自行搜索 import 的意义和用法</span>
<span>&gt;&gt;&gt; </span><span>np</span><span>.</span><span>empty</span><span>(</span><span>3</span><span>)</span> <span># 开容量为 3 的空数组，注意没有初始化为 0</span>
<span>array([0.00000000e+000, 0.00000000e+000, 2.01191014e+180])</span>
<span>&gt;&gt;&gt; </span><span>np</span><span>.</span><span>zeros</span><span>((</span><span>3</span><span>,</span> <span>3</span><span>))</span> <span># 开 3*3 的数组，并初始化为 0</span>
<span>array([[0., 0., 0.],</span>
<span>       [0., 0., 0.],</span>
<span>       [0., 0., 0.]])</span>
<span>&gt;&gt;&gt; </span><span>a1</span> <span>=</span> <span>np</span><span>.</span><span>zeros</span><span>((</span><span>3</span><span>,</span> <span>3</span><span>),</span> <span>dtype</span><span>=</span><span>int</span><span>)</span> <span># 开 3×3 的整数数组</span>
<span>&gt;&gt;&gt; </span><span>a1</span><span>[</span><span>0</span><span>][</span><span>0</span><span>]</span> <span>=</span> <span>1</span> <span># 访问和赋值</span>
<span>&gt;&gt;&gt; </span><span>a1</span><span>[</span><span>0</span><span>,</span> <span>0</span><span>]</span> <span>=</span> <span>1</span> <span># 更友好的语法</span>
<span>&gt;&gt;&gt; </span><span>a1</span><span>.</span><span>shape</span> <span># 数组的形状</span>
<span>(3, 3)</span>

<span>&gt;&gt;&gt; </span><span>a1</span><span>[:</span><span>2</span><span>,</span> <span>:</span><span>2</span><span>]</span> <span># 取前两行、前两列构成的子阵，无拷贝</span>
<span>array([[1, 0],</span>
<span>       [0, 0]])</span>

<span>&gt;&gt;&gt; </span><span>a1</span><span>[:,</span> <span>[</span><span>0</span><span>,</span> <span>2</span><span>]]</span> <span># 获取第 1、3 列，无拷贝</span>
<span>array([[1, 0],</span>
<span>       [0, 0],</span>
<span>       [0, 0]])</span>
<span>&gt;&gt;&gt; </span><span>np</span><span>.</span><span>max</span><span>(</span><span>a1</span><span>)</span> <span># 获取数组最大值</span>
<span>1</span>
<span>&gt;&gt;&gt; </span><span>a1</span><span>.</span><span>flatten</span><span>()</span> <span># 将数组展平</span>
<span>array([1, 0, 0, 0, 0, 0, 0, 0, 0])</span>

<span>&gt;&gt;&gt; </span><span>np</span><span>.</span><span>sort</span><span>(</span><span>a1</span><span>,</span> <span>axis</span> <span>=</span> <span>1</span><span>)</span> <span># 沿行方向对数组进行排序，返回排序结果</span>
<span>array([[0, 0, 1],</span>
<span>       [0, 0, 0],</span>
<span>       [0, 0, 0]])</span>
<span>&gt;&gt;&gt; </span><span>a1</span><span>.</span><span>sort</span><span>(</span><span>axis</span> <span>=</span> <span>1</span><span>)</span> <span># 沿行方向对数组进行原地排序</span>
</code></pre></div></td></tr></tbody></table>

#### 使用 `array`

[`array`](https://docs.python.org/zh-cn/3/library/array.html) 是 Python 标准库提供的一种高效数值数组，可以紧凑地表示基本类型值的数组，但不支持数组嵌套，也很少见到有人使用它，这里只是顺便提一下。

若无特殊说明，后文出现「数组」一般指「列表」。

### [输入输出](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html)

Python 中的输入输出主要通过内置函数 `input()` 和 `print()` 完成。前文已经介绍过，下面介绍进阶用法。

#### 格式化输出

算法竞赛中通常只涉及到基本的数值和字符串输出，`print()` 已基本足够，只有当涉及到浮点数位数时需要用到格式化字符串输出。格式化有三种方法，第一种也是最老旧的方法是使用 `printf()` 风格的 `%` 操作符；另一种是利用 [`format` 函数](https://docs.python.org/3/library/string.html#formatstrings)；第三种是 Python 3.6 新增的 [f-string](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#formatted-string-literals)，最为简洁，但不保证考场中的 Python 版本足够新。详细丰富的说明可以参考 [这个网页](https://www.python-course.eu/python3_formatted_output.php)，尽管更推荐使用 `format()` 方法，但为了获得与 C 接近的体验，下面仅演示与 `printf()` 类似的老式方法：

<table><tbody><tr><td></td><td><div><pre><code tabindex="0"><span>&gt;&gt;&gt; </span><span>pi</span> <span>=</span> <span>3.1415926</span><span>;</span> <span>print</span><span>(</span><span>'</span><span>%.4f</span><span>'</span> <span>%</span> <span>pi</span><span>)</span>   <span># 格式为 %[flags][width][.precision]type</span>
<span>3.1416</span>
<span>&gt;&gt;&gt; </span><span>'</span><span>%.4f</span><span> - </span><span>%8f</span><span> = </span><span>%d</span><span>'</span> <span>%</span> <span>(</span><span>pi</span><span>,</span> <span>0.1416</span><span>,</span> <span>3</span><span>)</span>  <span># 右边多个参数用 () 括住，后面会看到其实是「元组」 </span>
<span>'3.1416 - 0.141600 = 3'</span>
</code></pre></div></td></tr></tbody></table>

#### `split()` 函数

`input()` 函数的行为接近 C++ 中的 `getline()`，即将一整行作为字符串读入，且末尾没有换行符，但在算法竞赛中，常见的输入形式是一行输入多个数值，因此就需要使用字符串的 `split()` 方法并搭配列表推导式得到存放数值类型的列表，下面以输入 n 个数求平均值为例演示输入 n 个数得到「数组」的方法：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>s</span> <span>=</span> <span>input</span><span>(</span><span>'请输入一串数字: '</span><span>);</span> <span>s</span>  <span># 自己调试时可以向 input() 传入字符串作为提示</span>
<span>请输入一串数字: 1 2 3 4 5 6</span>
<span>'1 2 3 4 5 6'</span>
<span>&gt;&gt;&gt; </span><span>a</span> <span>=</span> <span>s</span><span>.</span><span>split</span><span>();</span> <span>a</span>
<span>['1', '2', '3', '4', '5', '6']</span>
<span>&gt;&gt;&gt; </span><span>a</span> <span>=</span> <span>[</span><span>int</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>a</span><span>];</span> <span>a</span>
<span>[1, 2, 3, 4, 5, 6]</span>
<span>&gt;&gt;&gt; </span><span># 以上输入过程可写成一行 a = [int(x) for x in input().split()]</span>
<span>&gt;&gt;&gt; </span><span>sum</span><span>(</span><span>a</span><span>)</span> <span>/</span> <span>len</span><span>(</span><span>a</span><span>)</span>  <span># sum() 是内置函数</span>
<span>3.5</span>
</code></pre></div></td></tr></tbody></table>

有时题目会在每行输入固定几个数，比如边的起点、终点、权重，如果只用上面提到的方法就只能每次读入数组然后根据下标赋值，这时可以使用 Python 的「拆包」特性一次赋值多个变量：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span> <span>=</span> <span>[</span><span>int</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>()]</span>
<span>1 2 4</span>
<span>&gt;&gt;&gt; </span><span>print</span><span>(</span><span>u</span><span>,</span><span>v</span><span>,</span><span>w</span><span>)</span>
<span>1 2 4</span>
</code></pre></div></td></tr></tbody></table>

题目中经常遇到输入 N 行的情况，可我们还没有讲最基本的循环语句，但 Python 强大的序列操作能在不使用循环的情况下应对多行输入，下面假设将各条边的起点、终点、权值分别读入三个数组：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>N</span> <span>=</span> <span>4</span><span>;</span> <span>mat</span> <span>=</span> <span>[[</span><span>int</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>()]</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>N</span><span>)]</span>
<span>1 3 3 </span>
<span>1 4 1 </span>
<span>2 3 4 </span>
<span>3 4 1 </span>
<span>&gt;&gt;&gt; </span><span>mat</span>  <span># 先按行读入二维数组</span>
<span>[[1, 3, 3], [1, 4, 1], [2, 3, 4], [3, 4, 1]]</span>
<span>&gt;&gt;&gt; </span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span> <span>=</span> <span>map</span><span>(</span><span>list</span><span>,</span> <span>zip</span><span>(</span><span>*</span><span>mat</span><span>))</span>   
<span># *将 mat 解包得到里层的多个列表</span>
<span># zip() 将多个列表中对应元素聚合成元组，得到一个迭代器</span>
<span># map(list, iterable) 将序列中的元素（这里为元组）转成列表</span>
<span>&gt;&gt;&gt; </span><span>print</span><span>(</span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span><span>)</span>  <span># 直接将 map() 得到的迭代器拆包，分别赋值给 u, v, w</span>
<span>[1, 1, 2, 3] [3, 4, 3, 4] [3, 1, 4, 1]</span>
</code></pre></div></td></tr></tbody></table>

上述程序实际上相当于先读入一个 N 行 3 列的矩阵，然后将其转置成 3 行 N 列的矩阵，也就是外层列表中嵌套了 3 个列表，最后将代表这起点、终点、权值的 3 个列表分别赋值给 u, v, w。内置函数 [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html#zip) 可以将多个等长序列中的对应元素拼接在「元组」内，得到新序列。而 `map()` 其实是函数式编程的一种操作，它将一个给定函数作用于 `zip()` 所产生序列的元素，这里就是用 `list()` 将元组变成列表。你可以自行练习使用 `*` 和 [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html#zip)，[`map()`](https://docs.python.org/zh-cn/3/library/functions.html#map) 以理解其含义。需要注意的是 Python 3 中 `zip()` 和 `map()` 创建的不再返回列表而是返回迭代器，这里暂不解释它们之间的异同，你可以认为迭代器可以产生列表中的各个元素，用 `list()` 套住迭代器就能生成列表。

#### [文件读写](https://docs.python.org/3/reference/compound_stmts.html#the-with-statement)

Python 内置函数 [`open()`](https://docs.python.org/3/library/functions.html#open) 用于文件读写，为了防止读写过程中出错导致文件未被正常关闭，这里只介绍使用 [`with`](https://docs.python.org/3/reference/compound_stmts.html#the-with-statement) 语句的安全读写方法：

<table><tbody><tr><td></td><td><div><pre><code><span>a</span> <span>=</span> <span>[]</span>
<span>with</span> <span>open</span><span>(</span><span>"in.txt"</span><span>)</span> <span>as</span> <span>f</span><span>:</span>
    <span>N</span> <span>=</span> <span>int</span><span>(</span><span>f</span><span>.</span><span>readline</span><span>())</span>  <span># 读入第一行的 N</span>
    <span>a</span><span>[</span><span>len</span><span>(</span><span>a</span><span>)</span> <span>:]</span> <span>=</span> <span>[[</span><span>int</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>f</span><span>.</span><span>readline</span><span>()</span><span>.</span><span>split</span><span>()]</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>N</span><span>)]</span>

<span>with</span> <span>open</span><span>(</span><span>"out.txt"</span><span>,</span> <span>"w"</span><span>)</span> <span>as</span> <span>f</span><span>:</span>
    <span>f</span><span>.</span><span>write</span><span>(</span><span>"1</span><span>\n</span><span>"</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

关于文件读写的函数有很多，分别适用于不同的场景，由于 OI 赛事尚不支持使用 Python，这里从略。

### [控制流程](https://docs.python.org/zh-cn/3/tutorial/controlflow.html)

尽管我们已经学习了 Python 的许多特性，但到目前为止我们展示的 Python 代码都是单行语句，这掩盖了 Python 和 C 在代码风格上的重大差异：首先，Python 中不用 `{}` 而是用缩进表示块结构，如果缩进没有对齐会直接报错，如果 tab 和 空格混用也会报错；其次，块结构开始的地方比如 `if` 和 `for` 语句的行末要有冒号 `:`。这有助于代码的可读性，但你也可能怀念 C 那种自由的体验，毕竟如果复制粘贴时因为丢失缩进而不得不手动对齐是很恼人的。

#### 循环结构

列表推导式能在一行内高效地完成批量操作，但有时为了压行我们已经显得过分刻意，许多场景下还是只能使用循环结构，所以我们再以读入多行数据为例展示 Python 中的循环是如何编写的：

<table><tbody><tr><td></td><td><div><pre><code><span># 请注意从现在开始我们不再使用 REPL，请自行复制多行数据</span>
<span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span> <span>=</span> <span>([]</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>3</span><span>))</span>  <span># 多变量赋值</span>
<span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>4</span><span>):</span>  <span># 这里假设输入 4 行数据</span>
    <span>_u</span><span>,</span> <span>_v</span><span>,</span> <span>_w</span> <span>=</span> <span>[</span><span>int</span><span>(</span><span>x</span><span>)</span> <span>for</span> <span>x</span> <span>in</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>()]</span>
    <span>u</span><span>.</span><span>append</span><span>(</span><span>_u</span><span>),</span> <span>v</span><span>.</span><span>append</span><span>(</span><span>_v</span><span>),</span> <span>w</span><span>.</span><span>append</span><span>(</span><span>_w</span><span>)</span>
    <span># 不可进行类似 cin &gt;&gt; u[i] &gt;&gt; v[i] &gt;&gt; w[i] 的操作，因为必定超出列表当前的长度</span>
    <span># 当然你可以选择初始化长度为 MAXN 的全 0 列表，不过需要记住真实长度并删掉多余元素</span>
<span>print</span><span>(</span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

需要注意，Python 中的 for 循环和 C/C++ 有较大的差别，其作用类似 C++ 11 引入的 [「基于范围的循环」](https://oi.wiki/lang/new/#%E5%9F%BA%E4%BA%8E%E8%8C%83%E5%9B%B4%E7%9A%84-for-%E5%BE%AA%E7%8E%AF)，实质是迭代序列中的元素，比如编写循环遍历数组下标需要迭代 `range(len(lst))`，而非真正定义起始和终止条件，所以使用起来并没有 C/C++ 灵活。

下面再用 while 循环展示行数不定的情况下如何输入：

<table><tbody><tr><td></td><td><div><pre><code tabindex="0"><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span> <span>=</span> <span>[],</span> <span>[],</span> <span>[]</span>  <span># 多变量赋值，其实同上</span>
<span>s</span> <span>=</span> <span>input</span><span>()</span>  <span># 注意 Python 中赋值语句不能放在条件表达式中</span>
<span>while</span> <span>s</span><span>:</span>  <span># 不能像 C 那样 while(!scanf())</span>
    <span># 用切片拼接避免了 append()，注意列表推导式中又嵌套了列表</span>
    <span>u</span><span>[</span><span>len</span><span>(</span><span>u</span><span>)</span> <span>:],</span> <span>v</span><span>[</span><span>len</span><span>(</span><span>v</span><span>)</span> <span>:],</span> <span>w</span><span>[</span><span>len</span><span>(</span><span>w</span><span>)</span> <span>:]</span> <span>=</span> <span>[[</span><span>int</span><span>(</span><span>x</span><span>)]</span> <span>for</span> <span>x</span> <span>in</span> <span>s</span><span>.</span><span>split</span><span>()]</span>
    <span>s</span> <span>=</span> <span>input</span><span>()</span>
<span># Python 3.8 引入了 walrus operator 海象运算符后，你可以节省两行，但考场环境很可能不支持</span>
<span>while</span> <span>s</span> <span>:=</span> <span>input</span><span>():</span>
    <span>u</span><span>[</span><span>len</span><span>(</span><span>u</span><span>)</span> <span>:],</span> <span>v</span><span>[</span><span>len</span><span>(</span><span>v</span><span>)</span> <span>:],</span> <span>w</span><span>[</span><span>len</span><span>(</span><span>w</span><span>)</span> <span>:]</span> <span>=</span> <span>[[</span><span>int</span><span>(</span><span>x</span><span>)]</span> <span>for</span> <span>x</span> <span>in</span> <span>s</span><span>.</span><span>split</span><span>()]</span>
<span>print</span><span>(</span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

#### 选择结构

和 C/C++ 大同小异，一些形式上的差别都在下面的示例中有所展示，此外还需注意条件表达式中不允许使用赋值运算符（Python 3.8 以上可用 [`:=`](https://www.python.org/dev/peps/pep-0572/)），以及 [没有 switch 语句](https://docs.python.org/zh-cn/3/faq/design.html#why-isn-t-there-a-switch-or-case-statement-in-python)。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span></pre></div></td><td><div><pre><code tabindex="0"><span># 条件表达式两侧无括号</span>
<span>if</span> <span>4</span> <span>&gt;=</span> <span>3</span> <span>&gt;</span> <span>2</span> <span>and</span> <span>3</span> <span>!=</span> <span>5</span> <span>==</span> <span>5</span> <span>!=</span> <span>7</span><span>:</span>
    <span>print</span><span>(</span><span>"关系运算符可以连续使用"</span><span>)</span>
    <span>x</span> <span>=</span> <span>None</span> <span>or</span> <span>[]</span> <span>or</span> <span>-</span><span>2</span>
    <span>print</span><span>(</span><span>"&amp;&amp;  ||  !"</span><span>,</span> <span>"与  或  非"</span><span>,</span> <span>"and or not"</span><span>,</span> <span>sep</span><span>=</span><span>"</span><span>\n</span><span>"</span><span>)</span>
    <span>print</span><span>(</span><span>"善用 and/or 可节省行数"</span><span>)</span>
    <span>if</span> <span>not</span> <span>x</span><span>:</span>
        <span>print</span><span>(</span><span>"负数也是 True，不执行本句"</span><span>)</span>
    <span>elif</span> <span>x</span> <span>&amp;</span> <span>1</span><span>:</span>
        <span>print</span><span>(</span><span>"用 elif 而不是 else if</span><span>\n</span><span>"</span> <span>"位运算符与 C 相近，偶数&amp;1 得 0，不执行本句"</span><span>)</span>
    <span>else</span><span>:</span>
        <span>print</span><span>(</span><span>"也有三目运算符"</span><span>)</span> <span>if</span> <span>x</span> <span>else</span> <span>print</span><span>(</span><span>"注意结构"</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

#### 异常处理

尽管 C++ 中有 [try 块](https://zh.cppreference.com/w/cpp/language/try_catch) 用于异常处理，但竞赛中一般从不使用，而 Python 中常见的是 [EAFP](https://docs.python.org/zh-cn/3/glossary.html#term-eafp) 风格，故而代码中可能大量使用 [`try-except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#the-try-statement) 语句，在后文介绍 `dict` 这一结构时还会用到，这里展示：

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code><span>s</span> <span>=</span> <span>"OI-wiki"</span>
<span>pat</span> <span>=</span> <span>"NOIP"</span>
<span>x</span> <span>=</span> <span>s</span><span>.</span><span>find</span><span>(</span><span>pat</span><span>)</span>  <span># find() 找不到返回 -1</span>
<span>try</span><span>:</span>
    <span>y</span> <span>=</span> <span>s</span><span>.</span><span>index</span><span>(</span><span>pat</span><span>)</span>  <span># index() 找不到则抛出错误</span>
    <span>print</span><span>(</span><span>y</span><span>)</span>  <span># 这句被跳过</span>
<span>except</span> <span>ValueError</span><span>:</span>
    <span>print</span><span>(</span><span>"没找到"</span><span>)</span>
    <span>try</span><span>:</span>
        <span>print</span><span>(</span><span>y</span><span>)</span>  <span># 此时 y 并没有定义，故又会抛出错误</span>
    <span>except</span> <span>NameError</span> <span>as</span> <span>e</span><span>:</span>
        <span>print</span><span>(</span><span>"无法输出 y"</span><span>)</span>
        <span>print</span><span>(</span><span>"原因:"</span><span>,</span> <span>e</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

### 内置容器

Python 内置了许多强大的容器类型，只有熟练使用并了解其特点才能真正让 Python 在算法竞赛中有用武之地，除了上面详细介绍的 `list`（列表），还有 `tuple`（元组）、[`dict`](https://docs.python.org/zh-cn/3/library/stdtypes.html#mapping-types-dict)（字典）和 `set`（集合）这几种类型。

元组可以简单理解成不可变的列表，不过还需注意「不可变」的内涵，如果元组中的某元素是可变类型比如列表，那么仍可以修改该列表的值，元组中存放的是对列表的引用所以元组本身并没有改变。元组的优点是开销较小且「[可哈希](https://docs.python.org/zh-cn/3/glossary.html)」，后者在创建字典和集合时非常有用。

<table><tbody><tr><td></td><td><div><pre><code><span>tup</span> <span>=</span> <span>tuple</span><span>([[</span><span>1</span><span>,</span> <span>2</span><span>],</span> <span>4</span><span>])</span>  <span># 由列表得到元组</span>
<span># 等同于 tup = ([1,2], 4)</span>
<span>tup</span><span>[</span><span>0</span><span>]</span><span>.</span><span>append</span><span>(</span><span>3</span><span>)</span>
<span>print</span><span>(</span><span>tup</span><span>)</span>
<span>a</span><span>,</span> <span>b</span> <span>=</span> <span>0</span><span>,</span> <span>"I-Wiki"</span>  <span># 多变量赋值其实是元组拆包</span>
<span>print</span><span>(</span><span>id</span><span>(</span><span>a</span><span>),</span> <span>id</span><span>(</span><span>b</span><span>))</span>
<span>b</span><span>,</span> <span>a</span> <span>=</span> <span>a</span><span>,</span> <span>b</span>
<span>print</span><span>(</span><span>id</span><span>(</span><span>a</span><span>),</span> <span>id</span><span>(</span><span>b</span><span>))</span>  <span># 你应该会看到 a, b 的 id 值现在互换了</span>
<span># 这更说明 Python 中，变量更像是名字，赋值只是让其指代对象</span>
</code></pre></div></td></tr></tbody></table>

字典就像 C++ STL 中的 [`map`](https://oi.wiki/lang/csl/associative-container/#map)（请注意和 Python 中内置函数 [`map()`](https://docs.python.org/zh-cn/3/library/functions.html#map) 区分）用于存储键值对，形式类似 [JSON](https://docs.python.org/3/library/json.html)，但 JSON 中键必须是字符串且以双引号括住，字典则更加灵活强大，可哈希的对象都可作为字典的键。需要注意 Python 几次版本更新后字典的特性有了较多变化，包括其中元素的顺序等，请自行探索。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span></pre></div></td><td><div><pre><code tabindex="0"><span>dic</span> <span>=</span> <span>{</span><span>"key"</span><span>:</span> <span>"value"</span><span>}</span>  <span># 基本形式</span>
<span>dic</span> <span>=</span> <span>{</span><span>chr</span><span>(</span><span>i</span><span>):</span> <span>i</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>65</span><span>,</span> <span>91</span><span>)}</span>  <span># 大写字母到对应 ASCII 码的映射，注意断句</span>
<span>dic</span> <span>=</span> <span>dict</span><span>(</span><span>zip</span><span>([</span><span>chr</span><span>(</span><span>i</span><span>)</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>65</span><span>,</span> <span>91</span><span>)],</span> <span>range</span><span>(</span><span>65</span><span>,</span> <span>91</span><span>)))</span>  <span># 效果同上</span>
<span>dic</span> <span>=</span> <span>{</span><span>dic</span><span>[</span><span>k</span><span>]:</span> <span>k</span> <span>for</span> <span>k</span> <span>in</span> <span>dic</span><span>}</span>  <span># 将键值对逆转，for k in dic 迭代其键</span>
<span>dic</span> <span>=</span> <span>{</span><span>v</span><span>:</span> <span>k</span> <span>for</span> <span>k</span><span>,</span> <span>v</span> <span>in</span> <span>dic</span><span>.</span><span>items</span><span>()}</span>  <span># 和上行作用相同，dic.items() 以元组存放单个键值对</span>
<span>dic</span> <span>=</span> <span>{</span>
    <span>k</span><span>:</span> <span>v</span> <span>for</span> <span>k</span><span>,</span> <span>v</span> <span>in</span> <span>sorted</span><span>(</span><span>dic</span><span>.</span><span>items</span><span>(),</span> <span>key</span><span>=</span><span>lambda</span> <span>x</span><span>:</span> <span>-</span><span>x</span><span>[</span><span>1</span><span>])</span>
<span>}</span>  <span># 字典按值逆排序，用到了 lambda 表达式</span>

<span>print</span><span>(</span><span>dic</span><span>[</span><span>"A"</span><span>])</span>  <span># 返回 dic 中 以 'A' 为键的项，这里值为65</span>
<span>dic</span><span>[</span><span>"a"</span><span>]</span> <span>=</span> <span>97</span>  <span># 将 d[key] 设为 value，字典中原无 key 就是直接插入</span>
<span>if</span> <span>"b"</span> <span>in</span> <span>dic</span><span>:</span>  <span># LBYL(Look Before You Leap) 风格</span>
    <span>print</span><span>(</span><span>dic</span><span>[</span><span>"b"</span><span>])</span>  <span># 若字典中无该键则会出错，故先检查</span>
<span>else</span><span>:</span>
    <span>dic</span><span>[</span><span>"b"</span><span>]</span> <span>=</span> <span>98</span>

<span># 经典场景 统计出现次数</span>
<span># 新键不存在于原字典，需要额外处理</span>
<span>try</span><span>:</span>  <span># EAFP (Easier to Ask for Forgiveness than Permission) 风格</span>
    <span>cnter</span><span>[</span><span>key</span><span>]</span> <span>+=</span> <span>1</span>
<span>except</span> <span>KeyError</span><span>:</span>
    <span>cnter</span><span>[</span><span>key</span><span>]</span> <span>=</span> <span>1</span>
</code></pre></div></td></tr></tbody></table>

集合就像 C++ STL 中的 [`set`](https://oi.wiki/lang/csl/associative-container/#set)，不会保存重复的元素，可以看成只保存键的字典。需要注意集合和字典都用 `{}` 括住，不过单用 `{}` 会创建空字典而不是空集合，这里就不再给出示例。

### 编写函数

Python 中定义函数无需指定参数类型和返回值类型，无形中为 OI 选手减少了代码量

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span></pre></div></td><td><div><pre><code><span>def</span><span>add</span><span>(</span><span>a</span><span>,</span> <span>b</span><span>):</span>
    <span>return</span> <span>a</span> <span>+</span> <span>b</span>  <span># 动态类型的优势，a 和 b 也可以是字符串</span>


<span>def</span><span>add_no_swap</span><span>(</span><span>a</span><span>,</span> <span>b</span><span>):</span>
    <span>print</span><span>(</span><span>"in func #1:"</span><span>,</span> <span>id</span><span>(</span><span>a</span><span>),</span> <span>id</span><span>(</span><span>b</span><span>))</span>
    <span>a</span> <span>+=</span> <span>b</span>
    <span>b</span><span>,</span> <span>a</span> <span>=</span> <span>a</span><span>,</span> <span>b</span>
    <span>print</span><span>(</span><span>"in func #2:"</span><span>,</span> <span>id</span><span>(</span><span>a</span><span>),</span> <span>id</span><span>(</span><span>b</span><span>))</span>  <span># a, b 已交换</span>
    <span>return</span> <span>a</span><span>,</span> <span>b</span>  <span># 返回多个值，其实就是返回元组，可以拆包接收</span>


<span>lst1</span> <span>=</span> <span>[</span><span>1</span><span>,</span> <span>2</span><span>]</span>
<span>lst2</span> <span>=</span> <span>[</span><span>3</span><span>,</span> <span>4</span><span>]</span>
<span>print</span><span>(</span><span>"outside func #1:"</span><span>,</span> <span>id</span><span>(</span><span>lst1</span><span>),</span> <span>id</span><span>(</span><span>lst2</span><span>))</span>
<span>add_no_swap</span><span>(</span><span>lst1</span><span>,</span> <span>lst2</span><span>)</span>
<span># 函数外 lst1, lst2 并未交换</span>
<span>print</span><span>(</span><span>"outside func #2:"</span><span>,</span> <span>id</span><span>(</span><span>lst1</span><span>),</span> <span>id</span><span>(</span><span>lst2</span><span>))</span>
<span># 不过值确实已经改变</span>
<span>print</span><span>(</span><span>lst1</span><span>,</span> <span>lst2</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

#### 默认参数

Python 中函数的参数非常灵活，有关键字参数、可变参数等，但在算法竞赛中这些特性的用处并不是很大，这里只介绍一下默认参数，因为 C++ 中也有默认参数，且在 Python 中使用默认参数很有可能遇到坑。

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span></pre></div></td><td><div><pre><code><span>def</span><span>append_to</span><span>(</span><span>element</span><span>,</span> <span>to</span><span>=</span><span>[]):</span>
    <span>to</span><span>.</span><span>append</span><span>(</span><span>element</span><span>)</span>
    <span>return</span> <span>to</span>


<span>lst1</span> <span>=</span> <span>append_to</span><span>(</span><span>12</span><span>)</span>
<span>lst2</span> <span>=</span> <span>append_to</span><span>(</span><span>42</span><span>)</span>
<span>print</span><span>(</span><span>lst1</span><span>,</span> <span>lst2</span><span>)</span>

<span># 你可能以为输出是 [12] [42]</span>
<span># 但运行结果其实是 [12] [12, 42]</span>


<span># 这是因为默认参数的值仅仅在函数定义的时候赋值一次</span>
<span># 默认参数的值应该是不可变对象，使用 None 占位是一种最佳实践</span>
<span>def</span><span>append_to</span><span>(</span><span>element</span><span>,</span> <span>to</span><span>=</span><span>None</span><span>):</span>
    <span>if</span> <span>to</span> <span>is</span> <span>None</span><span>:</span>
        <span>to</span> <span>=</span> <span>[]</span>
    <span>to</span><span>.</span><span>append</span><span>(</span><span>element</span><span>)</span>
    <span>return</span> <span>to</span>
</code></pre></div></td></tr></tbody></table>

#### 类型标注

Python 是一个动态类型检查的语言，以灵活但隐式的方式处理类型，Python 解释器仅仅在运行时检查类型是否正确，并且允许在运行时改变变量类型，俗话说「动态类型一时爽，代码重构火葬场」，程序中的一些错误可能在运行时才会暴露：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>if</span> <span>False</span><span>:</span>
<span>... </span>    <span>1</span> <span>+</span> <span>"two"</span>  <span># This line never runs, so no TypeError is raised</span>
<span>... </span><span>else</span><span>:</span>
<span>... </span>    <span>1</span> <span>+</span> <span>2</span>
<span>...</span>
<span>3</span>

<span>&gt;&gt;&gt; </span><span>1</span> <span>+</span> <span>"two"</span>  <span># Now this is type checked, and a TypeError is raised</span>
<span>TypeError: unsupported operand type(s) for +: 'int' and 'str'</span>
</code></pre></div></td></tr></tbody></table>

Python 3.5 后引入了类型标注，允许设置函数参数和返回值的类型，但只是作为提示，并没有实际的限制作用，需要静态检查工具才能排除这类错误（例如 [PyCharm](https://www.jetbrains.com/pycharm/) 和 [Mypy](http://mypy-lang.org/)），所以显得有些鸡肋，对于 OIer 来说更是只需了解，可按如下方式对函数的参数和返回值设置类型标注：

<table><tbody><tr><td></td><td><div><pre><code><span>def</span><span>headline</span><span>(</span>
    <span>text</span><span>,</span>  <span># type: str</span>
    <span>width</span><span>=</span><span>80</span><span>,</span>  <span># type: int</span>
    <span>fill_char</span><span>=</span><span>"-"</span><span>,</span>  <span># type: str</span>
<span>):</span>  <span># type: (...) -&gt; str</span>
    <span>return</span> <span>f</span><span>"</span><span>{</span><span>text</span><span>.</span><span>title</span><span>()</span><span>}</span><span>"</span><span>.</span><span>center</span><span>(</span><span>width</span><span>,</span> <span>fill_char</span><span>)</span>


<span>print</span><span>(</span><span>headline</span><span>(</span><span>"type comments work"</span><span>,</span> <span>width</span><span>=</span><span>40</span><span>))</span>
</code></pre></div></td></tr></tbody></table>

除了函数参数，变量也是可以类型标注的，你可以通过调用 `__annotations__` 来查看函数中所有的类型标注。变量类型标注赋予了 Python 静态语言的性质，即声明与赋值分离：

<table><tbody><tr><td></td><td><div><pre><code><span>&gt;&gt;&gt; </span><span>nothing</span><span>:</span> <span>str</span>
<span>&gt;&gt;&gt; </span><span>nothing</span>
<span>NameError: name 'nothing' is not defined</span>

<span>&gt;&gt;&gt; </span><span>__annotations__</span>
<span>{'nothing': &lt;class 'str'&gt;}</span>
</code></pre></div></td></tr></tbody></table>

## 装饰器

装饰器是一个函数，接受一个函数或方法作为其唯一的参数，并返回一个新函数或方法，其中整合了修饰后的函数或方法，并附带了一些额外的功能。简而言之，可以在不修改函数代码的情况下，增加函数的功能。相关知识可以参考 [官方文档](https://docs.python.org/3/glossary.html#term-decorator)。

部分装饰器在竞赛中非常实用，比如 [`lru_cache`](https://docs.python.org/3/library/functools.html#functools.lru_cache)，可以为函数自动增加记忆化的能力，在递归算法中非常实用：

`@lru_cache(maxsize=128,typed=False)`

*   传入的参数有 2 个：`maxsize` 和 `typed`，如果不传则 `maxsize` 的默认值为 128，`typed` 的默认值为 `False`。
*   其中 `maxsize` 参数表示的是 LRU 缓存的容量，即被装饰的方法的最大可缓存结果的数量。如果该参数值为 128，则表示被装饰方法最多可缓存 128 个返回结果；如果 `maxsize` 传入为 `None` 则表示可以缓存无限个结果。
*   如果 `typed` 设置为 `True`，不同类型的函数参数将被分别缓存，例如，`f(3)` 和 `f(3.0)` 会缓存两次。

以下是使用 `lru_cache` 优化计算斐波那契数列的例子：

<table><tbody><tr><td></td><td><div><pre><code><span>@lru_cache</span><span>(</span><span>maxsize</span><span>=</span><span>None</span><span>)</span>
<span>def</span><span>fib</span><span>(</span><span>n</span><span>):</span>
    <span>if</span> <span>n</span> <span>&lt;</span> <span>2</span><span>:</span>
        <span>return</span> <span>n</span>
    <span>return</span> <span>fib</span><span>(</span><span>n</span> <span>-</span> <span>1</span><span>)</span> <span>+</span> <span>fib</span><span>(</span><span>n</span> <span>-</span> <span>2</span><span>)</span>
</code></pre></div></td></tr></tbody></table>

## 常用内置库

在这里介绍一些写算法可能用得到的内置库，具体用法可以自行搜索或者阅读 [官方文档](https://docs.python.org/3/library/index.html)。

## 从例题对比 C++ 与 Python

[例题 洛谷 P4779【模板】单源最短路径（标准版）](https://www.luogu.com.cn/problem/P4779)

给定一个 n(1≤n≤105) 个点、m(1≤m≤2×105) 条有向边的带非负权图，请你计算从 s 出发，到每个点的距离。数据保证能从 s 出发到任意点。

### 声明常量

<table><tbody><tr><td></td><td><div><pre><code><span>#include</span><span>&lt;cstdio&gt;</span>
<span>#include</span><span>&lt;cstring&gt;</span>
<span>#include</span><span>&lt;queue&gt;</span>
<span>#include</span><span>&lt;vector&gt;</span>
<span>using</span><span>namespace</span><span>std</span><span>;</span>
<span>constexpr</span><span>int</span><span>N</span><span>=</span><span>1e5</span><span>+</span><span>5</span><span>,</span><span>M</span><span>=</span><span>2e5</span><span>+</span><span>5</span><span>;</span>
</code></pre></div></td></tr></tbody></table>

<table><tbody><tr><td></td><td><div><pre><code><span>try</span><span>:</span>  <span># 引入优先队列模块</span>
    <span>import</span><span>Queue</span><span>as</span><span>pq</span>  <span># python version &lt; 3.0</span>
<span>except</span> <span>ImportError</span><span>:</span>
    <span>import</span><span>queue</span><span>as</span><span>pq</span>  <span># python3.*</span>

<span>N</span> <span>=</span> <span>int</span><span>(</span><span>1e5</span> <span>+</span> <span>5</span><span>)</span>
<span>M</span> <span>=</span> <span>int</span><span>(</span><span>2e5</span> <span>+</span> <span>5</span><span>)</span>
<span>INF</span> <span>=</span> <span>0x3F3F3F3F</span>
</code></pre></div></td></tr></tbody></table>

### 声明前向星结构体和其它变量

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span></pre></div></td><td><div><pre><code tabindex="0"><span>struct</span><span>qxx</span><span>{</span>
<span>int</span><span>nex</span><span>,</span><span>t</span><span>,</span><span>v</span><span>;</span>
<span>};</span>

<span>qxx</span><span>e</span><span>[</span><span>M</span><span>];</span>
<span>int</span><span>h</span><span>[</span><span>N</span><span>],</span><span>cnt</span><span>;</span>

<span>void</span><span>add_path</span><span>(</span><span>int</span><span>f</span><span>,</span><span>int</span><span>t</span><span>,</span><span>int</span><span>v</span><span>)</span><span>{</span><span>e</span><span>[</span><span>++</span><span>cnt</span><span>]</span><span>=</span><span>qxx</span><span>{</span><span>h</span><span>[</span><span>f</span><span>],</span><span>t</span><span>,</span><span>v</span><span>},</span><span>h</span><span>[</span><span>f</span><span>]</span><span>=</span><span>cnt</span><span>;</span><span>}</span>

<span>using</span><span>pii</span><span>=</span><span>pair</span><span>&lt;</span><span>int</span><span>,</span><span>int</span><span>&gt;</span><span>;</span>
<span>priority_queue</span><span>&lt;</span><span>pii</span><span>,</span><span>vector</span><span>&lt;</span><span>pii</span><span>&gt;</span><span>,</span><span>greater</span><span>&lt;</span><span>pii</span><span>&gt;&gt;</span><span>q</span><span>;</span>
<span>int</span><span>dist</span><span>[</span><span>N</span><span>];</span>
</code></pre></div></td></tr></tbody></table>

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span>
<span>23</span>
<span>24</span>
<span>25</span></pre></div></td><td><div><pre><code><span>class</span><span>qxx</span><span>:</span>  <span># 前向星类（结构体）</span>
    <span>def</span><span>__init__</span><span>(</span><span>self</span><span>):</span>
        <span>self</span><span>.</span><span>nex</span> <span>=</span> <span>0</span>
        <span>self</span><span>.</span><span>t</span> <span>=</span> <span>0</span>
        <span>self</span><span>.</span><span>v</span> <span>=</span> <span>0</span>


<span>e</span> <span>=</span> <span>[</span><span>qxx</span><span>()</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>M</span><span>)]</span>  <span># 链表</span>
<span>h</span> <span>=</span> <span>[</span><span>0</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>N</span><span>)]</span>
<span>cnt</span> <span>=</span> <span>0</span>

<span>dist</span> <span>=</span> <span>[</span><span>INF</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>N</span><span>)]</span>
<span>q</span> <span>=</span> <span>pq</span><span>.</span><span>PriorityQueue</span><span>()</span>  <span># 定义优先队列，默认第一元小根堆</span>


<span>def</span><span>add_path</span><span>(</span><span>f</span><span>,</span> <span>t</span><span>,</span> <span>v</span><span>):</span>  <span># 在前向星中加边</span>
    <span># 如果要修改全局变量，要使用 global 来声明</span>
    <span>global</span> <span>cnt</span><span>,</span> <span>e</span><span>,</span> <span>h</span>
    <span># 调试时的输出语句，多个变量使用元组</span>
    <span># print("add_path(%d,%d,%d)" % (f,t,v))</span>
    <span>cnt</span> <span>+=</span> <span>1</span>
    <span>e</span><span>[</span><span>cnt</span><span>]</span><span>.</span><span>nex</span> <span>=</span> <span>h</span><span>[</span><span>f</span><span>]</span>
    <span>e</span><span>[</span><span>cnt</span><span>]</span><span>.</span><span>t</span> <span>=</span> <span>t</span>
    <span>e</span><span>[</span><span>cnt</span><span>]</span><span>.</span><span>v</span> <span>=</span> <span>v</span>
    <span>h</span><span>[</span><span>f</span><span>]</span> <span>=</span> <span>cnt</span>
</code></pre></div></td></tr></tbody></table>

### Dijkstra 算法

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span></pre></div></td><td><div><pre><code><span>void</span><span>dijkstra</span><span>(</span><span>int</span><span>s</span><span>)</span><span>{</span>
<span>memset</span><span>(</span><span>dist</span><span>,</span><span>0x3f</span><span>,</span><span>sizeof</span><span>(</span><span>dist</span><span>));</span>
<span>dist</span><span>[</span><span>s</span><span>]</span><span>=</span><span>0</span><span>,</span><span>q</span><span>.</span><span>push</span><span>(</span><span>make_pair</span><span>(</span><span>0</span><span>,</span><span>s</span><span>));</span>
<span>while</span><span>(</span><span>q</span><span>.</span><span>size</span><span>())</span><span>{</span>
<span>pii</span><span>u</span><span>=</span><span>q</span><span>.</span><span>top</span><span>();</span>
<span>q</span><span>.</span><span>pop</span><span>();</span>
<span>if</span><span>(</span><span>dist</span><span>[</span><span>u</span><span>.</span><span>second</span><span>]</span><span>&lt;</span><span>u</span><span>.</span><span>first</span><span>)</span><span>continue</span><span>;</span>
<span>for</span><span>(</span><span>int</span><span>i</span><span>=</span><span>h</span><span>[</span><span>u</span><span>.</span><span>second</span><span>];</span><span>i</span><span>;</span><span>i</span><span>=</span><span>e</span><span>[</span><span>i</span><span>].</span><span>nex</span><span>)</span><span>{</span>
<span>const</span><span>int</span><span>&amp;</span><span>v</span><span>=</span><span>e</span><span>[</span><span>i</span><span>].</span><span>t</span><span>,</span><span>&amp;</span><span>w</span><span>=</span><span>e</span><span>[</span><span>i</span><span>].</span><span>v</span><span>;</span>
<span>if</span><span>(</span><span>dist</span><span>[</span><span>v</span><span>]</span><span>&lt;=</span><span>dist</span><span>[</span><span>u</span><span>.</span><span>second</span><span>]</span><span>+</span><span>w</span><span>)</span><span>continue</span><span>;</span>
<span>dist</span><span>[</span><span>v</span><span>]</span><span>=</span><span>dist</span><span>[</span><span>u</span><span>.</span><span>second</span><span>]</span><span>+</span><span>w</span><span>;</span>
<span>q</span><span>.</span><span>push</span><span>(</span><span>make_pair</span><span>(</span><span>dist</span><span>[</span><span>v</span><span>],</span><span>v</span><span>));</span>
<span>}</span>
<span>}</span>
<span>}</span>
</code></pre></div></td></tr></tbody></table>

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span></pre></div></td><td><div><pre><code><span>def</span><span>nextedgeid</span><span>(</span><span>u</span><span>):</span>  <span># 生成器，可以用在 for 循环里</span>
    <span>i</span> <span>=</span> <span>h</span><span>[</span><span>u</span><span>]</span>
    <span>while</span> <span>i</span><span>:</span>
        <span>yield</span> <span>i</span>
        <span>i</span> <span>=</span> <span>e</span><span>[</span><span>i</span><span>]</span><span>.</span><span>nex</span>


<span>def</span><span>dijkstra</span><span>(</span><span>s</span><span>):</span>
    <span>dist</span><span>[</span><span>s</span><span>]</span> <span>=</span> <span>0</span>
    <span>q</span><span>.</span><span>put</span><span>((</span><span>0</span><span>,</span> <span>s</span><span>))</span>
    <span>while</span> <span>not</span> <span>q</span><span>.</span><span>empty</span><span>():</span>
        <span>u</span> <span>=</span> <span>q</span><span>.</span><span>get</span><span>()</span>  <span># get 函数会顺便删除堆中对应的元素</span>
        <span>if</span> <span>dist</span><span>[</span><span>u</span><span>[</span><span>1</span><span>]]</span> <span>&lt;</span> <span>u</span><span>[</span><span>0</span><span>]:</span>
            <span>continue</span>
        <span>for</span> <span>i</span> <span>in</span> <span>nextedgeid</span><span>(</span><span>u</span><span>[</span><span>1</span><span>]):</span>
            <span>v</span> <span>=</span> <span>e</span><span>[</span><span>i</span><span>]</span><span>.</span><span>t</span>
            <span>w</span> <span>=</span> <span>e</span><span>[</span><span>i</span><span>]</span><span>.</span><span>v</span>
            <span>if</span> <span>dist</span><span>[</span><span>v</span><span>]</span> <span>&lt;=</span> <span>dist</span><span>[</span><span>u</span><span>[</span><span>1</span><span>]]</span> <span>+</span> <span>w</span><span>:</span>
                <span>continue</span>
            <span>dist</span><span>[</span><span>v</span><span>]</span> <span>=</span> <span>dist</span><span>[</span><span>u</span><span>[</span><span>1</span><span>]]</span> <span>+</span> <span>w</span>
            <span>q</span><span>.</span><span>put</span><span>((</span><span>dist</span><span>[</span><span>v</span><span>],</span> <span>v</span><span>))</span>
</code></pre></div></td></tr></tbody></table>

### 主函数

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code><span>int</span><span>n</span><span>,</span><span>m</span><span>,</span><span>s</span><span>;</span>

<span>int</span><span>main</span><span>()</span><span>{</span>
<span>scanf</span><span>(</span><span>"%d%d%d"</span><span>,</span><span>&amp;</span><span>n</span><span>,</span><span>&amp;</span><span>m</span><span>,</span><span>&amp;</span><span>s</span><span>);</span>
<span>for</span><span>(</span><span>int</span><span>i</span><span>=</span><span>1</span><span>;</span><span>i</span><span>&lt;=</span><span>m</span><span>;</span><span>i</span><span>++</span><span>)</span><span>{</span>
<span>int</span><span>u</span><span>,</span><span>v</span><span>,</span><span>w</span><span>;</span>
<span>scanf</span><span>(</span><span>"%d%d%d"</span><span>,</span><span>&amp;</span><span>u</span><span>,</span><span>&amp;</span><span>v</span><span>,</span><span>&amp;</span><span>w</span><span>);</span>
<span>add_path</span><span>(</span><span>u</span><span>,</span><span>v</span><span>,</span><span>w</span><span>);</span>
<span>}</span>
<span>dijkstra</span><span>(</span><span>s</span><span>);</span>
<span>for</span><span>(</span><span>int</span><span>i</span><span>=</span><span>1</span><span>;</span><span>i</span><span>&lt;=</span><span>n</span><span>;</span><span>i</span><span>++</span><span>)</span><span>printf</span><span>(</span><span>"%d "</span><span>,</span><span>dist</span><span>[</span><span>i</span><span>]);</span>
<span>return</span><span>0</span><span>;</span>
<span>}</span>
</code></pre></div></td></tr></tbody></table>

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span></pre></div></td><td><div><pre><code><span>if</span> <span>__name__</span> <span>==</span> <span>"__main__"</span><span>:</span>
    <span># 一行读入多个整数。注意它会把整行都读进来</span>
    <span>n</span><span>,</span> <span>m</span><span>,</span> <span>s</span> <span>=</span> <span>map</span><span>(</span><span>int</span><span>,</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>())</span>
    <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>m</span><span>):</span>
        <span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span> <span>=</span> <span>map</span><span>(</span><span>int</span><span>,</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>())</span>
        <span>add_path</span><span>(</span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span><span>)</span>

    <span>dijkstra</span><span>(</span><span>s</span><span>)</span>
    
    <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>1</span><span>,</span> <span>n</span> <span>+</span> <span>1</span><span>):</span>
        <span>print</span><span>(</span><span>dist</span><span>[</span><span>i</span><span>],</span> <span>end</span><span>=</span><span>" "</span><span>)</span>
    
    <span>print</span><span>()</span>
</code></pre></div></td></tr></tbody></table>

### 完整代码

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span>
<span>23</span>
<span>24</span>
<span>25</span>
<span>26</span>
<span>27</span>
<span>28</span>
<span>29</span>
<span>30</span>
<span>31</span>
<span>32</span>
<span>33</span>
<span>34</span>
<span>35</span>
<span>36</span>
<span>37</span>
<span>38</span>
<span>39</span>
<span>40</span>
<span>41</span>
<span>42</span>
<span>43</span>
<span>44</span>
<span>45</span>
<span>46</span>
<span>47</span>
<span>48</span>
<span>49</span></pre></div></td><td><div><pre><code tabindex="0"><span>#include</span><span>&lt;cstdio&gt;</span>
<span>#include</span><span>&lt;cstring&gt;</span>
<span>#include</span><span>&lt;queue&gt;</span>
<span>#include</span><span>&lt;vector&gt;</span>
<span>using</span><span>namespace</span><span>std</span><span>;</span>
<span>constexpr</span><span>int</span><span>N</span><span>=</span><span>1e5</span><span>+</span><span>5</span><span>,</span><span>M</span><span>=</span><span>2e5</span><span>+</span><span>5</span><span>;</span>

<span>struct</span><span>qxx</span><span>{</span>
<span>int</span><span>nex</span><span>,</span><span>t</span><span>,</span><span>v</span><span>;</span>
<span>};</span>

<span>qxx</span><span>e</span><span>[</span><span>M</span><span>];</span>
<span>int</span><span>h</span><span>[</span><span>N</span><span>],</span><span>cnt</span><span>;</span>

<span>void</span><span>add_path</span><span>(</span><span>int</span><span>f</span><span>,</span><span>int</span><span>t</span><span>,</span><span>int</span><span>v</span><span>)</span><span>{</span><span>e</span><span>[</span><span>++</span><span>cnt</span><span>]</span><span>=</span><span>qxx</span><span>{</span><span>h</span><span>[</span><span>f</span><span>],</span><span>t</span><span>,</span><span>v</span><span>},</span><span>h</span><span>[</span><span>f</span><span>]</span><span>=</span><span>cnt</span><span>;</span><span>}</span>

<span>using</span><span>pii</span><span>=</span><span>pair</span><span>&lt;</span><span>int</span><span>,</span><span>int</span><span>&gt;</span><span>;</span>
<span>priority_queue</span><span>&lt;</span><span>pii</span><span>,</span><span>vector</span><span>&lt;</span><span>pii</span><span>&gt;</span><span>,</span><span>greater</span><span>&lt;</span><span>pii</span><span>&gt;&gt;</span><span>q</span><span>;</span>
<span>int</span><span>dist</span><span>[</span><span>N</span><span>];</span>

<span>void</span><span>dijkstra</span><span>(</span><span>int</span><span>s</span><span>)</span><span>{</span>
<span>memset</span><span>(</span><span>dist</span><span>,</span><span>0x3f</span><span>,</span><span>sizeof</span><span>(</span><span>dist</span><span>));</span>
<span>dist</span><span>[</span><span>s</span><span>]</span><span>=</span><span>0</span><span>,</span><span>q</span><span>.</span><span>push</span><span>(</span><span>make_pair</span><span>(</span><span>0</span><span>,</span><span>s</span><span>));</span>
<span>while</span><span>(</span><span>q</span><span>.</span><span>size</span><span>())</span><span>{</span>
<span>pii</span><span>u</span><span>=</span><span>q</span><span>.</span><span>top</span><span>();</span>
<span>q</span><span>.</span><span>pop</span><span>();</span>
<span>if</span><span>(</span><span>dist</span><span>[</span><span>u</span><span>.</span><span>second</span><span>]</span><span>&lt;</span><span>u</span><span>.</span><span>first</span><span>)</span><span>continue</span><span>;</span>
<span>for</span><span>(</span><span>int</span><span>i</span><span>=</span><span>h</span><span>[</span><span>u</span><span>.</span><span>second</span><span>];</span><span>i</span><span>;</span><span>i</span><span>=</span><span>e</span><span>[</span><span>i</span><span>].</span><span>nex</span><span>)</span><span>{</span>
<span>const</span><span>int</span><span>&amp;</span><span>v</span><span>=</span><span>e</span><span>[</span><span>i</span><span>].</span><span>t</span><span>,</span><span>&amp;</span><span>w</span><span>=</span><span>e</span><span>[</span><span>i</span><span>].</span><span>v</span><span>;</span>
<span>if</span><span>(</span><span>dist</span><span>[</span><span>v</span><span>]</span><span>&lt;=</span><span>dist</span><span>[</span><span>u</span><span>.</span><span>second</span><span>]</span><span>+</span><span>w</span><span>)</span><span>continue</span><span>;</span>
<span>dist</span><span>[</span><span>v</span><span>]</span><span>=</span><span>dist</span><span>[</span><span>u</span><span>.</span><span>second</span><span>]</span><span>+</span><span>w</span><span>;</span>
<span>q</span><span>.</span><span>push</span><span>(</span><span>make_pair</span><span>(</span><span>dist</span><span>[</span><span>v</span><span>],</span><span>v</span><span>));</span>
<span>}</span>
<span>}</span>
<span>}</span>

<span>int</span><span>n</span><span>,</span><span>m</span><span>,</span><span>s</span><span>;</span>

<span>int</span><span>main</span><span>()</span><span>{</span>
<span>scanf</span><span>(</span><span>"%d%d%d"</span><span>,</span><span>&amp;</span><span>n</span><span>,</span><span>&amp;</span><span>m</span><span>,</span><span>&amp;</span><span>s</span><span>);</span>
<span>for</span><span>(</span><span>int</span><span>i</span><span>=</span><span>1</span><span>;</span><span>i</span><span>&lt;=</span><span>m</span><span>;</span><span>i</span><span>++</span><span>)</span><span>{</span>
<span>int</span><span>u</span><span>,</span><span>v</span><span>,</span><span>w</span><span>;</span>
<span>scanf</span><span>(</span><span>"%d%d%d"</span><span>,</span><span>&amp;</span><span>u</span><span>,</span><span>&amp;</span><span>v</span><span>,</span><span>&amp;</span><span>w</span><span>);</span>
<span>add_path</span><span>(</span><span>u</span><span>,</span><span>v</span><span>,</span><span>w</span><span>);</span>
<span>}</span>
<span>dijkstra</span><span>(</span><span>s</span><span>);</span>
<span>for</span><span>(</span><span>int</span><span>i</span><span>=</span><span>1</span><span>;</span><span>i</span><span>&lt;=</span><span>n</span><span>;</span><span>i</span><span>++</span><span>)</span><span>printf</span><span>(</span><span>"%d "</span><span>,</span><span>dist</span><span>[</span><span>i</span><span>]);</span>
<span>return</span><span>0</span><span>;</span>
<span>}</span>
</code></pre></div></td></tr></tbody></table>

<table><tbody><tr><td><div><pre><span> 1</span>
<span> 2</span>
<span> 3</span>
<span> 4</span>
<span> 5</span>
<span> 6</span>
<span> 7</span>
<span> 8</span>
<span> 9</span>
<span>10</span>
<span>11</span>
<span>12</span>
<span>13</span>
<span>14</span>
<span>15</span>
<span>16</span>
<span>17</span>
<span>18</span>
<span>19</span>
<span>20</span>
<span>21</span>
<span>22</span>
<span>23</span>
<span>24</span>
<span>25</span>
<span>26</span>
<span>27</span>
<span>28</span>
<span>29</span>
<span>30</span>
<span>31</span>
<span>32</span>
<span>33</span>
<span>34</span>
<span>35</span>
<span>36</span>
<span>37</span>
<span>38</span>
<span>39</span>
<span>40</span>
<span>41</span>
<span>42</span>
<span>43</span>
<span>44</span>
<span>45</span>
<span>46</span>
<span>47</span>
<span>48</span>
<span>49</span>
<span>50</span>
<span>51</span>
<span>52</span>
<span>53</span>
<span>54</span>
<span>55</span>
<span>56</span>
<span>57</span>
<span>58</span>
<span>59</span>
<span>60</span>
<span>61</span>
<span>62</span>
<span>63</span>
<span>64</span>
<span>65</span>
<span>66</span>
<span>67</span>
<span>68</span>
<span>69</span>
<span>70</span>
<span>71</span>
<span>72</span>
<span>73</span>
<span>74</span>
<span>75</span>
<span>76</span></pre></div></td><td><div><pre><code><span>try</span><span>:</span>  <span># 引入优先队列模块</span>
    <span>import</span><span>Queue</span><span>as</span><span>pq</span>  <span># python version &lt; 3.0</span>
<span>except</span> <span>ImportError</span><span>:</span>
    <span>import</span><span>queue</span><span>as</span><span>pq</span>  <span># python3.*</span>

<span>N</span> <span>=</span> <span>int</span><span>(</span><span>1e5</span> <span>+</span> <span>5</span><span>)</span>
<span>M</span> <span>=</span> <span>int</span><span>(</span><span>2e5</span> <span>+</span> <span>5</span><span>)</span>
<span>INF</span> <span>=</span> <span>0x3F3F3F3F</span>


<span>class</span><span>qxx</span><span>:</span>  <span># 前向星类（结构体）</span>
    <span>def</span><span>__init__</span><span>(</span><span>self</span><span>):</span>
        <span>self</span><span>.</span><span>nex</span> <span>=</span> <span>0</span>
        <span>self</span><span>.</span><span>t</span> <span>=</span> <span>0</span>
        <span>self</span><span>.</span><span>v</span> <span>=</span> <span>0</span>


<span>e</span> <span>=</span> <span>[</span><span>qxx</span><span>()</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>M</span><span>)]</span>  <span># 链表</span>
<span>h</span> <span>=</span> <span>[</span><span>0</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>N</span><span>)]</span>
<span>cnt</span> <span>=</span> <span>0</span>

<span>dist</span> <span>=</span> <span>[</span><span>INF</span> <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>N</span><span>)]</span>
<span>q</span> <span>=</span> <span>pq</span><span>.</span><span>PriorityQueue</span><span>()</span>  <span># 定义优先队列，默认第一元小根堆</span>


<span>def</span><span>add_path</span><span>(</span><span>f</span><span>,</span> <span>t</span><span>,</span> <span>v</span><span>):</span>  <span># 在前向星中加边</span>
    <span># 如果要修改全局变量，要使用 global 来声名</span>
    <span>global</span> <span>cnt</span><span>,</span> <span>e</span><span>,</span> <span>h</span>
    <span># 调试时的输出语句，多个变量使用元组</span>
    <span># print("add_path(%d,%d,%d)" % (f,t,v))</span>
    <span>cnt</span> <span>+=</span> <span>1</span>
    <span>e</span><span>[</span><span>cnt</span><span>]</span><span>.</span><span>nex</span> <span>=</span> <span>h</span><span>[</span><span>f</span><span>]</span>
    <span>e</span><span>[</span><span>cnt</span><span>]</span><span>.</span><span>t</span> <span>=</span> <span>t</span>
    <span>e</span><span>[</span><span>cnt</span><span>]</span><span>.</span><span>v</span> <span>=</span> <span>v</span>
    <span>h</span><span>[</span><span>f</span><span>]</span> <span>=</span> <span>cnt</span>


<span>def</span><span>nextedgeid</span><span>(</span><span>u</span><span>):</span>  <span># 生成器，可以用在 for 循环里</span>
    <span>i</span> <span>=</span> <span>h</span><span>[</span><span>u</span><span>]</span>
    <span>while</span> <span>i</span><span>:</span>
        <span>yield</span> <span>i</span>
        <span>i</span> <span>=</span> <span>e</span><span>[</span><span>i</span><span>]</span><span>.</span><span>nex</span>


<span>def</span><span>dijkstra</span><span>(</span><span>s</span><span>):</span>
    <span>dist</span><span>[</span><span>s</span><span>]</span> <span>=</span> <span>0</span>
    <span>q</span><span>.</span><span>put</span><span>((</span><span>0</span><span>,</span> <span>s</span><span>))</span>
    <span>while</span> <span>not</span> <span>q</span><span>.</span><span>empty</span><span>():</span>
        <span>u</span> <span>=</span> <span>q</span><span>.</span><span>get</span><span>()</span>
        <span>if</span> <span>dist</span><span>[</span><span>u</span><span>[</span><span>1</span><span>]]</span> <span>&lt;</span> <span>u</span><span>[</span><span>0</span><span>]:</span>
            <span>continue</span>
        <span>for</span> <span>i</span> <span>in</span> <span>nextedgeid</span><span>(</span><span>u</span><span>[</span><span>1</span><span>]):</span>
            <span>v</span> <span>=</span> <span>e</span><span>[</span><span>i</span><span>]</span><span>.</span><span>t</span>
            <span>w</span> <span>=</span> <span>e</span><span>[</span><span>i</span><span>]</span><span>.</span><span>v</span>
            <span>if</span> <span>dist</span><span>[</span><span>v</span><span>]</span> <span>&lt;=</span> <span>dist</span><span>[</span><span>u</span><span>[</span><span>1</span><span>]]</span> <span>+</span> <span>w</span><span>:</span>
                <span>continue</span>
            <span>dist</span><span>[</span><span>v</span><span>]</span> <span>=</span> <span>dist</span><span>[</span><span>u</span><span>[</span><span>1</span><span>]]</span> <span>+</span> <span>w</span>
            <span>q</span><span>.</span><span>put</span><span>((</span><span>dist</span><span>[</span><span>v</span><span>],</span> <span>v</span><span>))</span>


<span># 如果你直接运行这个 Python 代码（不是模块调用什么的）就执行命令</span>
<span>if</span> <span>__name__</span> <span>==</span> <span>"__main__"</span><span>:</span>
    <span># 一行读入多个整数。注意它会把整行都读进来</span>
    <span>n</span><span>,</span> <span>m</span><span>,</span> <span>s</span> <span>=</span> <span>map</span><span>(</span><span>int</span><span>,</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>())</span>
    <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>m</span><span>):</span>
        <span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span> <span>=</span> <span>map</span><span>(</span><span>int</span><span>,</span> <span>input</span><span>()</span><span>.</span><span>split</span><span>())</span>
        <span>add_path</span><span>(</span><span>u</span><span>,</span> <span>v</span><span>,</span> <span>w</span><span>)</span>

    <span>dijkstra</span><span>(</span><span>s</span><span>)</span>
    
    <span>for</span> <span>i</span> <span>in</span> <span>range</span><span>(</span><span>1</span><span>,</span> <span>n</span> <span>+</span> <span>1</span><span>):</span>
        <span># 两种输出语法都是可以用的</span>
        <span>print</span><span>(</span><span>"</span><span>{}</span><span>"</span><span>.</span><span>format</span><span>(</span><span>dist</span><span>[</span><span>i</span><span>]),</span> <span>end</span><span>=</span><span>" "</span><span>)</span>
        <span># print("%d" % dist[i],end=' ')</span>
    
    <span>print</span><span>()</span>  <span># 结尾换行</span>
</code></pre></div></td></tr></tbody></table>

## 参考文档

1.  [Python Documentation](https://www.python.org/doc/)
2.  [Python 官方中文教程](https://docs.python.org/zh-cn/3/tutorial/)
3.  [Learn Python3 In Y Minutes](https://learnxinyminutes.com/docs/python3/)
4.  [Real Python Tutorials](https://realpython.com/)
5.  [廖雪峰的 Python 教程](https://www.liaoxuefeng.com/wiki/1016959663602400/)
6.  [GeeksforGeeks: Python Tutorials](https://www.geeksforgeeks.org/python-programming-language/)

## 参考资料和注释

> 本页面最近更新：2025/7/20 00:07:52，[更新历史](https://github.com/OI-wiki/OI-wiki/commits/master/docs/lang/python.md)发现错误？想一起完善？ [在 GitHub 上编辑此页！](https://oi-wiki.org/edit-landing/?ref=/lang/python.md "edit.link.title")本页面贡献者：[Ir1d](https://github.com/Ir1d), [abc1763613206](https://github.com/abc1763613206), [Enter-tainer](https://github.com/Enter-tainer), [Tiphereth-A](https://github.com/Tiphereth-A), [cmpute](https://github.com/cmpute), [ksyx](https://github.com/ksyx), [LovelyBuggies](https://github.com/LovelyBuggies), [countercurrent-time](https://github.com/countercurrent-time), [NachtgeistW](https://github.com/NachtgeistW), [shuzhouliu](https://github.com/shuzhouliu), [StudyingFather](https://github.com/StudyingFather), [chinggg](https://github.com/chinggg), [Early0v0](https://github.com/Early0v0), [H-J-Granger](https://github.com/H-J-Granger), [Henry-ZHR](https://github.com/Henry-ZHR), [sshwy](https://github.com/sshwy), [Suyun514](mailto:suyun514@qq.com), [billchenchina](https://github.com/billchenchina), [CoelacanthusHex](https://github.com/CoelacanthusHex), [F1shAndCat](https://github.com/F1shAndCat), [mgt](mailto:i@margatroid.xyz), [ouuan](https://github.com/ouuan), [ranwen](https://github.com/ranwen), [Rottenwooood](https://github.com/Rottenwooood), [AngelKitty](https://github.com/AngelKitty), [CCXXXI](https://github.com/CCXXXI), [ChungZH](https://github.com/ChungZH), [cjsoft](https://github.com/cjsoft), [diauweb](https://github.com/diauweb), [Dong Tsing-hsuen](mailto:68433824+alissa42@users.noreply.github.com), [ezoixx130](https://github.com/ezoixx130), [GekkaSaori](https://github.com/GekkaSaori), [Great-designer](https://github.com/Great-designer), [hensier](https://github.com/hensier), [HeRaNO](https://github.com/HeRaNO), [Hszzzx](https://github.com/Hszzzx), [imba-tjd](https://github.com/imba-tjd), [jiangmuran](https://github.com/jiangmuran), [Konano](https://github.com/Konano), [lingxier](https://github.com/lingxier), [Makkiy](https://github.com/Makkiy), [Marcythm](https://github.com/Marcythm), [minghu6](https://github.com/minghu6), [Mooos-MoSheng](https://github.com/Mooos-MoSheng), [P-Y-Y](https://github.com/P-Y-Y), [PotassiumWings](https://github.com/PotassiumWings), [SamZhangQingChuan](https://github.com/SamZhangQingChuan), [shawlleyw](https://github.com/shawlleyw), [SukkaW](https://github.com/SukkaW), [tLLWtG](https://github.com/tLLWtG), [weiyong1024](https://github.com/weiyong1024), [wineee](https://github.com/wineee), [wxh06](https://github.com/wxh06), [Xeonacid](https://github.com/Xeonacid), [yusancky](https://github.com/yusancky), [zyouxam](https://github.com/zyouxam), [zzjjbb](https://github.com/zzjjbb), [Dong Tsing-hsuen](https://github.com/Dong%20Tsing-hsuen), [GavinZhengOI](https://github.com/GavinZhengOI), [Gesrua](https://github.com/Gesrua), [kxccc](https://github.com/kxccc), [lychees](https://github.com/lychees), [mgt](https://github.com/mgt), [Niazye](https://github.com/Niazye), [Peanut-Tang](https://github.com/Peanut-Tang), [Suyun514](https://github.com/Suyun514), [TOMWT-qwq](https://github.com/TOMWT-qwq)本页面的全部内容在 **[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.zh) 和 [SATA](https://github.com/zTrix/sata-license)** 协议之条款下提供，附加条款亦可能应用