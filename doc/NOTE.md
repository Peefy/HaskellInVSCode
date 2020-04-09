
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
首先，被告知“无法将预期类型`[a0]`与实际类型匹配Char”。这意味着某些东西应该具有列表类型，而实际上却具有type Char。什么事 下一行告诉：它的第一个参数有(++)误，即'x'。接下来的几行继续为提供了更多背景信息。现在可以看到问题所在：正如第一行所说，显然'x'具有type Char。为什么会期望具有列表类型？好吧，因为它用作的参数(++)，该参数将列表作为第一个参数。

当收到大量错误消息时，请抵制最初的冲动以逃避；深吸一口气；并仔细阅读。不一定会理解整个事情，但是可能会学到很多东西，并且可能仅会获得足够的信息来找出问题所在。

## Haskell 枚举类型

Haskell允许程序员创建自己的枚举类型。这是一个简单的示例：

```hs
data Thing = Shoe 
           | Ship 
           | SealingWax 
           | Cabbage 
           | King
  deriving Show
```

此声明新的类型，称为Thing具有五个数据构造 Shoe，Ship等，这些类型的（仅）值Thing。（这deriving Show是一个神奇的咒语，它告诉GHC自动生成用于将Things 转换为Strings的默认代码。这是ghci在打印type表达式的值时使用的Thing。）

```hs
shoe :: Thing
shoe = Shoe

listO'Things :: [Thing]
listO'Things = [Shoe, SealingWax, King, Cabbage, King]
```

可以Thing通过模式匹配在s 上编写函数。

```hs
isSmall :: Thing -> Bool
isSmall Shoe       = True
isSmall Ship       = False
isSmall SealingWax = True
isSmall Cabbage    = True
isSmall King       = False
```

回顾函数子句如何按从上到下的顺序进行尝试，还可以使定义isSmall简短一些，如下所示：

```hs
isSmall2 :: Thing -> Bool
isSmall2 Ship = False
isSmall2 King = False
isSmall2 _    = True
```

## Haskell 扩展枚举

Thing是枚举类型，类似于其他语言（例如Java或C ++）提供的类型。但是，枚举实际上只是Haskell更通用的代数数据类型的特例。作为不只是枚举的数据类型的第一个示例，请考虑以下定义FailableDouble：

```hs
data FailableDouble = Failure
                    | OK Double
  deriving Show
```

这表示该FailableDouble类型具有两个数据构造函数。第一个Failure没有参数，因此Failure它本身就是type的值FailableDouble。第二个OK参数接受type的参数Double。因此OK本身不是类型的值FailableDouble; 需要给它一个Double。例如，OK 3.4是type的值FailableDouble。

```hs
ex01 = Failure
ex02 = OK 3.4
```

```hs
safeDiv :: Double -> Double -> FailableDouble
safeDiv _ 0 = Failure
safeDiv x y = OK (x / y)
```

模式匹配更多！请注意，在这种OK情况下，如何命名随Double其附带的。

```hs
failureToZero :: FailableDouble -> Double
failureToZero Failure = 0
failureToZero (OK d)  = d
```

数据构造函数可以有多个参数。

```hs
-- Store a person's name, age, and favourite Thing.
data Person = Person String Int Thing
  deriving Show

brent :: Person
brent = Person "Brent" 31 SealingWax

stan :: Person
stan  = Person "Stan" 94 Cabbage

getAge :: Person -> Int
getAge (Person _ a _) = a
```

类型构造函数和数据构造函数都是如何命名的Person，但是它们使用不同的名称空间，并且是不同的东西。这种习惯用法（给一个构造函数类型的类型和数据构造函数赋予相同的名称）是很常见的，但是在习惯之前会造成混淆。

### 一般的代数数据类型

代数数据类型具有一个或多个数据构造函数，每个数据构造函数可以具有零个或多个参数。

```hs
data AlgDataType = Constr1 Type11 Type12
                 | Constr2 Type21
                 | Constr3 Type31 Type32 Type33
                 | Constr4
```

这指定类型的值AlgDataType可以以四种方式之一来构造：使用Constr1，Constr2，Constr3，或Constr4。根据所使用的构造函数，一个AlgDataType值可能包含其他一些值。例如，如果使用构造它Constr1，则它带有两个值，一个是type Type11，另一个是type Type12。

**类型和数据构造函数名称必须始终以大写字母开头**；变量（包括函数名称）必须始终以小写字母开头。（否则，Haskell解析器将很难确定哪个名称表示变量，哪个名称表示构造函数）。

## Haskell 模式匹配

从根本上讲，模式匹配是通过找出构建它的构造函数来分解一个值。这些信息可以用作决定做什么的基础-实际上，在Haskell中，这是做出决定的唯一方法。

要决定如何处理type值AlgDataType（在上一节中定义的虚构类型），可以编写r类似

```hs
foo (Constr1 a b)   = ...
foo (Constr2 a)     = ...
foo (Constr3 a b c) = ...
foo Constr4         = ...
```

*注意，在不仅仅是一个构造函数的模式周围需要括号。*

