---
title: 值、类型和运算符
description: values
---

> 在机器表面之下，程序在运转。它毫不费力地扩张和收缩。电子在和谐中分散和重组。显示器上的形式不过是水面上的涟漪。本质隐藏在下面，不可见。
>
> —— 元马大师，编程之书

![chapter_picture_01.jpg](./chapter_picture_1.jpg)

在计算机的世界里，只有数据。你可以读取数据、修改数据、创建新数据 —— 但不能提及不是数据的东西。所有这些数据都以长序列的位存储，因此从根本上来说都是相似的。

比特（Bits） 是任何一种二值事物，通常用 0 和 1 来描述。在计算机内部，它们的形式包括高或低电荷、强或弱信号，或 CD 表面上的亮点或暗点。任何离散信息都可以简化为 0 和 1 的序列，从而用比特来表示。

例如，我们可以用位来表示数字 13。其工作原理与十进制数相同，但不是 10 个不同的数字，而是只有 2 个，并且每个数字的权重从右到左增加 2 倍。以下是组成数字 13 的位，其下方显示了数字的权重：

```
   0 0 0 0 1 1 0 1
 128 64 32 16 8 4 2 1
```

这就是二进制数 00001101。它的非零数字代表 8、4 和 1，加起来为 13。

## 值

想象一下比特的海洋——无边无际。一台典型的现代计算机的易失性数据存储器（工作内存）中存储着超过 1000 亿比特。非易失性存储器（硬盘或类似设备）的存储量往往还要大几个数量级。

为了能够处理如此大量的位而不至于迷失方向，我们将它们分成代表信息片段的块。在 JavaScript 环境中，这些块称为值。虽然所有值都是由位组成的，但它们扮演着不同的角色。每个值都有一种决定其角色的类型。有些值是数字，有些值是文本片段，有些值是函数，等等。

要创建一个值，你只需调用它的名称即可。这很方便。你不必为值收集构建材料或为它们付费。你只需调用一个，然后嗖，你就拥有了它。当然，值并不是凭空而来的。每个值都必须存储在某个地方，如果你想同时使用大量的值，你可能会耗尽计算机内存。幸运的是，这只有在你同时需要它们时才会成为问题。一旦你不再使用某个值，它就会消散，留下它的位元作为下一代值的构建材料被回收利用。

本章的其余部分介绍 JavaScript 程序的原子元素，即简单值类型和可以对这些值进行操作的运算符。

## 数字

数字类型的值，毫无疑问是数值。在 JavaScript 程序中，它们的写法如下：

```js
13;
```

在程序中使用该指令将导致数字 13 的位模式在计算机内存中出现。

JavaScript 使用固定数量的位（64 位）来存储单个数值。使用 64 位可以创建的模式数量有限，这限制了可以表示的不同数字的数量。使用 _N_ 十进制数字，您可以表示 10<sup>n</sup> 个数字。同样，给定 64 个二进制数字，您可以表示 2<sup>64</sup> 不同的数字，大约是 18 千万亿（18 后面有 18 个零）。这可不少。

计算机内存曾经很小，人们倾向于使用 8 位或 16 位来表示数字。如此小的数字很容易意外溢出— 最终得到一个无法容纳给定位数的数字。如今，即使是口袋大小的计算机也拥有充足的内存，因此您可以自由使用 64 位块，只有在处理真正天文数字时才需要担心溢出。

不过，并非所有小于 18 千万亿的整数都适合用 JavaScript 数字表示。这些位还存储负数，因此一位表示数字的符号。更大的问题是如何表示非整数。为此，一些位用于存储小数点的位置。可以存储的实际最大整数在 9 千万亿（15 个零）范围内——这仍然非常大。

小数用点来书写：

```js
9.81;
```

对于非常大或非常小的数字，您也可以使用科学计数法，即添加 e（表示指数），后跟数字的指数。

```js
2.998e8;
```

即 2.998 × 10<sup>8</sup> = 299,800,000。

对于小于上述 9 千万亿的整数（也称为整数）的计算，保证始终精确。不幸的是，对于分数的计算通常并非如此。正如 π (pi) 不能用有限数量的十进制数字精确表示一样，当只有 64 位可用来存储它们时，许多数字会失去一些精度。这很遗憾，但它只会在特定情况下造成实际问题。重要的是要意识到这一点，并将分数数字视为近似值，而不是精确值。

### 算术

与数字有关的主要事情是算术。诸如加法或乘法之类的算术运算采用两个数值并从中产生一个新数字。它们在 JavaScript 中的样子如下：

```js
100 + 4 * 11;
```

