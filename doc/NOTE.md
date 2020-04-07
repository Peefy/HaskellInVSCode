
# Haskell In VS Code

## Haskell简介

Haskell是一种懒惰的函数式编程语言，由学术委员会于1980年代后期创建。

Hashkell特点：

* Statically typed 静态类型
* Purely functional 纯粹函数式
* Type inference 类型推断
* Concurrent 并发的
* Lazy     懒惰的
* Packages 包管理

Haskell是一个按照纯函数式编程思想创造的语言，支持静态类型、类型推断、惰性处理（推迟计算）、支持并发编程。

* 函数是一等公民的，也就是说，函数是可以与其他任何类型的值完全相同的方式使用的值。
* Haskell程序的含义集中在评估表达式而不是执行指令上。

Haskell表达式始终是引用透明的，即：

* 一切（变量，数据结构…）都是不可变的。
* 表达式永远不会有“副作用”（例如更新全局变量或在屏幕上打印）。
* 每次使用相同的参数调用相同的函数都会导致相同的输出。

每个Haskell表达式都有一个类型，并且所有类型都在编译时检查。带有类型错误的程序无法编译，无法运行。

Haskell类型系统的特点：

* 有助于理清思路并表达程序结​​构：编写Haskell程序的第一步通常是写下所有类型。因为Haskell的类型系统表现力强，所以这是一个不平凡的设计步骤，并且对阐明人们对程序的想法有极大的帮助。
* 用作文件形式：给定一个富有表现力的类型系统，即使只读过一个书面文档，只要查看一个函数的类型，它就会告诉很多有关该函数可能做什么以及如何使用的信息。
* 将运行时错误转换为编译时错误：能够预先修复错误比仅仅进行大量测试并希望达到最佳效果要好得多。“如果可以编译，它必须是正确的”在大多数情况下都是滑稽的（即使在类型正确的程序中，逻辑上仍然有可能出错），但是在Haskell中发生的情况要比其他语言多得多。

Haskell非常擅长抽象：参数多态性，高阶函数和类型类之类的功能都有助于对抗重复。

一个例子，如下的代码

```java
int acc = 0;
for ( int i = 0; i < lst.length; i++ ) {
  acc = acc + 3 * lst[i];
}
```

可以用Haskell写为：

```hs
sum (map (3*) lst)
```

## Hashell声明和变量

```hs
x :: Int
x = 3

-- Note that normal (non-literate) comments are preceded by two hyphens
{- or enclosed
   in curly brace/hyphen pairs. -}
```

上面的代码声明了一个x类型为type 的变量Int（`::`表示为“具有类型”），并声明了x的值为3。请注意，这将是x永远的值（至少在此特定程序中）。此后的值x以后不能更改。

换句话说，`=`它并不像许多其他语言那样表示“赋值”。相反，它=表示定义，就像在数学中一样。也就是说，`x = 4`不应该被解读为“ x赋值为4”或“分配4到x”，而是“ x被定义为 4 ” 

## Hashell基本类型

* **整型**-在64位机器上，取值范围为 $\pm 2^{63}$ 

```hs
i :: Int
i = -78

biggestInt, smallestInt :: Int
biggestInt  = maxBound
smallestInt = minBound

-- Arbitrary-precision integers
n :: Integer
n = 1234567890987654321987340982334987349872349874534

reallyBig :: Integer
reallyBig = 2^(2^(2^(2^2)))

numDigits :: Int
numDigits = length (show reallyBig)
```

* **浮点型**-

```hs
-- Double-precision floating point
d1, d2 :: Double
d1 = 4.5387
d2 = 6.2831e-4
```

* **布尔型**-

```hs
-- Booleans
b1, b2 :: Bool
b1 = True
b2 = False
```

* **字符和字符串**

```hs
-- Unicode characters
c1, c2, c3 :: Char
c1 = 'x'
c2 = 'Ø'
c3 = 'ダ'

-- Strings are lists of characters with special syntax
s :: String
s = "Hello, Haskell!"
```

## GHCi

GHCi是GHC随附的交互式Haskell REPL（读取-评估-打印循环）。在ghci的提示，可以计算表达式，负载哈斯克尔使用文件:load（:l）（并与重新加载它们:reload（:r）），要求的表达与类型:type（:t），和许多其他的东西（尝试:?对命令的列表）。

```hs
ex01 = 3 + 2
ex02 = 19 - 27
ex03 = 2.35 * 8.6
ex04 = 8.7 / 3.1
ex05 = mod 19 3
ex06 = 19 `mod` 3
ex07 = 7 ^ 222
ex08 = (-3) * (-7)
```

注意“反引号”是如何将函数名称转换为中缀运算符。还请注意，负数必须经常用括号括起来，以避免将否定符号解析为减法。（是的，这很丑。对不起。）

因为/仅执行浮点除法。对于整数除法，可以使用div。

```hs
ex09 = i `div` i
ex10 = 12 `div` 5
```

如果习惯于使用其他语言进行数字类型的隐式转换，那么一开始这一切似乎都比较谨慎和烦人。并且随着时间的流逝，甚至可能会逐渐体会到它。隐式数字转换鼓励对数字代码草率的思考。