* 下划线_可以用作匹配任何内容的“通配符模式”。
* 表单的模式`x@pat`可用于将值与模式进行匹配`pat`，但也x可为整个要匹配的值指定名称。例如：

```hs
baz :: Person -> String
baz p@(Person n _ _) = "The name field of (" ++ show p ++ ") is " ++ n
*Main> baz brent
"The name field of (Person \"Brent\" 31 SealingWax) is Brent"
```

* 模式可以嵌套。例如：

```hs
checkFav :: Person -> String
checkFav (Person n _ SealingWax) = n ++ ", you're my kind of person!"
checkFav (Person n _ _)          = n ++ ", your favorite thing is lame."
*Main> checkFav brent
"Brent, you're my kind of person!"
*Main> checkFav stan
"Stan, your favorite thing is lame."
```

请注意如何将模式嵌套在的模式SealingWax内Person。

以下语法定义了可以用作模式的内容：

```rs
pat ::= _
     |  var
     |  var @ ( pat )
     |  ( Constructor pat1 pat2 ... patn )
```

第一行说下划线是一种模式。第二行说一个变量本身就是一个模式：这种模式匹配任何东西，并将给定的变量名“绑定”到匹配的值。第三行指定@-patterns。最后一行说，构造函数名称后跟一系列模式本身就是一个模式：如果该模式是使用给定构造函数构造的，则该模式会与该值匹配，并且 pat1通过patn递归方式与该构造函数所包含的所有值进行匹配。

实际上，模式的完整语法仍然包含更多功能，但是其余的功能暂时将带到了很远的地方。

请注意，像2或一样的文字值'c'可以认为是没有参数的构造函数。就像类型Int和Char定义一样

```hs
data Int  = 0 | 1 | -1 | 2 | -2 | ...
data Char = 'a' | 'b' | 'c' | ...
```

这意味着可以对文字值进行模式匹配。（当然，Int并且实际上Char不是通过这种方式定义的。）

在Haskell中进行模式匹配的基本结构是case表达式。通常，case表达式看起来像

```hs
case exp of
  pat1 -> exp1
  pat2 -> exp2
  ...
```

当评估时，表达exp被针对每个图案的匹配pat1，pat2...反过来。选择第一个匹配模式，然后整个case表达式计算为与匹配模式相对应的表达式。例如，

```hs
ex03 = case "Hello" of
           []      -> 3
           ('H':s) -> length s
           _       -> 7
```

计算结果为4（选择了第二个模式；当然，第三个模式也匹配，但从未达到）。

实际上，看到的用于定义函数的语法实际上只是用于定义case表达式的方便语法。
例如，failureToZero先前给定的定义可以等效地写为

```
failureToZero' :: FailableDouble -> Double
failureToZero' x = case x of
                     Failure -> 0
                     OK d    -> d
```

## 递归数据类型

数据类型可以是递归的，即根据自身定义。实际上，已经看到了递归类型-列表的类型。列表为空，或者为单个元素，后跟剩余列表。可以这样定义自己的列表类型：

```
data IntList = Empty | Cons Int IntList
```

Haskell自己的内置列表非常相似。他们只是使用特殊的内置语法（[]和:）。
（当然，它们也适用于任何类型的元素，而不仅仅是Ints；）

经常使用递归函数来处理递归数据类型：

```hs
intListProd :: IntList -> Int
intListProd Empty      = 1
intListProd (Cons x l) = x * intListProd l
```

作为另一个简单的示例，可以定义一种二叉树的类型，
其Int值存储在每个内部节点上，并且Char存储在每个叶上：

```hs
data Tree = Leaf Char
          | Node Tree Int Tree
  deriving Show
```

```hs
tree :: Tree
tree = Node (Leaf 'x') 1 (Node (Leaf 'y') 2 (Leaf 'z'))
```

## Haskell 递归模式，多态性

尽管递归函数在理论上可以做很多事情，但实际上，某些通用模式会一遍又一遍地出现。通过将这些模式抽象到库函数中，程序员可以保留对这些函数进行递归的底层细节，而在更高层次上思考问题，这是全程编程的目标。

```hs
data IntList = Empty | Cons Int IntList
  deriving Show
```

可能会对IntList作的处理：

* 对列表的每个元素执行一些操作
* 根据测试，仅保留列表中的某些元素，并丢弃其他元素
* 以某种方式“汇总”列表中的元素（找到它们的总和，乘积，最大值…）。

例如可以向列表中的每个元素添加一个元素：

或者可以通过采用绝对值来确保列表中的每个元素都是非负的：

```hs
absAll :: IntList -> IntList
absAll Empty       = Empty
absAll (Cons x xs) = Cons (abs x) (absAll xs)
```

或者可以对每个元素求平方：

```hs
squareAll :: IntList -> IntList
squareAll Empty       = Empty
squareAll (Cons x xs) = Cons (x*x) (squareAll xs)
```

确实有一种方法-能解决吗？这三个示例中哪些部分相同，哪些部分发生变化？

