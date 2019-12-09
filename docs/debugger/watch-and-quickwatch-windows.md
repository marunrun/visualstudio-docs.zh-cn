---
title: 设置监视变量 |Microsoft Docs
ms.custom: seodec18
ms.date: 10/11/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.watch
helpviewer_keywords:
- debugging [Visual Studio], Watch window
- expressions [debugger], evaluating
- variables [debugger], evaluating
- expression evaluation
- registers, evaluating
- debugging [Visual Studio], expression evaluation
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ea3d2a1e82e92473859fef29754fbb831cf3685b
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2019
ms.locfileid: "74904037"
---
# <a name="watch-variables-with-watch-windows-and-quickwatch"></a>通过 "监视" 窗口和 "快速监视" 监视变量

进行调试时，可以使用 "**监视**" 窗口和 "**快速**监视" 来监视变量和表达式。 仅在调试会话期间，这两个窗口才可用。

**监视**窗口可以在调试时一次显示多个变量。 "**快速监视**" 对话框一次显示一个变量，必须先关闭，然后才能继续调试。

如果这是您第一次尝试调试代码，则在完成本文之前，您可能需要阅读[调试绝对](../debugger/debugging-absolute-beginners.md)和[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="observe-variables-with-a-watch-window"></a>观察带有监视窗口的变量

您可以打开多个 "**监视**" 窗口，并在 "**监视**" 窗口中观察多个变量。

例如，若要在以下代码中设置对 `a`、`b`和 `c` 的值的监视：

```C++
int main()
{
    int a, b, c;
    a = 1;
    b = 2;
    c = 0;

    for (int i = 0; i < 10; i++)
    {
        a++;
        b *= 2;
        c = a + b;
    }

    return 0;
}

```

1. 在 `c = a + b;` 行上设置断点，方法是单击左边距，选择 "**调试**" > **切换断点**或按**F9**。

1. 通过选择 "绿色**开始**" 箭头或 "**调试**" ** > 启动调试**，或按**F5**。 执行在断点处暂停。

1. 通过选择 "**调试**" > **Windows** > **watch** > **watch 1**"打开"**监视**"窗口，或按**Ctrl**+**Alt**+**W** > **1**"。

   可以通过选择 "windows **2**"、" **3**" 或 " **4**" 打开其他**监视**窗口。

1. 在 "**监视**" 窗口中，选择一个空行，然后键入 variable `a`。 对 `b` 和 `c`执行相同操作。

   ![监视变量](../debugger/media/watchvariables.png "WatchVariables")

1. 继续调试，方法是选择 "**调试**" > **单步**执行，或根据需要按**F11** 。 在循环访问 `for` 循环时，"**监视**" 窗口中的变量值将发生变化。

>[!NOTE]
>仅C++适用于
>- 您可能需要限定变量名的上下文或使用变量名的表达式。 上下文是变量所在的函数、源文件或模块。 如果需要限定上下文，请在 "**监视**" 窗口中的**名称**中使用[上下文C++运算符（）](../debugger/context-operator-cpp.md)语法。
>
>- 可以在 "**监视**"**窗口中使用** **$\<注册&nbsp;名称 >** 或 **@\<注册&nbsp;名称 >** 来添加注册名称和变量名称。 有关详细信息，请参阅 [Pseudovariables](../debugger/pseudovariables.md)。

## <a name="use-expressions-in-a-watch-window"></a>在监视窗口中使用表达式

可以在 "**监视**" 窗口中观察调试器识别的任何有效表达式。

例如，对于之前部分中的代码，可以通过在 "**监视**" 窗口中输入 `(a + b + c) / 3` 来获取这三个值的平均值：

![监视表达式](../debugger/media/watchexpression.png "监视表达式")

在 "**监视**" 窗口中计算表达式的规则通常与在代码语言中计算表达式的规则相同。 如果表达式具有语法错误，则与代码编辑器中的编译器错误应相同。 例如，前面的表达式中的拼写错误会在 "**监视**" 窗口中产生此错误：

![监视表达式错误](../debugger/media/watchexpressionerror.png "监视表达式错误")

"**监视**" 窗口中可能会显示具有两个波浪线图标的圆圈。 此图标表示由于潜在的跨线程依赖关系，调试器不会计算表达式。 评估代码需要应用中的其他线程暂时运行，但由于处于中断模式，因此应用中的所有线程通常都处于停止状态。 允许其他线程暂时运行可能会对应用的状态产生意外影响，并且调试器可能会忽略断点和这些线程上的异常等事件。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-watch-window"></a>在监视窗口中搜索

可以使用每个窗口上方的搜索栏在 "**监视**" 窗口的 "名称"、"值" 和 "类型" 列中搜索关键字。 点击输入或选择一个箭头，执行搜索。 若要取消正在进行的搜索，请选择搜索栏中的 "x" 图标。

使用左右箭头（分别为 Shift + F3 和 F3）在找到的匹配项之间导航。

![在监视窗口中搜索](../debugger/media/ee-search-watch.png "在监视窗口中搜索")

若要使搜索更全面或更不全面，请使用 "**监视**" 窗口顶部的 "**搜索更深层**" 下拉列表来选择要在嵌套对象中搜索的深度级别。 

## <a name="pin-properties-in-the-watch-window"></a>固定监视窗口中的属性

>[!NOTE]
> .NET Core 3.0 或更高版本支持此功能。

您可以使用**Pinnable 属性**工具在监视窗口中按对象的属性快速检查对象。  若要使用此工具，请将鼠标悬停在属性上，并选择显示或右键单击的固定图标，然后在生成的上下文菜单中选择 "将**成员固定到收藏夹**" 选项。  这会将该属性冒泡到对象的属性列表的顶部，并且属性名称和值会显示在 "**值**" 列中。  若要取消固定属性，请再次选择 "固定" 图标，或在上下文菜单中选择 "**取消固定成员**" 选项。

![固定监视窗口中的属性](../debugger/media/basic-pin-watch.gif "固定监视窗口中的属性")

在监视窗口中查看对象的属性列表时，还可以切换属性名称并筛选出未固定的属性。  您可以通过在 "监视" 窗口上方的工具栏中选择相应的按钮来访问这两个选项。

::: moniker-end

### <a name="bkmk_refreshWatch"></a>刷新监视值

计算表达式时，"**监视**" 窗口中可能会出现刷新图标（环形箭头）。 刷新图标指示错误或过期的值。

若要刷新值，请选择 "刷新" 图标或按空格键。 调试器尝试重新计算该表达式。 不过，您可能不希望或无法重新计算表达式的值，具体取决于不计算值的原因。

将鼠标悬停在刷新图标上，或查看 "**值**" 列，了解表达式未计算的原因。 原因包括：

- 计算表达式时出现错误，如前面的示例中所示。 可能出现超时，或变量可能超出范围。

- 表达式具有可在应用程序中触发副作用的函数调用。 请参阅[表达式](#bkmk_sideEffects)的副作用。

- 禁用属性和隐式函数调用的自动计算。

如果因为属性和隐式函数调用的自动求值被禁用而出现刷新图标，则可以通过在 "**工具**" 中选择 "**启用属性求值和其他隐式函数调用**" > **选项**来启用它 > **调试** > "**常规**"。

若要演示如何使用刷新图标：

1. 在 "**工具**" > **选项**" > **调试** > "**常规**"中，清除"**启用属性求值和其他隐式函数调用**"复选框。

1. 输入以下代码，并在 "**监视**" 窗口中设置 "监视" `list.Count` 属性。

   ```csharp
   static void Main(string[] args)
   {
       List<string> list = new List<string>();
       list.Add("hello");
       list.Add("goodbye");
   }
   ```

1. 开始调试。 "**监视**" 窗口显示类似于以下消息的内容：

   ![刷新监视](../debugger/media/refreshwatch.png "刷新监视")

1. 若要刷新值，请选择 "刷新" 图标或按空格键。 调试器重新评估表达式。

### <a name="bkmk_sideEffects"></a>表达式副作用

计算某些表达式可以更改变量的值，否则会影响应用的状态。 例如，计算下列表达式会更改 `var1`的值：

```csharp
var1 = var2
```

此代码可能会导致[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。 副作用可能会改变应用运行的方式，从而使调试变得更加困难。

仅在第一次输入带有副作用的表达式时，才计算此表达式。 之后，该表达式在 "**监视**" 窗口中显示为灰色，并禁用其他评估。 Tooltip 或**Value**列说明表达式导致了副作用。 可以通过选择显示在值旁边的 "刷新" 图标来强制进行重新评估。

阻止副作用指定的一种方法是关闭自动功能计算。 在**工具** > **选项**" > **调试** > "**常规**"中，取消选择"**启用属性求值和其他隐式函数调用**"。

仅C#对于，当关闭属性计算或隐式函数调用时，可以通过在 "**监视**" 窗口中将 " **ac**格式" 修饰符添加到变量**名称**来强制进行计算。 请参阅 [C# 中的格式说明符](../debugger/format-specifiers-in-csharp.md)。

## <a name="bkmk_objectIds"></a>在监视窗口中使用对象 Id （C#和 Visual Basic）

有时，您想要观察特定对象的行为。 例如，你可能想要跟踪局部变量超出范围后由该变量引用的对象。 在 C# 和 Visual Basic 中，可以创建引用类型的特定实例的对象 ID，并在“监视”窗口中和断点条件下使用它们。 对象 ID 由公共语言运行时 (CLR) 调试服务生成并与该对象关联。

> [!NOTE]
> 对象 Id 创建弱引用，不会阻止对象被垃圾回收。 它们仅对当前调试会话有效。

在下面的代码中，`MakePerson()` 方法使用局部变量创建 `Person`：

```csharp
class Person
{
    public Person(string name)
    {
        Name = name;
    }
    public string Name { get; set; }
}

public class Program
{
    static List<Person> _people = new List<Person>();
    public static void Main(string[] args)
    {
        MakePerson();
        DoSomething();
    }

    private static void MakePerson()
    {
        var p = new Person("Bob");
        _people.Add(p);
    }

    private static void DoSomething()
    {
        // more processing
         Console.WriteLine("done");
    }
}
```

若要确定 `DoSomething()` 方法中 `Person` 的名称，可以在 "**监视**" 窗口中添加对 `Person` 对象 ID 的引用。

1. 创建 `Person` 对象之后，在代码中设置断点。

1. 开始调试。

1. 当执行在断点处暂停时，通过选择 "**调试**" > **Windows** > "**局部变量**" 来打开 "**局部变量**" 窗口。

1. 在 "**局部变量**" 窗口中，右键单击 `Person` 变量，然后选择 "**创建对象 ID**"。

   你应该会在 "**局部变量**" 窗口中看到美元符号（ **$** ）加上一个数字，它是对象 ID。

1. 右键单击对象 ID，然后选择 "**添加监视**"，将对象 id 添加到 "**监视**" 窗口。

1. 在 `DoSomething()` 方法中设置另一个断点。

1. 继续调试。 当执行在 `DoSomething()` 方法中暂停时，"**监视**" 窗口将显示 `Person` 对象。

   > [!NOTE]
   > 若要查看对象的属性（如 `Person.Name`），必须通过选择 "**工具**" > **选项**来启用属性求值， > **调试** >  > **常规**"**启用属性求值和其他隐式函数调用**。

## <a name="dynamic-view-and-the-watch-window"></a>动态视图和监视窗口

某些脚本语言（例如，JavaScript 或 Python）使用[动态或有类型的类型](https://en.wikipedia.org/wiki/Duck_typing)，.net 版本4.0 和更高版本支持在正常调试窗口中难以观察的对象。

"**监视**" 窗口将这些对象显示为动态对象，这些对象是从实现 <xref:System.Dynamic.IDynamicMetaObjectProvider> 接口的类型创建的。 动态对象节点显示动态对象的动态成员，但不允许编辑成员值。

若要刷新**动态视图**值，请选择 "动态对象" 节点旁边的 "[刷新" 图标](#bkmk_refreshWatch)。

若要仅显示对象的**动态视图**，请在 "**监视**" 窗口中的动态对象名称后添加一个**动态**格式说明符：

- 对于 C#：`ObjectName, dynamic`
- 对于 Visual Basic：`$dynamic, ObjectName`

>[!NOTE]
>- 当C#你单步执行下一行代码时，调试器不会自动重新计算**动态视图**中的值。
>- Visual Basic 调试器会自动刷新通过 "**动态视图**" 添加的表达式。
>- 计算“动态视图”的成员可能会有[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。

**插入一个将对象强制转换为动态对象的新监视变量：**

1. 右键单击**动态视图**的任何子级。
1. 选择 "**添加监视**"。 `object.name` 将变成 `((dynamic) object).name` 并显示在新的 "**监视**" 窗口中。

调试器还会将对象的 "**动态视图**" 子节点添加到 **"自动**" 窗口。 若要打开 "自动 **" 窗口，请选择 "调试**"，然后选择 "**调试**" > **Windows** ** > 自动**。

**动态视图**还增强了 COM 对象的调试。 当调试器获取包装在 **__ComObject**中的 COM 对象时，它将为该对象添加**动态视图**节点。

## <a name="observe-a-single-variable-or-expression-with-quickwatch"></a>使用 "快速监视" 观察单个变量或表达式

您可以使用 "**快速监视**" 观察单个变量。

例如，对于以下代码：

```csharp
static void Main(string[] args)
{
    int a, b;
    a = 1;
    b = 2;
    for (int i = 0; i < 10; i++)
    {
        a = a + b;
    }
}
```

若要观察 `a` 变量，

1. 在 `a = a + b;` 行上设置断点。

1. 开始调试。 执行在断点处暂停。

1. 在代码中选择变量 `a`。

1. 选择 "**调试**" > "**快速监视**"，按**Shift**+**F9**，或右键单击并选择 "**快速监视**"。

   此时会显示 "**快速监视**" 对话框。 `a` 变量位于 "**表达式**" 框中，其**值**为**1**。

   ![快速监视变量](../debugger/media/quickwatchvariable.png "快速监视变量")

1. 若要使用变量计算表达式，请在 "**表达式**" 框中键入表达式，如 `a + b`，然后选择 "重新**计算**"。

   ![快速监视表达式](../debugger/media/quickwatchexpression.png "快速监视表达式")

1. 若要将变量或表达式从 "**快速**监视" 添加到 "**监视**" 窗口，请选择 "**添加监视**"。

1. 选择 "**关闭**" 以关闭 "**快速监视**" 窗口。 （"**快速监视**" 是一个模式对话框，因此只要它处于打开状态，就无法继续进行调试。）

1. 继续调试。 可以在 "**监视**" 窗口中观察到该变量。

## <a name="see-also"></a>另请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [首先查看调试](../debugger/debugger-feature-tour.md)
- [调试器窗口](../debugger/debugger-windows.md)