## Haskell 布尔逻辑

布尔值可以与(&&)（逻辑和），(||)（逻辑或）和组合not。例如，

```hs
ex11 = True && False
ex12 = not (False || True)
``

可以进行比较，以平等(==)和(/=)，或使用相比，顺序(<)，(>)，(<=)，和(>=)。

```hs
ex13 = ('a' == 'a')
ex14 = (16 /= 3)
ex15 = (5 > 3) && ('p' <= 'q')
ex16 = "Haskell" > "C++"
```

Haskell还具有if-expressions：if b then t else f是一个表达式，其计算结果t是布尔表达式的b计算结果是否为True，以及Boolean表达式的计算结果f是否b为False。请注意if- 表情比非常不同的if- 语句。例如，使用if语句，该else部分可以是可选的；省略的else子句表示“如果测试评估为False不执行任何操作”。if另一方面，对于-expression，该else部分是必需的，因为if-expression必须产生一定的值。

惯用的Haskell不太使用if表达式，通常使用**模式匹配**或后卫。

## 定义基本函数

可以根据情况在整数上编写函数。

```hs
-- Compute the sum of the integers from 1 to n.
sumtorial :: Integer -> Integer
sumtorial 0 = 0
sumtorial n = n + sumtorial (n-1)
```

请注意函数类型的语法：sumtorial :: Integer -> Integer表示该sumtorial函数以a Integer作为输入，并产生另一个Integer作为输出。

从上到下依次检查每个子句，然后选择第一个匹配子句。例如，由于第一个子句已匹配，因此sumtorial 0求值为0。sumtorial 3与第一个子句不匹配（3is not 0），因此尝试第二个子句。像n这样的变量可以匹配所有内容，因此第二个子句匹配并sumtorial 3求和3 + sumtorial (3-1)（然后可以进一步求值）。

也可以使用guards根据任意布尔表达式进行选择。例如：

```hs
hailstone :: Integer -> Integer
hailstone n
  | n `mod` 2 == 0 = n `div` 2
  | otherwise      = 3*n + 1
```

函数定义的每个子句都可以关联任意数量的保护，每个保护都是一个布尔表达式。如果子句的模式匹配，则按从上到下的顺序评估防护，并选择第一个评估为的防护True。如果所有防护均不等于True，则匹配继续进行下一个子句。

例如，假设评估hailstone 3。首先，3与匹配n，该匹配成功（因为变量匹配任何内容）。
接下来，n `mod` 2 == 0进行评估；这是False因为n = 3不会导致0除以时的余数2。
otherwise只是一个方便的同义词True，因此选择了第二个后卫，因此的结果hailstone 3是3*3 + 1 = 10。

作为更复杂（但更人为）的示例：

```
foo :: Integer -> Integer
foo 0 = 16
foo 1 
  | "Haskell" > "C++" = 3
  | otherwise         = 4
foo n
  | n < 0            = 0
  | n `mod` 17 == 2  = -43
  | otherwise        = n + 3
```


什么foo (-3)啊 foo 0？foo 1？foo 36？foo 38？

作为关于布尔表达式和保护的最后说明，假设想抽象化定义中使用的均匀性测试hailstone。第一次尝试如下所示：

```hs
isEven :: Integer -> Bool
isEven n 
  | n `mod` 2 == 0 = True
  | otherwise      = False
```

这有效，但是太复杂了。知道为什么吗？

## Hashell Pair

可以将事物配对在一起，如下所示：

```hs
p :: (Int, Char)
p = (3, 'x')
```

注意，该(x,y)符号用于对的类型和对的值。

可以使用模式匹配再次提取一对元素：

```hs
sumPair :: (Int,Int) -> Int
sumPair (x,y) = x + y
```

Haskell还具有三元组，四元组，…，但是绝对不要使用它们。将在下周看到，有更好的方法将三个或更多信息打包在一起。

使用函数和多个参数
要将函数应用于某些参数，只需在函数后列出参数，并用空格分隔即可，如下所示：

```
f :: Int -> Int -> Int -> Int
f x y z = x + y + z
ex17 = f 3 17 8
```

上述示例中的函数应用f到三个参数3，17和8。还要注意具有多个参数的函数类型的语法，例如Arg1Type -> Arg2Type -> ... -> ResultType。这对来说似乎很奇怪（应该！）。为什么所有的箭头？f像这样的类型会更有意义Int Int Int -> Int吗？实际上，语法并不是偶然的：这是出于非常深刻而美丽的原因的方式，将在几周后了解到它。现在，只需相信我的话！

请注意，**函数应用程序的优先级高于任何中缀运算符。所以写是不正确的**

```hs
f 3 n+1 7
```

如果打算将n+1作为第二个参数传递给f，因为它解析为

```hs
(f 3 n) + (1 7)。
```

相反，必须写

```hs
f 3 (n+1) 7。
```

## Hashell 列表

列表是Haskell中最基本的数据类型之一。

```hs
nums, range, range2 :: [Integer]
nums   = [1,2,3,19]
range  = [1..100]
range2 = [2,4..100]
```

Haskell（如Python）也具有列表理解能力；可以在LYAH中阅读有关它们的信息。

字符串只是字符列表。也就是说，String它只是的缩写`[Char]`，而字符串文字语法（文本用双引号引起来）只是一系列Char文字的缩写。

```hs
-- hello1 and hello2 are exactly the same.