当然，改变的是要对列表的每个元素执行的操作。可以将此操作指定为type 的函数Int -> Int。在这里，开始看到能够将功能作为输入传递给其他功能有多么巨大的用处！

现在，可以使用，和mapIntList实现：addOneToAllabsAllsquareAll

```rs
exampleList = Cons (-1) (Cons 2 (Cons (-6) Empty))

addOne x = x + 1
square x = x * x
mapIntList addOne exampleList
mapIntList abs    exampleList
mapIntList square exampleList
```

另一个常见的模式是，只想基于测试保留列表中的某些元素，而丢弃其他元素。例如，只保留正数或偶数：

```hs
keepOnlyEven :: IntList -> IntList
keepOnlyEven Empty = Empty
keepOnlyEven (Cons x xs)
  | even x    = Cons x (keepOnlyEven xs)
  | otherwise = keepOnlyEven xs
```

## Haskell 多态性

已经编写了一些不错的通用函数来映射和过滤Ints 列表。但是还没有完成概括！如果想过滤Integers的列表怎么办？或Bools？还是Strings 栈树列表的列表？对于每种情况，都必须创建一个新的数据类型和一个新的函数。更糟糕的是，代码将完全相同。唯一不同的是类型签名。Haskell不能在这里帮助吗？

当然可以！Haskell支持数据类型和函数的多态性。“多态”一词来自希腊语（πολύμορφος），意思是“具有多种形式”：多态的东西适用于多种类型。

### 多态数据类型

如何声明一个多态数据类型。

```hs
data List t = E | C t (List t)
```

之前data IntList = ...，有data List t = ...The t是一个类型变量，可以代表任何类型。（类型变量必须以小写字母开头，而类型必须以大写字母开头。）data List t = ...表示List类型是由类型参数化的，与函数可以由某些输入参数化的方式几乎相同。

给定类型t，a (List t)由构造器E或构造器C以及type值t和another组成(List t)。例子如下：

```rs
lst1 :: List Int
lst1 = C 3 (C 5 (C 2 E))

lst2 :: List Char
lst2 = C 'x' (C 'y' (C 'z' E))

lst3 :: List Bool
lst3 = C True (C False E)
```

### 多态函数

概括一下filterIntList的新多态Lists。可以只取码filterIntList并更换Empty由E并且Cons通过C：

```hs
filterList _ E = E
filterList p (C x xs)
  | p x       = C x (filterList p xs)
  | otherwise = filterList p xs
```

什么是类型filterList？看看ghci的类型推断：

```hs
*Main> :t filterList
filterList :: (t -> Bool) -> List t -> List t    
```

可以将其理解为：“对于任何类型t，filterList从tto中获取一个函数Bool，并包含一个t'的列表，并返回一个t'的列表。”

泛化mapIntList呢？应该赋予函数一个什么类型的函数以将函数mapList应用于a中的每个元素List t？

第一个想法可能是给它一个类型

```hs
mapList :: (t -> t) -> List t -> List t
```

这行得通，但是这意味着在应用时mapList，总是会得到一个列表，其元素类型与开始时的列表相同。这过于严格：希望能够执行类似的操作mapList show，例如将Ints 列表转换为s列表String。那么，这里是，实现的最通用类型mapList：
```hs
mapList :: (a -> b) -> List a -> List b
mapList _ E        = E
mapList f (C x xs) = C (f x) (mapList f xs)
```
关于多态函数要记住的一件事是，调用者可以选择类型。编写多态函数时，它必须适用于每种可能的输入类型。再加上Haskell无法直接根据某物是什么类型做出决策的事实，这具有一些有趣的含义，将在后面进行探讨。

该Prelude是一堆的标准定义是被隐式地导入每一个Haskell程序的模块。值得花一些时间浏览其文档以熟悉可用的工具。

当然，在中定义了多态列表Prelude，以及用于处理它们的许多有用的多态函数。例如，filter和map是filterList和的对应对象mapList。实际上，该Data.List模块仍然包含更多列表函数。

另一个有用的多态类型是Maybe，定义为
```hs
data Maybe a = Nothing | Just a
```
类型Maybe a的值要么包含类型的值a（包装在Just构造函数中），要么包含Nothing（表示某种故障或错误）。该Data.Maybe模块具有处理Maybe值的功能。

考虑以下多态类型：

```
[a] -> a
```

哪些功能可以具有这种类型？类型表示给定类型的事物列表a，函数必须产生一些类型的值a。例如，Prelude函数head具有这种类型。

…但是如果head输入一个空列表怎么办？让来看看源代码，为head...

它崩溃了！由于它必须适用于所有类型，因此它可能无能为力。没有办法凭空组成任意类型的元素。

head这就是所谓的局部函数：某些输入head会崩溃。具有某些输入将使它们无限递归的函数也称为局部函数。在所有可能的输入上定义明确的功能称为总功能。

Haskell的最佳实践是尽可能避免局部函数。实际上，在任何编程语言中，避免使用局部函数都是一种好习惯，但是在大多数情况下，这是令人讨厌的。Haskell倾向于使其变得非常容易和明智。

