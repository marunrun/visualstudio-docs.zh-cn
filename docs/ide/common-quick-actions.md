---
title: 常见快速操作
description: C# 和 Visual Basic 最常用的快速操作包括修复拼错的关键字或符号、解决合并冲突、删除必要的导入、生成类型、引入局部变量等。
ms.date: 03/28/2018
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: bad97ac5574afd65103263b2ce51a4dfba02741c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652250"
---
# <a name="common-quick-actions"></a>常见快速操作

此主题的各个部分列出了同时适用于 C# 和 Visual Basic 代码的一些常见“快速操作”  。 这些操作是适用于编译器诊断或 Visual Studio 中的内置 [.NET Compiler Platform 分析器](../code-quality/roslyn-analyzers-overview.md)的代码修复  。

## <a name="actions-that-fix-errors"></a>修复错误的操作

本节中的“快速操作”可修复会导致生成失败的代码中的错误。 当“快速操作”可用于修复一行代码中的错误时，边距中或红色波浪线下会显示一个带有红色“x”的灯泡图标。

![“快速操作”错误图标和菜单](media/error-light-bulb-with-code.png)

### <a name="correct-misspelled-symbol-or-keyword"></a>更正拼写错误的符号或关键字

如果在 Visual Studio 中意外拼错类型或关键字，此“快速操作”会自动更正拼写错误。 灯泡菜单“将‘\<拼写错误的单词>’更改为‘\<正确单词>’”中会显示这些项  。 例如:

```csharp
// Before
private viod MyMethod()
{
}

// Change 'viod' to 'void'

// After
private void MyMethod()
{
}
```

```vb
' Before
Function MyFunction as Intger
End Function

' Change 'Intger' to 'Integer'

' After
Function MyFunction as Integer
End Function
```

| 错误 ID | 适用的语言 |
| - | - |
| CS0103、BC30002 | C# 和 Visual Basic |

### <a name="resolve-git-merge-conflict"></a>解决 git 合并冲突

借助这些快速操作，可以通过“接受更改”（即移除冲突的代码和标记）解决 git 合并冲突问题。

```csharp
// Before
private void MyMethod()
{
    if (false)
    {

    }
}

// Take changes from 'HEAD'

// After
private void MyMethod()
{
    if (true)
    {

    }
}
```

| 错误 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| CS8300、BC37284 | C# 和 Visual Basic | Visual Studio 2017 版本 15.3 及更高版本 |

## <a name="actions-that-remove-unnecessary-code"></a>删除不必要代码的操作

### <a name="remove-unnecessary-usingsimports"></a>删除不必要的 using/Import

“删除不必要的 Using/Import”  快速操作将删除当前文件中任何未使用的 `using` 和 `Import` 指令。 选择此项后，将删除未使用的命名空间导入。

| 适用的语言 | 支持的版本 |
| - | - |
| C# 和 Visual Basic | Visual Studio 2015 及更高版本 |

### <a name="remove-unnecessary-cast"></a>删除不必要的 cast

如果你将一种类型强制转换为另一种不需要强制转换的类型，“删除不必要的强制转换”  快速操作可删除不必要的强制转换。

```csharp
// before
int number = (int)3;

// Remove Unnecessary Cast

// after
int number = 3;
```

```vb
' Before
Dim number as Integer = CType(3, Integer)

' Remove Unnecessary Cast

' After
Dim number as Integer = 3
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0004 | C# 和 Visual Basic | Visual Studio 2015 及更高版本 |

### <a name="remove-unused-variables"></a>删除未使用的变量

借助此快速操作，可以从代码中删除已声明但从未用过的变量。

```csharp
// Before
public MyMethod()
{
    var unused = 8;
    var used = 1;
    return DoStuff(used);
}

// Remove unused variables

// After
public MyMethod()
{
    var used = 1;
    return DoStuff(used);
}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| CS0219、BC42024 | C# 和 Visual Basic | Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="remove-type-from-default-value-expression"></a>从“默认”值表达式中删除类型