hello1 :: [Char]
hello1 = ['h', 'e', 'l', 'l', 'o']

hello2 :: String
hello2 = "hello"

helloSame = hello1 == hello2
```

这意味着用于处理列表的所有标准库函数也可以用于处理String。

### 构造列表

最简单的列表是空列表：
```hs
emptyList = []
```
其他列表是使用cons运算符从空列表中构建的(:)。Cons接受一个元素和一个列表，并生成一个新列表，该元素位于前面。
```hs
ex18 = 1 : []
ex19 = 3 : (1 : [])
ex20 = 2 : 3 : 4 : []
ex21 = [2,3,4] == 2 : 3 : 4 : []
```
可以看到，`[2,3,4]`符号只是的方便速记`2 : 3 : 4 : []`。还要注意，这些实际上是单链接列表，而不是数组。
```hs
-- Generate the sequence of hailstone iterations from a starting number.
hailstoneSeq :: Integer -> [Integer]
hailstoneSeq 1 = [1]
hailstoneSeq n = n : hailstoneSeq (hailstone n)
```
当到达1时，停止冰雹序列。一般的冰雹序列由其自身n组成n，然后是的冰雹序列hailstone n，即通过对进行一次冰雹变换而获得的数字n。

列表中的功能
可以使用模式匹配在列表上编写函数。
```hs
-- Compute the length of a list of Integers.
intListLength :: [Integer] -> Integer
intListLength []     = 0
intListLength (x:xs) = 1 + intListLength xs
```
第一个子句说一个空列表的长度是0。第二个子句说如果输入列表看起来像(x:xs)，即第一个元素被x约束在剩余的列表上xs，那么该长度比的长度大一个xs。

由于根本不使用x，因此也可以用下划线代替：`intListLength (_:xs) = 1 + intListLength xs`。

还可以使用嵌套模式：
```hs
sumEveryTwo :: [Integer] -> [Integer]
sumEveryTwo []         = []     -- Do nothing to the empty list
sumEveryTwo (x:[])     = [x]    -- Do nothing to lists with a single element
sumEveryTwo (x:(y:zs)) = (x + y) : sumEveryTwo zs
```
请注意last子句如何匹配x以...开头y和后跟的列表…以...开头和后跟的列表zs。实际上不需要多余的括号，因此sumEveryTwo (x:y:zs) = ...是等效的。

## Haskell组合功能
通过组合许多简单功能来构建更复杂的功能是一种很好的Haskell风格。
```
-- The number of hailstone steps needed to reach 1 from a starting
-- number.
hailstoneLen :: Integer -> Integer
hailstoneLen n = intListLength (hailstoneSeq n) - 1
```
这对来说似乎效率低下：它先生成整个冰雹序列，然后找到其长度，这会浪费大量的内存……不是吗？实际上，事实并非如此！由于Haskell的惰性计算，仅根据需要生成序列的每个元素，因此交错了序列生成和列表长度计算。无论序列多长时间，整个计算仅使用O（1）内存。（实际上，这是一个很小的谎言，但要解释为什么（以及如何解决）将需要等待几周。）

将在几周内进一步了解Haskell的惰性评估策略。目前，要传达的信息是：不要害怕编写可转换整个数据结构的小函数，并将它们组合以产生更复杂的函数。刚开始时可能会感觉不自然，但这是编写惯用的（高效的）Haskell的方式，并且实际上是一种习惯后就很容易编写程序的方式。

关于错误消息的一句话
实际上，有六个：

不要害怕错误消息！

GHC的错误消息可能会很长，并且（似乎）令人恐惧。但是，通常它们长久以来并不是因为它们晦涩难懂，而是因为它们包含了大量有用的信息！这是一个例子：
```
Prelude> 'x' ++ "foo"

<interactive>:1:1:
    Couldn't match expected type `[a0]' with actual type `Char'
    In the first argument of `(++)', namely 'x'
    In the expression: 'x' ++ "foo"
    In an equation for `it': it = 'x' ++ "foo"
```
首先，被告知“无法将预期类型[a0]与实际类型匹配Char”。这意味着某些东西应该具有列表类型，而实际上却具有type Char。什么事 下一行告诉：它的第一个参数有(++)误，即'x'。接下来的几行继续为提供了更多背景信息。现在可以看到问题所在：正如第一行所说，显然'x'具有type Char。为什么会期望具有列表类型？好吧，因为它用作的参数(++)，该参数将列表作为第一个参数。

当收到大量错误消息时，请抵制最初的冲动以逃避；深吸一口气；并仔细阅读。不一定会理解整个事情，但是可能会学到很多东西，并且可能仅会获得足够的信息来找出问题所在。