head是个错误！它不应该在中Prelude。其他部分Prelude，几乎从来不应该使用的功能包括tail，init，last，和(!!)。从这一点开始，在作业中使用以下功能之一将失去样式得分！

通常，局部函数（如head，tail等等）可以由模式匹配代替。请考虑以下两个定义：

```hs
doStuff1 :: [Int] -> Int
doStuff1 []  = 0
doStuff1 [_] = 0
doStuff1 xs  = head xs + (head (tail xs)) 
doStuff2 :: [Int] -> Int
doStuff2 []        = 0
doStuff2 [_]       = 0
doStuff2 (x1:x2:_) = x1 + x2
```

这些函数计算出的结果完全相同，并且它们都是合计的。但是显然只有第二个是全部，并且无论如何都更容易阅读。

如果发现自己编写了局部函数怎么办？有两种方法。首先是更改函数的输出类型以指示可能的故障。回顾以下的定义Maybe：

```hs
data Maybe a = Nothing | Just a
```

可以按照如下的方式安全地重写它：

```hs
safeHead :: [a] -> Maybe a
safeHead []    = Nothing
safeHead (x:_) = Just x
```

```hs
data NonEmptyList a = NEL a [a]

nelToList :: NonEmptyList a -> [a]
nelToList (NEL x xs) = x:xs

listToNel :: [a] -> Maybe (NonEmptyList a)
listToNel []     = Nothing
listToNel (x:xs) = Just $ NEL x xs

headNEL :: NonEmptyList a -> a
headNEL (NEL a _) = a

tailNEL :: NonEmptyList a -> [a]
tailNEL (NEL _ as) = as
```

## Hashell 高阶编程和类型推断

### 匿名函数

假设要编写一个函数
```hs
greaterThan100 :: [Integer] -> [Integer]
```
仅保留Integers输入列表中大于100的那些内容。例如，
```hs
greaterThan100 [1,9,349,6,907,98,105] = [349,907,105].
```
到目前为止，知道一种执行此操作的好方法：
```hs
gt100 :: Integer -> Bool
gt100 x = x > 100
```
```hs
greaterThan100 :: [Integer] -> [Integer]
greaterThan100 xs = filter gt100 xs
```
但是，gt100命名很烦人，因为可能永远不会再使用它了。相反，可以使用匿名函数，也称为lambda抽象：
```hs
greaterThan100_2 :: [Integer] -> [Integer]
greaterThan100_2 xs = filter (\x -> x > 100) xs
```
`\x -> x > 100`（反斜杠看起来像是缺少短腿的lambda）是一种函数，它接受单个参数x并输出是否x大于100。

Lambda抽象也可以有多个参数。例如：
```hs
Prelude> (\x y z -> [x,2*y,3*z]) 5 6 3
[5,12,9]
```
但是，在特定的情况下greaterThan100，有一种更好的方式编写它，而无需使用lambda抽象：
```
greaterThan100_3 :: [Integer] -> [Integer]
greaterThan100_3 xs = filter (>100) xs
```
`(>100)`是运算符部分：如果`?`是运算符，则`(?y)`等效于函数`\x -> x ? y`，并且`(y?)`等效于`\x -> y ? x`。换句话说，使用运算符部分可以使将运算符部分应用于其两个参数之一。得到的是单个参数的函数。这里有些例子：
```hs
Prelude> (>100) 102
True
Prelude> (100>) 102
False
Prelude> map (*6) [1..5]
[6,12,18,24,30]
```

### 函数组成

在继续阅读之前，可以写下一个类型为
```hs
(b -> c) -> (a -> b) -> (a -> c)
？
```
它必须接受两个参数（均为函数），并输出一个函数。
```hs
foo f g = ...
```
代替`...`为需要编写的type函数`a -> c`。好吧，可以使用`lambda抽象`创建一个函数：
```hs
foo f g = \x -> ...
```
x将具有类型a，现在`...`需要编写一个类型的表达式`c`。好的，有一个g可以将a a变成a b的函数，以及一个f可以将a b变成a 的函数c，所以这应该起作用：
```hs
foo :: (b -> c) -> (a -> b) -> (a -> c)
foo f g = \x -> f (g x)
```

好的，那是什么意思呢？是否foo真正做任何有用的或是只是一个无聊的练习与类型的工作？

事实证明，它foo是真正的`(.)`，代表函数的组成。也就是说，如果f和g是函数，则f . g先执行g然后再执行的功能f。

在编写简洁，优雅的代码时，函数组合可能非常有用。它非常适合“全餐”风格，在此考虑将数据结构的连续高级转换组合在一起。

例如，考虑以下函数：
```hs
myTest :: [Integer] -> Bool
myTest xs = even (length (greaterThan100 xs))
```
可以将其重写为：
```
myTest' :: [Integer] -> Bool
myTest' = even . length . greaterThan100
```
这个版本使发生的事情更加清晰：myTest'只是由三个较小函数组成的“管道”。此示例还说明了为什么函数组合看起来“向后”：这是因为函数应用程序向后！由于是从左到右阅读的，因此将值也视为从左到右流动是有意义的。但是在那种情况下，应该写\（（x）f \）来表示给定值\（x \）作为函数\（f \）的输入。