此快速操作从默认值表达式中删除值类型，并在编译器可推断出表达式类型时使用 [默认文本](/dotnet/csharp/language-reference/operators/default#default-literal)。

```csharp
// Before
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }

// Simplify default expression

// After
void DoWork(CancellationToken cancellationToken = default) { ... }
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0034 | C# 7.1+ | Visual Studio 2017 版本 15.3 及更高版本 |

## <a name="actions-that-add-missing-code"></a>添加缺失代码的操作

### <a name="add-usingsimports-for-types-in-reference-assemblies-nuget-packages-or-other-types-in-your-solution"></a>在引用程序集、NuGet 包或解决方案的其他类型中为类型添加 using/import

位于解决方案其他项目中的 using 类型将自动显示快速操作，但其他类型的快速操作则需要从“工具”>“选项”>“C#”  或“基本”>“高级”  选项卡中启用：

- 建议对引用程序集中的类型使用 using/import
- 建议对 NuGet 包中的类型使用 using/import

启用后，如果使用当前未导入但引用程序集或 NuGet 包中存在的命名空间中的类型，则会创建 using 或 import 指令。

```csharp
// Before
Debug.WriteLine("Hello");

// using System.Diagnostics;

// After
using System.Diagnostics;

Debug.WriteLine("Hello");
```

```vb
' Before
Debug.WriteLine("Hello")

' Imports System.Diagnostics

' After
Imports System.Diagnostics

Debug.WriteLine("Hello")
```

| 诊断 ID | 适用的语言 |
| - | - |
| CS0103、BC30451 | C# 和 Visual Basic|

### <a name="add-missing-casesdefault-caseboth"></a>添加缺少的 case/默认 case/二者

在 C# 中创建 `switch` 语句，或在 Visual Basic 中创建 `Select Case` 语句时，可使用代码操作自动添加缺少的 case 项、默认 case 语句或同时添加二者。

请考虑使用以下枚举和空 `switch` 或 `Select Case` 语句：

```csharp
enum MyEnum
{
    Item1,
    Item2,
    Item3
}

...

MyEnum myEnum = MyEnum.Item1;

switch(myEnum)
{
}
```

```vb
Enum MyEnum
    Item1
    Item2
    Item3
End Enum

...

Dim myEnum as MyEnum = MyEnum.Item1

Select Case myEnum
End Select
```

使用“添加二者”  快速操作可填充缺少的案例，并添加默认案例：

```csharp
switch(myEnum)
{
    case MyEnum.Item1:
        break;
    case MyEnum.Item2:
        break;
    case MyEnum.Item3:
        break;
    default:
        break;
}
```

```vb
Select Case myEnum
    Case MyEnum.Item1
        Exit Select
    Case MyEnum.Item2
        Exit Select
    Case Else
        Exit Select
End Select
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0010 | C# 和 Visual Basic| Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="add-null-checks-for-parameters"></a>添加 null 参数检查

借助此快速操作，可以在代码中添加检查，从而指明参数是否为 null。

```csharp
// Before
class MyClass
{
    public string MyProperty { get; set; }

    public MyClass(string myProperty) // cursor inside myProperty
    {
        MyProperty = myProperty;
    }
}

// Add null check

// After
class MyClass
{
    public string MyProperty { get; set; }

    public MyClass(string myProperty)
    {
        MyProperty = myProperty ?? throw new ArgumentNullException(nameof(myProperty));
    }
}
```

| 适用的语言 | 支持的版本 |
| -------------------- | ---------------- |
| C# 和 Visual Basic| Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="add-argument-name"></a>添加参数名称

```csharp
// Before
var date = new DateTime(1997, 7, 8);

// Include argument name 'year' (include trailing arguments)

// After
var date = new DateTime(year: 1997, month: 7, day: 8);
```

| 适用的语言 | 支持的版本 |
| -------------------- | ---------------- |
| C# 和 Visual Basic| Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="add-braces"></a>添加大括号

“添加大括号”快速操作将单行 `if` 语句包含在大括号内。

```csharp
// Before
if (true)
    return "hello,world";

// Add braces

// After
if (true)
{
    return "hello,world";
}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0011 | C# | Visual Studio 2017 及更高版本 |

### <a name="add-and-order-modifiers"></a>添加修饰符并对其排序

这些快速操作通过对现有辅助功能修饰符排序和添加缺失的辅助功能修饰符来帮助整理修饰符。

```csharp
// Before
enum Color
{
    Red, White, Blue
}

// Add accessibility modifiers

// After
internal enum Color
{
    Red, White, Blue
}
```

```csharp
// Before
static private int thisFieldIsPublic;

// Order modifiers

// After
private static int thisFieldIsPublic;
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0036 | C# 和 Visual Basic| Visual Studio 2017 版本 15.5 及更高版本 |
| IDE0040 | C# 和 Visual Basic| Visual Studio 2017 版本 15.5 及更高版本 |

## <a name="code-transformations"></a>代码转换

### <a name="convert-if-construct-to-switch"></a>将“if”构造转换成“switch”

借助此快速操作，可以将 **if-then-else** 构造转换成 **switch** 构造。

```csharp
// Before
if (obj is string s)
{
  Console.WriteLine("obj is a string: " + s);
}

else if (obj is int i && i > 10)
{
  Console.WriteLine("obj is an int greater than 10");
}

// Convert to switch

// After
switch (obj)
{
  case string s:
    Console.WriteLine("Obj is a string: " + s);
    break;
  case int i when i > 10:
    Console.WriteLine("obj is an int greater than 10");
    break;
}
```

```vb
' Before
If TypeOf obj Is String s Then
    Console.WriteLine("obj is a string: " + s)
Else If TypeOf obj Is Integer i And i > 10 Then
    Console.WriteLine("obj is an int greater than 10")
End If

' Convert to switch

' After
Select Case obj
  Case String s
    Console.WriteLine("Obj is a string: " + s)
    Exit Sub
  Case Integer i when i > 10
    Console.WriteLine("obj is an int greater than 10")
    Exit Sub
End Select
```

| 适用的语言 | 支持的版本 |
| -------------------- | ---------------- |
| C# 和 Visual Basic| Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="convert-to-interpolated-string"></a>转换为内插字符串

类似于 **[String.Format](/dotnet/api/system.string.format#overloads)** 方法，[内插字符串](/dotnet/csharp/language-reference/keywords/interpolated-strings)是使用嵌入式变量来表达字符串的一种简单方式。  此快速操作可识别何时需要将字符串连接在一起或使用 **String.Format**，然后将用法更改为内插字符串。

```csharp
// Before
int num = 3;
string s = string.Format("My string with {0} in the middle", num);

// Convert to interpolated string

// After
int num = 3;
string s = $"My string with {num} in the middle";
```

```vb
' Before
Dim num as Integer = 3
Dim s as String = String.Format("My string with {0} in the middle", num)

' Convert to interpolated string

' After
Dim num as Integer = 3
Dim s As String = $"My string with {num} in the middle"
```

| 适用的语言 | 支持的版本 |
| -------------------- | ---------------- |
| C# 6.0+ 和 Visual Basic 14+ | Visual Studio 2017 及更高版本 |

### <a name="use-object-initializers"></a>使用对象初始值设定项

借助此快速操作，可使用[对象初始值设定项](/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers)，无需调用构造函数并添加赋值语句行。

```csharp
// Before
var c = new Customer();
c.Age = 21;

// Object initialization can be simplified

// After
var c = new Customer() { Age = 21 };
```

```vb
' Before
Dim c = New Customer()
c.Age = 21

' Object initialization can be simplified

' After
Dim c = New Customer() With {.Age = 21}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0017 | C# 和 Visual Basic | Visual Studio 2017 及更高版本 |

### <a name="use-collection-initializers"></a>使用集合初始值设定项

借助此快速操作，可使用[集合初始值设定项](/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers)，而无需多次调用类的 `Add` 方法。

```csharp
// Before
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);

// Collection initialization can be simplified

// After
var list = new List<int> { 1, 2, 3 };
```

```vb
' Before
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)