\+ 和符号 \* 称为运算符。第一个表示加法，第二个表示乘法。将运算符放在两个值之间会将其应用于这些值并产生一个新值。

这个例子的意思是“将 4 和 100 相加，然后将结果乘以 11”，还是先进行乘法再进行加法？您可能已经猜到了，乘法先进行。与数学一样，您可以通过将加法括在括号中来更改这一点。

```js
（100 + 4）* 11
```

对于减法，有 \- 运算符。除法可以用运算符完成 /。

当运算符一起出现且不带括号时，它们的应用顺序由运算符的优先级决定。示例显示乘法在加法之前。/ 运算符的优先级与相同 \*。同样，\+ 和 \- 具有相同的优先级。当多个具有相同优先级的运算符彼此相邻出现时，例如 1 - 2 + 1，它们将从左到右应用：(1 - 2) + 1。

不必太担心这些优先规则。如有疑问，只需添加括号即可。

还有一个算术运算符，您可能不会立即认出。符号 % 用于表示余数运算。是除以 X % Y 的余数。例如，314 % 100 等于 14 以及 144 % 12 等于 0。余数运算符的优先级与乘法和除法相同。您还会经常看到此运算符称为模运算。

### 特殊数字

JavaScript 中有三个特殊值，它们被视为数字，但行为却与普通数字不同。前两个是 Infinity 和 \- Infinity，分别代表正无穷和负无穷。Infinity - 1 仍然是 Infinity，等等。不过，不要太相信基于无穷的计算。它在数学上是不合理的，很快就会得出下一个特殊数字：NaN。

NaN 代表“不是数字”，即使它是数字类型的值。例如，当您尝试计算 0 / 0（零除以零）Infinity - Infinity 或任何其他不会产生有意义结果的数字运算时，您将得到此结果。

## 字符串

下一个基本数据类型是字符串。字符串用于表示文本。它们的内容用引号括起来。

```js
`Down on the sea`;
("Lie on the ocean");
("Float on the ocean");
```

您可以使用单引号、双引号或反引号来标记字符串，只要字符串开头和结尾的引号匹配即可。