让仔细看看的类型`(.)`。如果使用ghci检查它的类型，可以得到
```hs
Prelude> :t (.)
(.) :: (b -> c) -> (a -> b) -> a -> c
```

还记得多参数函数的类型看起来很奇怪，就像它们中有“多余”箭头吗？例如考虑功能
```hs
f :: Int -> Int -> Int
f x y = 2 * x + y
```
之前曾承诺过，这有一个美丽而深刻的原因，现在终于可以揭露它了：Haskell中的所有函数都只接受一个参数。说什么？！但是f上面显示的函数不接受两个参数吗？不，实际上，它不是：它接受一个参数（an Int）并输出一个函数（类型Int -> Int）。该函数接受一个参数并返回最终答案。实际上，可以这样等效地编写f的类型：
```hs
f' :: Int -> (Int -> Int)
f' x y = 2*x + y
```
特别要注意的是，右侧的功能箭头`W -> X -> Y -> Z`等效于`W -> (X -> (Y -> Z))`。始终可以在类型中最右边的顶级箭头周围添加或删除括号。

而函数应用程序则保持左关联。也就是说，`f 3 2`确实是的简写`(f 3) 2`。考虑到之前所说的关于f实际接受一个参数并返回一个函数f的说法3，这是有道理的：适用于一个参数，该参数返回一个类型为type的函数`Int -> Int`，即一个将Int加上6 的函数。然后，2通过编写将该函数应用于自变量(f 3) 2，从而得到一个Int。由于函数应用程序关联到左侧，因此可以缩写(f 3) 2为f 3 2，从而f为“多参数”函数提供了一个很好的表示法。

### “多参数” lambda抽象

`\x y z -> ...` 只是语法糖，其实可写为`\x -> (\y -> (\z -> ...))`.  

同样，函数定义`f x y z = ...` 也是语法糖，其实是`f = \x -> (\y -> (\z -> ...)).`

请注意，可以通过`\x -> ...`从的右侧将=移到左侧来从上方重写合成函数：
```hs
comp :: (b -> c) -> (a -> b) -> a -> c
comp f g x = f (g x)
```
将多参数函数表示为单参数函数返回函数的想法被称为currying，以英国数学家和逻辑学家Haskell Curry的名字命名。

如果要实际表示两个参数的函数，则可以使用一个**元组**的单个参数。即功能
```hs
f'' :: (Int,Int) -> Int
f'' (x,y) = 2*x + y
```
也可以考虑采用“两个论点”，尽管从另一种意义上说，它实际上只采用了一个恰好是一对的论点。为了在两个参数的函数的两种表示形式之间进行转换，标准库定义了称为curry和的函数uncurry，其定义如下（除非使用不同的名称）：
```
schönfinkel :: ((a,b) -> c) -> a -> b -> c
schönfinkel f x y = f (x,y)

unschönfinkel :: (a -> b -> c) -> (a,b) -> c
unschönfinkel f (x,y) = f x y
```
uncurry特别是当有一对想要对它应用功能时，该功能很有用。例如：
```
Prelude> uncurry (+) (2,3)
5
```

Haskell中的函数被咖喱化的事实使得部分应用特别容易。部分应用的想法是，可以采用多个参数的功能，并将其仅应用于其某些参数，然后得出其余参数的功能。但是，正如刚刚看到的，在Haskell 中没有多重参数的功能！每个函数都可以“部分地”应用到其第一个（也是唯一一个）参数，从而产生其余参数的功能。

请注意，Haskell并不容易将部分参数应用于第一个参数之外的其他参数。一个例外是中缀运算符，正如已经看到的那样，可以使用运算符部分将其部分应用于两个自变量。实际上，这并不是很大的限制。确定某项函数的参数顺序以使其部分应用尽可能有用是一种技巧：参数应从“最小变化到最大变化”进行排序，也就是说，通常应该相同的参数应为首先列出，然后通常会有所不同的论点应该放在最后。

让将一个示例中刚刚学到的东西放在一起，该示例还显示了“全餐”编程风格的强大功能。考虑foobar定义如下的函数：
```hs
foobar :: [Integer] -> Integer
foobar []     = 0
foobar (x:xs)
  | x > 3     = (7*x + 2) + foobar xs
  | otherwise = foobar xs
```
这似乎很简单，但是不是很好的Haskell样式。问题是

与其考虑要对每个元素做什么，不如考虑使用已知的现有递归模式对整个输入进行增量转换。这是一个更加惯用的实现foobar：
```hs
foobar' :: [Integer] -> Integer
foobar' = sum . map (\x -> 7*x + 2) . filter (>3)
```
这定义foobar'为三个函数的“管道”：首先，将列表中不大于三个的所有元素丢弃。接下来，对其余列表的每个元素进行算术运算；最后，对结果求和。