' Collection initialization can be simplified

' After
Dim list = New List(Of Integer) From {1, 2, 3}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0028 | C# 和 Visual Basic | Visual Studio 2017 及更高版本 |

### <a name="convert-auto-property-to-full-property"></a>将自动属性转换为完整属性

借助此快速操作，可在自动属性与完整属性之间转换。

```csharp
// Before
private int MyProperty { get; set; }

// Convert to full property

// After
private int MyProperty
{
    get { return _myProperty; }
    set { _myProperty = value; }
}
```

```vb
' Before
Public Property Name As String

' Convert to full property

' After
Private _Name As String

Public Property Name As String
    Get
        Return _Name
    End Get
    Set
        _Name = Value
    End Set
End Property
```

| 适用的语言 | 支持的版本 |
| -------------------- | ---------------- |
| C# 和 Visual Basic | Visual Studio 2017 版本 15.5 及更高版本 |

### <a name="convert-block-body-to-expression-bodied-member"></a>将程序块主体转换为 expression-bodied 成员

借助此快速操作，可将程序块主体转换为方法、构造函数、运算符、属性、索引器和访问器的 expression-bodied 成员。

```csharp
//Before
class MyClass4
{
    private int _myProperty;

    public int MyProperty
    {
        get { return _myProperty; }
        set
        {
            _myProperty = value;
        }
    }

    public MyClass4(int myProperty)
    {
        MyProperty = myProperty;
    }

    public void PrintProperty()
    {
        Console.WriteLine(MyProperty);
    }
}

// Use expression body for accessors/constructors/methods

// After
class MyClass4
{
    private int _myProperty;

    public int MyProperty
    {
        get => _myProperty;
        set => _myProperty = value;
    }

    public MyClass4(int myProperty) => MyProperty = myProperty;

    public void PrintProperty() => Console.WriteLine(MyProperty);
}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0021-27 | C# 6.0+ | Visual Studio 2017 及更高版本 |

### <a name="convert-anonymous-function-to-local-function"></a>将匿名函数转换为本地函数

此快速操作将匿名函数转换为本地函数。

```csharp
// Before
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};