您可以将几乎任何内容放在引号之间，以便 JavaScript 将其转换为字符串值。但有些字符比较难处理。您可以想象在引号之间放置引号有多难，因为它们看起来像字符串的结尾。只有当字符串用反引号 ( ) 括起来时，才能包含换行符（按 Enter 时得到的字符） `。

为了能够在字符串中包含此类字符，使用以下符号：\引号内的反斜杠 ( ) 表示其后的字符具有特殊含义。这称为转义字符。以反斜杠开头的引号不会结束字符串，而是字符串的一部分。当字符 n 出现在反斜杠后时，它将被解释为换行符。同样，t 反斜杠后的 表示制表符。以以下字符串为例：

```js
"This is the first line\nAnd this is the second";
```

这是该字符串中的实际文本：

```js
This is the first line
And this is the second
```

当然，有些情况下，您希望字符串中的反斜杠只是一个反斜杠，而不是特殊代码。如果两个反斜杠接在一起，它们将合并在一起，并且结果字符串值中只剩下一个。字符串“换行符写成"\n "。 ”可以这样表达：

```js
"A newline character is written like \"\\n\".";
```

同样，字符串也必须被建模为一系列位才能存在于计算机中。JavaScript 实现这一点的方式基于 Unicode 标准。该标准为几乎所有您需要的字符分配一个数字，包括希腊语、阿拉伯语、日语、亚美尼亚语等字符。如果我们为每个字符分配一个数字，那么字符串就可以用一系列数字来描述。这就是 JavaScript 所做的。

<!-- TODO -->

不过，有一个问题很复杂：JavaScript 的表示方法为每个字符串元素使用 16 位，最多可以描述 2<sup>16</sup> 个不同的字符。但是，Unicode 定义的字符比这要多——目前大约是这个数字的两倍。因此，某些字符（例如许多表情符号）在 JavaScript 字符串中占用两个“字符位置”。我们将在第 5 章中回顾这一点。

字符串不能除法、乘法或减法。+运算符可以用于它们，不是加法，而是连接——将两个字符串粘合在一起。以下行将生成字符串"concatenate"：

```js
"con" + "cat" + "e" + "nate";
```

<!-- TODO -->

字符串值有许多相关函数（方法），可用于对其执行其他操作。我将在第 4 章中详细介绍这些内容。

用单引号或双引号编写的字符串的行为非常相似 —— 唯一的区别在于您需要在其中转义哪种类型的引号。反引号字符串（通常称为模板文字）可以执行更多技巧。除了能够跨行之外，它们还可以嵌入其他值。

```js
`half of 100 is ${100 / 2}`;
```

当你在模板字面量中写入某些内容时${}，其结果将被计算、转换为字符串并包含在该位置。此示例生成字符串"half of 100 is 50"。

## 一元运算符

并非所有运算符都是符号。有些写成单词。一个例子是 typeof 运算符，它生成一个字符串值，该字符串值命名了您赋予它的值的类型。

```js
console.log(typeof 4.5);
// → number
console.log(typeof "x");
// → string
```

我们将在示例代码中使用 console.log 来表示我们想要看到评估某事物的结果。（下一章将详细介绍。）

本章到目前为止介绍的其他运算符都对两个值进行运算，但 typeof 只接受一个值。使用两个值的运算符称为二元运算符，而接受一个值的运算符称为一元运算符。减号运算符 (\-) 既可以用作二元运算符，也可以用作一元运算符。

```js
console.log(-(10 - 2));
// → -8
```

## 布尔值

通常，拥有一个仅区分两种可能性的值很有用，例如“是”和“否”或“开”和“关”。为此，JavaScript 有一个布尔类型，它只有两个值，即 true 和 false，写成这些词。

### 比较

以下是产生布尔值的一种方法：

```js
console.log(3 > 2);
// → true
console.log(3 < 2);
// → false
```

\> 和符号 < 分别是“大于”和“小于”的传统符号。它们是二元运算符。应用它们会产生一个布尔值，表示它们在这种情况下是否成立。

可以用同样的方式比较字符串。

```js
console.log("Aardvark" < "Zoroaster");
// → true
```

字符串的排序方式大致是按字母顺序排列的，但实际上并不是您期望在字典中看到的顺序：大写字母总是比小写字母“小”，因此"Z" < "a"，和非字母字符（！、- 等）也包含在排序中。比较字符串时，JavaScript 会从左到右逐个比较字符的 Unicode 代码。

其他类似的运算符有>=（大于或等于）、<=（小于或等于）、==（等于）和!=（不等于）。

```js
console.log("Garnet" != "Ruby");
// → true
console.log("Pearl" == "Amethyst");
// → false
```

JavaScript 中只有一个值不等于其自身，那就是 NaN（“不是数字”）。

```js
console.log(NaN == NaN);
// → false
```

NaN 应该表示无意义计算的结果，因此，它不等于任何其他无意义计算的结果。

### 逻辑运算符

还有一些运算可以应用于布尔值本身。JavaScript 支持三个逻辑运算符：and、or 和 not。这些可用于“推理”布尔值。

运算符 && 表示逻辑与。它是一个二元运算符，只有当赋予它的两个值都为真时，其结果才为真。

```js
console.log(true && false);
// → false
console.log(true && true);
// → true
```

|| 运算符表示逻辑或。如果给定的任一值是真，则结果为真。

```js
console.log(false || true)
// → true
控制台.log（false || false）
// → false
```

取反写成成感叹号 ( !)。它是一个一元运算符，对给定的值进行翻转 —— !true 产生 false 同时 !false 返回 true。

当将这些布尔运算符与算术运算符和其他运算符混合使用时，何时需要使用括号并不总是很明显。实际上，您通常可以知道到目前为止我们看到的运算符中，||优先级最低，然后是&&，然后是比较运算符（>，== 等等），然后是其余的。选择此顺序是为了在类似以下的典型表达式中，需要尽可能少的括号：

```js
1 + 1 == 2 && 10 * 10 > 50;
```

我们将要讨论的最后一个逻辑运算符不是一元的，也不是二元的，而是三元的，对三个值进行运算。它用问号和冒号写成，如下所示：

```js
console.log(true ? 1 : 2);
// → 1
console.log(false ? 1 : 2);
// → 2
```

这个运算符被称为条件运算符（有时也被称为三元运算符，因为它是该语言中唯一的三元运算符）。该运算符使用问号左侧的值来决定“选择”其他两个值中的哪一个。如果你写 a ? b : c，当 a 为真的时结果将是 b ，否则为 c。

## 空值

有两个特殊值，写作 null 和 undefined，用于表示没有有意义的值。它们本身也是值，但不携带任何信息。

语言中许多不会产生有意义值的操作 undefined 仅仅是因为它们必须产生一些值。

undefined 和之间的含义差异 null 是 JavaScript 设计的偶然现象，大多数情况下并不重要。如果您确实需要关注这些值，我建议将它们视为几乎可以互换。

## 自动类型转换

在[介绍](../../00_intro/readme/)中，我提到 JavaScript 会尽其所能地接受你给它的任何程序，即使是执行奇怪操作的程序。以下表达式很好地证明了这一点：

```js
console.log(8 * null);
// → 0
console.log("5" - 1);
// → 4
console.log("5" + 1);
// → 51
console.log("five" * 2);
// → NaN
console.log(false == 0);
// → true
```

当运算符应用于“错误”类型的值时，JavaScript 会悄悄地将该值转换为所需的类型，使用一组通常不是您想要或期望的规则。这称为类型强制。null 第一个表达式中的 变为 0，"5"第二个表达式中的 变为 5（从字符串到数字）。然而在第三个表达式中，+在数字加法之前尝试字符串连接，因此 1 被转换为"1"（从数字到字符串）。

当无法以明显方式映射到数字的东西（例如"five"或 undefined）转换为数字时，您将获得值 NaN。 对 NaN 的进一步算术运算将继续产生 NaN，因此，如果您发现自己在意想不到的地方得到了 NaN，请查找意外的类型转换。

使用运算符比较相同类型的值时 ==，结果很容易预测：当两个值相同时，结果应该为 true，但 NaN 的情况除外。但是当类型不同时，JavaScript 会使用一组复杂而令人困惑的规则来确定要做什么。在大多数情况下，它只是尝试将其中一个值转换为另一个值的类型。但是，当 null 或 undefined 出现在运算符的两侧时，只有当两侧都是 null 或 undefined 时，结果才会为 true

```js
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