请注意，在上面的示例中，map和filter已部分应用。例如，类型filter为
```hs
(a -> Bool) -> [a] -> [a]
```
将它应用于`(>3)`（具有类型的`Integer -> Bool`）会产生一个类型的函数`[Integer] -> [Integer]`，这与将另一个函数组合在一起恰到好处`[Integer]`。

编码的这种风格中，定义一个函数不参照它的参数，在一定意义上说的功能什么的，而不是什么它做 -is被称为“自由点”的风格。从上面的示例可以看出，它可能非常漂亮。甚至有人甚至说应该始终使用无点样式。但是太远了，它会变得非常混乱。lambdabot在#haskellIRC信道有一个命令@pl用于使功能集成到相当的自由点表达式; 这是一个例子：
```hs
@pl \f g x y -> f (x ++ g x) (g y)
join . ((flip . ((.) .)) .) . (. ap (++)) . (.)
```

列表上还有一个递归模式可以讨论：**折叠**。
以下是一些遵循类似模式的列表函数：它们全部以某种方式“组合”列表中的元素成为最终答案。
```hs
sum' :: [Integer] -> Integer
sum' []     = 0
sum' (x:xs) = x + sum' xs

product' :: [Integer] -> Integer
product' [] = 1
product' (x:xs) = x * product' xs

length' :: [a] -> Int
length' []     = 0
length' (_:xs) = 1 + length' xs
```
这三个功能有什么共同点，有什么不同？与往常一样，该想法将是借助定义高阶函数的能力来抽象出变化的部分。
```hs
fold :: b -> (a -> b -> b) -> [a] -> b
fold z f []     = z
fold z f (x:xs) = f x (fold z f xs)
```
请注意如何fold基本上取代了[]用z并(:)用f，也就是说，

fold f z [a,b,c] == a `f` (b `f` (c `f` z))
（如果fold从这个角度考虑，也许可以弄清楚如何归纳fold为列表以外的数据类型……）