// Use local function

// After
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

### <a name="convert-referenceequals-to-is-null"></a>将“ReferenceEquals”转换为“is null”

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0041 | C# 7.0+ | Visual Studio 2017 版本 15.5 及更高版本 |

此快速操作建议尽可能使用[模式匹配](/dotnet/csharp/pattern-matching)，而不是 ```ReferenceEquals``` 代码模式。

```csharp
// Before
var value = "someString";
if (object.ReferenceEquals(value, null))
{
    return;
}

// Use 'is null' check

// After
var value = "someString";
if (value is null)
{
    return;
}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0039 | C# 7.0+ | Visual Studio 2017 版本 15。 及更高版本 |

### <a name="introduce-pattern-matching"></a>引入模式匹配

此快速操作建议使用[模式匹配](/dotnet/csharp/pattern-matching)以及 C# 中的强制转换和 null 检查。

```csharp
// Before
if (o is int)
{
    var i = (int)o;
    ...
}

// Use pattern matching

// After
if (o is int i)
{
    ...
}
```

```csharp
// Before
var s = o as string;
if (s != null)
{
    ...
}

// Use pattern matching

// After
if (o is string s)
{
    ...
}
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0020 | C# 7.0+ | Visual Studio 2017 及更高版本 |
| IDE0019 | C# 7.0+ | Visual Studio 2017 及更高版本 |

### <a name="change-base-for-numeric-literals"></a>更改数字参数的基数

借助此快速操作，可以将数字文本从一种基本数制转换成另一种。 例如，可以将数字更改为十六进制或二进制格式。

```csharp
// Before
int countdown = 2097152;

// Convert to hex

// After
int countdown = 0x200000;
```

```vb
' Before
Dim countdown As Integer = 2097152

' Convert to hex

' After
Dim countdown As Integer = &H200000
```