这种行为通常很有用。当你想测试一个值是否具有真实值而不是 null 或 undefined 时，你可以使用 == 或 != 来和 null 进行对比。

如果你想测试某个值是否引用精确值，该怎么办？由于自动类型转换，像 0 == false 表达式也为真。当你不希望发生任何类型转换时，有两个额外的运算符：=== 和 !==。第一个测试一个值是否精确等于另一个值，第二个测试它是否不精确相等。因此，正如预期的那样 "" === false，结果是 false。

我建议谨慎使用三字符比较运算符，以防止意外的类型转换让您陷入困境。但是，当您确定两边的类型相同时，使用较短的运算符就没有问题了。

### 逻辑运算符的短路

逻辑运算符 && 和 || 运算符以特殊的方式处理不同类型的值。它们会将左侧的值转换为布尔类型，以决定要做什么，但根据运算符和转换的结果，它们将返回原始左侧值或右侧值。

例如，当该值可以转换为 true 时，该 || 运算符将返回其左侧的值，否则将返回其右侧的值。当值为布尔值时，这会产生预期的效果，对于其他类型的值，也会执行类似的操作。

```js
console.log(null || "用户");
// → 用户
console.log("Agnes" || "用户");
// → Agnes
```

我们可以使用此功能作为返回默认值的一种方式。如果您有一个可能为空的值，则可以 || 在其后面放置替换值。如果初始值可以转换为 false，你使用后面的值替换它。如果当前值是 0、NaN 或字符串 ("") 都会计为 false，而所有其他值计为 true。这意味着 (0 || -1) 产生 -1，("" || "!?") 产生字符串 "!?"。

运算 ?? 符类似于 ||，但仅当左侧值为 null 或 undefined 时才返回右侧值，而当左侧值为其他可转换为 false 的值时则不返回。通常，这比 || 的行为更可取。

```js
console.log(0 || 100);
// → 100
console.log(0 ?? 100);
// → 0
console.log(null ?? 100);
// → 100
```

&& 运算符的工作原理类似，但方向相反。当其左侧的值转换为 false 时，它将返回该值，否则将返回其右侧的值。

这两个运算符的另一个重要特性是，它们右边的部分只在必要时才进行求值。例如 true || X，无论 X 是什么 —— 即使它是一段做了一些可怕的事情的程序 —— 这将返回 true 同时 X 永远不会被求值。同样 false && X，它为假，也不会执行 X。这称为短路求值。

条件运算符的工作方式类似。对于第二和第三个值，仅评估所选的值。

## 概括

本章我们了解了四种类型的 JavaScript 值：数字、字符串、布尔值和 undefined。这些值通过输入其名称（true, null）或值（13, "abc"）来创建。

您可以使用运算符组合和转换值。我们看到了用于算术的二元运算符（\+、\-、\*、/ 和 %）、字符串连接（\+）、比较（==, !=, ===, !==, <, >, <=, >=）和逻辑（&&, ||, ??）以及几个一元运算符（\- 用于对数字求反，! 用于逻辑求反，以及 typeof 用于查找值的类型）和一个三元运算符 (?:)，用于根据第三个值从两个值中选择一个。

这为您提供了足够的信息，可以将 JavaScript 用作袖珍计算器，但仅此而已。下一章将开始将这些表达式组合成基本程序。