现在，改写sum'，product'和length'在以下方面fold：
```
sum''     = fold 0 (+)
product'' = fold 1 (*)
length''  = fold 0 (\_ s -> 1 + s)
```
代替(`\_ s -> 1 + s`)也可以写(`\_ -> (1+)`)，甚至(`const (1+))`。

当然，fold已经在标准Prelude中以名称提供了foldr。参数的foldr顺序略有不同，但功能完全相同。以下是一些Prelude函数，它们的定义如下foldr：
```hs
length :: [a] -> Int
sum :: Num a => [a] -> a
product :: Num a => [a] -> a
and :: [Bool] -> Bool
or :: [Bool] -> Bool
any :: (a -> Bool) -> [a] -> Bool
all :: (a -> Bool) -> [a] -> Bool
```
还存在foldl“从左侧”折叠的。那是，
```hs
foldr f z [a,b,c] == a `f` (b `f` (c `f` z))
foldl f z [a,b,c] == ((z `f` a) `f` b) `f` c
```
但是，一般而言，应该改用foldl'fromData.List，它的作用与之相同，foldl但效率更高。

## Hashell 更多种类的多态和类型类

Haskell特殊的多态被称为参数多态。本质上，这意味着多态函数必须对任何输入类型均一地工作。事实证明，这对于程序员和多态函数用户都具有一些有趣的含义。

### 参数化

考虑类型
```hs
a -> a -> a
```
请记住，a是一个类型变量，可以代表任何类型。这种类型的功能有哪些？

那这个呢：
```hs
f :: a -> a -> a
f x y = x && y
```
事实证明这是行不通的。该语法至少有效，但不进行检查。特别是，收到以下错误消息：
```
2012-02-09.lhs:37:16:
    Couldn't match type `a' with `Bool'
      `a' is a rigid type variable bound by
          the type signature for f :: a -> a -> a at 2012-02-09.lhs:37:3
    In the second argument of `(&&)', namely `y'
    In the expression: x && y
    In an equation for `f': f x y = x && y
```
这不起作用的原因是多态函数的调用者可以选择类型。在这里，（实现者）试图选择一种特定的类型（即Bool），但可能会给String，或Int，甚至是某人使用定义的某种类型f，而可能无法事先知道。换句话说，可以阅读类型
```hs
a -> a -> a
```
作为承诺，与这种类型的功能将工作不管是什么类型的调用者进行选择。

可以想象的另一个实现是
```
f a1 a2 = case (typeOf a1) of
            Int  -> a1 + a2
            Bool -> a1 && a2
            _    -> a1
```
其中f某些类型的行为以某些特定方式表现。毕竟，当然可以在Java中这样实现它：
```java
class AdHoc {

    public static Object f(Object a1, Object a2) {
        if (a1 instanceof Integer && a2 instanceof Integer) {
            return (Integer)a1 + (Integer)a2;
        } else if (a1 instanceof Boolean && a2 instanceof Boolean) {
            return (Boolean)a1 && (Boolean)a2;
        } else {
            return a1;
        }
    }

    public static void main (String[] args) {
        System.out.println(f(1,3));
        System.out.println(f(true, false));
        System.out.println(f("hello", "there"));
    }

}
```

但事实证明，无法用Haskell编写此代码。Haskell没有Java instanceof运算符之类的东西：不可能问什么是什么类型，并不能根据答案决定要做什么。原因之一是检查后，编译器将擦除 Haskell类型：在运行时，没有类型信息可供查询！但是，正如将看到的，还有其他充分的理由。

这种类型的多态被称为**参数多态**。说像这样的函数在类型中`f :: a -> a -> a`是参数化的a。在这里，“参数”只是“对于呼叫者选择的任何类型都可以统一工作”的奇特名词。在Java中，这种类型的多态性是由泛型提供的（猜对了，它受Haskell的启发：Haskell的原始设计师之一Philip Wadler后来成为Java泛型开发的主要参与者之一）。

那么，实际上什么功能可以具有这种类型？其实只有两个！
```hs
f1 :: a -> a -> a
f1 x y = x

f2 :: a -> a -> a
f2 x y = y
```
因此，事实证明类型`a -> a -> a`确实告诉了很多东西。

考虑以下每种多态类型。对于每种类型，确定该类型的功能可能具有的行为。
```hs
a -> a
a -> b
a -> b -> a
[a] -> [a]
(b -> c) -> (a -> b) -> (a -> c)
(a -> a) -> a -> a
```
关于参数化的两种观点:

* 作为多态函数的实现者，尤其是如果习惯于使用Java之类的结构的语言时instanceof，可能会发现这些限制很烦人。
* 作为多态函数的用户，参数性不对应于限制，而是对应于保证。通常，当这些工具为提供有关它们的行为方式的有力保证时，它们的使用和推理就容易得多。参数化是仅查看Haskell函数类型可以告诉有关函数的太多原因的一部分。

好的，很好，但是有时候根据类型决定要做什么真的很有用！例如，加法呢？已经看到加法是多态的（例如，可在Int，Integer和上Double使用），但显然它必须知道要添加的数字类型才能决定要做什么：两个Integers加法的方式与Double类型的加法完全不同。那么它实际上是如何工作的呢？只是魔术吗？

其实不是！实际上，可以使用Haskell根据类型决定要做什么，只是不像以前想象的那样。让先来看一下的类型(+)：
```hs
Prelude> :t (+)
(+) :: Num a => a -> a -> a
```
嗯，`Num a =>`那边在做什么？实际上，`(+)`并不是唯一一个带有有趣的双箭头类型的标准函数。以下是一些其他内容：
```hs
(==) :: Eq a   => a -> a -> Bool
(<)  :: Ord a  => a -> a -> Bool
show :: Show a => a -> String
```
那么这是怎么回事？

### 类型类别

Num，Eq，Ord，和Show是类型类，和说(==)，(<)和(+)有“型级多态”。直观地讲，类型类对应于为它们定义了某些操作的类型集，并且类型类多态函数仅适用于作为所讨论类型类实例的类型。作为示例，让详细研究Eq类型类。
```hs
class Eq a where
  (==) :: a -> a -> Bool
  (/=) :: a -> a -> Bool
```
可以这样阅读：Eq声明为带有单个参数的类型类a。任何a要成为的实例的类型都Eq必须定义两个函数，(==)并(/=)使用指定的类型签名。例如，要成为Int的实例，Eq必须定义(==) :: Int -> Int -> Bool和(/=) :: Int -> Int -> Bool。（当然，没有必要，因为标准的Prelude已经为定义了一个Int实例Eq。）

再次看看`(==)`类型：
```hs
(==) :: Eq a => a -> a -> Bool
```
在`Eq a`之前的`=>`是一个类型类的约束。可以这样解读：对于任何类型a，只要a是`Eq type`的实例，`(==)`都可以采用type的两个值a并返回`a Bool`。`(==)`在不是的实例的某种类型上调用函数是类型错误Eq。如果一个普通的多态类型是一个保证函数将适用于调用者选择的任何类型的承诺，则类型类多态函数是一个有限的保证，即该函数将适用于调用者选择的任何类型的只要该实例是一个实例。所需类型类别的。

需要注意的重要一点是，当使用`(==)`（或任何类型类方法）时，编译器将根据其参数的推断类型使用类型推断来确定应选择哪种实现(==)。换句话说，这类似于在Java之类的语言中使用重载方法。

为了更好地了解它在实际中的工作方式，让创建自己的类型并Eq为其声明一个实例。
```hs
data Foo = F Int | G Char

instance Eq Foo where
  (F i1) == (F i2) = i1 == i2
  (G c1) == (G c2) = c1 == c2
  _ == _ = False

  foo1 /= foo2 = not (foo1 == foo2)
```
必须同时定义`(==)`和`(/=)`。实际上，类型类可以根据其他方法提供方法的默认实现，只要实例不使用其自身覆盖默认定义，就应使用该方法。因此可以想象这样声明Eq：
```hs
class Eq a where
  (==) :: a -> a -> Bool
  (/=) :: a -> a -> Bool
  x /= y = not (x == y)
```
现在，任何声明`Eq`实例的地方都必须指定实现`(==)`。但是，如果由于某种原因想用自己的`(/=)`方法覆盖默认实现，那么也可以。

实际上，Eq该类实际上是这样声明的：
```hs
class Eq a where
  (==), (/=) :: a -> a -> Bool
  x == y = not (x /= y)
  x /= y = not (x == y)
```
这意味着，当做的一个实例Eq，可以定义两种 (==)或(/=)，取其更方便; 另一项将根据指定的一项自动定义。（但是，必须要小心：如果不指定任何一个，将得到无限递归！）

事实证明，Eq（以及其他一些标准类型类）很特殊：GHC能够自动Eq为生成的实例。像这样：
```hs
data Foo' = F' Int | G' Char
  deriving (Eq, Ord, Show)
```
这告诉GHC的自动派生实例Eq，Ord以及Show类型类为的数据类型Foo。

### 类型类和Java接口

类型类与Java接口非常相似。两者都定义了一组实现特定操作列表的类型/类。但是，有几种重要的方式可以使类型类比Java接口更通用：

* 定义Java类时，必须声明其实现的任何接口。另一方面，类型类实例是与相应类型的声明分开声明的，甚至可以放在单独的模块中。
* 与为Java接口方法提供的签名相比，可以为类型类方法指定的类型更通用，更灵活，尤其是在多参数类型类输入图片时。例如，假设一个假设类型类
```hs
class Blerg a b where
  blerg :: a -> b -> Bool
```
使用blerg达做多分派：其中实现blerg编译器应该选择取决于两种类型a和b。用Java没有简单的方法可以做到这一点。

Haskell类型类也可以轻松地处理二进制（或三进制或…）方法，如
```hs
class Num a where
  (+) :: a -> a -> a
  ...
```
在Java中，没有很好的方法来执行此操作：一方面，两个参数之一必须是“特权”参数，实际上是要`(+)`在其上调用方法，并且这种不对称性很尴尬。此外，由于Java的子类型化，获取某个接口类型的两个参数并不能保证它们实际上是同一类型，这使得实现二进制运算符（通常需要进行一些运行时类型检查）成为可能。

### 标准类型类别

这是应该了解的其他一些标准类型类：

* Ord用于其元素可以完全排序的类型，即可以比较任何两个元素以查看哪个元素小于另一个元素。它提供了类似的比较操作(<)和(<=)，也是compare功能。
* Num用于“数字”类型，它支持加，减和乘积运算。要注意的一件事很重要，就是整数文字实际上是类型多态的类型：
```hs
Prelude> :t 5
5 :: Num a => a
```
这意味着像这样的文字5可以用作Ints，Integers，Doubles或任何其他类型的类型，这些类型是Num（Rational，Complex Double甚至定义的类型...）的实例。

Show定义了方法show，该方法用于将值转换为Strings。

阅读是的双重性Show。

整数表示整数类型，例如Int和Integer。

### 类型类示例

作为创建自己的类型类的示例，请考虑以下内容：
```hs
class Listable a where
  toList :: a -> [Int]
```
可以将其Listable视为可以转换为Ints 列表的事物类。看一下类型toList：
```
toList :: Listable a => a -> [Int]
```
让为创建一些实例Listable。首先，Int可以转换为`[Int]`只通过创建一个单列表，并且Bool同样可以转换，也就是说，通过翻译True来1和False到0：
```hs
instance Listable Int where
  -- toList :: Int -> [Int]
  toList x = [x]

instance Listable Bool where
  toList True  = [1]
  toList False = [0]
```
无需做任何工作即可将的列表转换Int为的列表Int：
```hs
instance Listable [Int] where
  toList = id
```
最后，这是一个二叉树类型，可以通过展平将其转换为列表：
```hs
data Tree a = Empty | Node a (Tree a) (Tree a)

instance Listable (Tree Int) where
  toList Empty        = []
  toList (Node x l r) = toList l ++ [x] ++ toList r
```
如果根据实现其他功能toList，它们也会受到Listable约束。例如：
```hs
-- to compute sumL, first convert to a list of Ints, then sum
sumL x = sum (toList x)
```
ghci通知类型sumL为
```hs
sumL :: Listable a => a -> Int
```
这很有意义：由于使用，因此sumL仅适用于作为实例的类型。这个如何？ListabletoList
```hs
foo x y = sum (toList x) == sum (toList y) || x < y
```
ghci告知的类型foo是
```hs
foo :: (Listable a, Ord a) => a -> a -> Bool
```
也就是说，foo对同时作为 Listable和的实例的类型进行处理Ord，因为它toList在参数上同时使用和比较。

作为最后一个更复杂的示例，请考虑以下实例：
```
instance (Listable a, Listable b) => Listable (a,b) where
  toList (x,y) = toList x ++ toList y
```
注意如何将类型类约束放在实例以及函数类型上。这表示对类型(a,b)是和都Listable一样长的实例。然后，可以在类型的值上以及在对的定义中使用。请注意，此定义不是递归的！的版本，正在定义是调用其他的版本，而不是自己。