| 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| C# 7.0+ 和 Visual Basic 14+ | Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="insert-digit-separators-into-literals"></a>将数字分隔符插入数字文本

借助此快速操作，可以将分隔符添加到数字文本值中。

```csharp
// Before
int countdown = 1000000;

// Separate thousands

// After
int countdown = 1_000_000;
```

```vb
' Before
Dim countdown As Integer = 1000000

' Separate thousands

' After
Dim countdown As Integer = 1_000_000
```

| 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| C# 7.0+ 和 Visual Basic 14+ | Visual Studio 2017 版本 15.3 及更高版本 |

### <a name="use-explicit-tuple-names"></a>使用显式元组名称

此快速操作识别可以使用显式元组名称而不是项1、项2 等的位置。

```csharp
// Before
(string name, int age) customer = GetCustomer();
var name = customer.Item1;

// Use explicit tuple name

// After
(string name, int age) customer = GetCustomer();
var name = customer.name;
```

```vb
' Before
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1

' Use explicit tuple name

' After
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0033 | C# 7.0+ 和 Visual Basic 15+ | Visual Studio 2017 及更高版本 |

### <a name="use-inferred-names"></a>使用推断名称

此快速操作指出何时可简化代码，以使用匿名类型中推断的成员名称或元组中推断的元素名称。

```csharp
// Before
var anon = new { age = age, name = name };

// Use inferred member name

// After
var anon = new { age, name };
```

```csharp
// Before
var tuple = (age: age, name: name);

// Use inferred tuple element name

// After
var tuple = (age, name);
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0037 | C# | Visual Studio 2017 版本 15.5 及更高版本 |
| IDE0037 | C# 7.1+ | Visual Studio 2017 版本 15.5 及更高版本 |

### <a name="deconstruct-tuple-declaration"></a>析构元组声明

借助此快速操作，可析构元组变量声明。

```csharp
// Before
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");

//Deconstruct variable declaration

// After
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");
```

| 诊断 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| IDE0042 | C# 7.0+ | Visual Studio 2017 版本 15.5 及更高版本 |

### <a name="make-method-synchronous"></a>使方法同步

如果对方法使用 `async` 或 `Async` 关键字，还应在相应方法中使用 `await` 或 `Await` 关键字。 不过，如果不是这种情况，则会显示快速操作，可用于删除 `async` 或 `Async` 关键字并更改返回类型，从而让方法变成同步方法。 从“快速操作”菜单中使用“使方法同步”  选项。

```csharp
// Before
async Task<int> MyAsyncMethod()
{
    return 3;
}

// Make method synchronous

// After
int MyAsyncMethod()
{
    return 3;
}
```

```vb
' Before
Async Function MyAsyncMethod() As Task(Of Integer)
    Return 3
End Function

' Make method synchronous

' After
Function MyAsyncMethod() As Integer
    Return 3
End Function
```

| 错误 ID | 适用的语言 |
| ------- | -------------------- |
| CS1998、BC42356 | C# 和 Visual Basic |

### <a name="make-method-asynchronous"></a>使方法异步

如果你在方法内使用的是 `await` 或 `Await` 关键字，方法应标记有 `async` 或 `Async` 关键字。 不过，如果不是这种情况，便会看到让方法异步的快速操作。 从“快速操作”菜单中使用“使方法/函数异步”  选项。

```csharp
// Before
int MyAsyncMethod()
{
    return await Task.Run(...);
}

// Make method asynchronous

// After
async Task<int> MyAsyncMethod()
{
    return await Task.Run(...);
}
```

```vb
' Before
Function MyAsyncMethod() as Integer
    Return  Await Task.Run(...)
End Function

' Make method asynchronous

' After
Async Function MyAsyncMethod() As Task(Of Integer)
    Return Await Task.Run(...)
End Function
```

| 错误 ID | 适用的语言 | 支持的版本 |
| ------- | -------------------- | ---------------- |
| CS4032、BC37057 | C# 和 Visual Basic | Visual Studio 2017 及更高版本 |

## <a name="see-also"></a>请参阅

- [快速操作](../ide/quick-actions.md)
