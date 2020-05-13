---
title: 设置变量上的监视 |微软文档
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
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301013"
---
# <a name="watch-variables-with-watch-windows-and-quickwatch"></a>使用"监视窗口"和"快速监视"观看变量

调试时，可以使用 **"监视"** 窗口和**QuickWatch**监视变量和表达式。 仅在调试会话期间，这两个窗口才可用。

**监视**窗口在调试时一次可以显示多个变量。 **"QuickWatch"** 对话框一次显示单个变量，必须先关闭，然后才能继续调试。

如果这是您第一次尝试调试代码，则可能需要在阅读本文之前阅读[绝对初学者](../debugger/debugging-absolute-beginners.md)调试以及[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="observe-variables-with-a-watch-window"></a>使用"监视"窗口观察变量

您可以打开多个 **"监视"** 窗口，并在 **"监视"** 窗口中观察多个变量。

例如，要设置 值 上的监视`a`，`b`请`c`放在 和 在以下代码中：

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

1. 通过单击左边距、选择`c = a + b;`**调试** > **切换断点**或按**F9**在行上设置断点。

1. 通过选择绿色 **"开始"** 箭头或**调试** > **开始调试**，或按**F5**启动调试。 执行在断点处暂停。

1. 通过选择 **"调试** > **窗口** > **监视** > **1"** 或按**Ctrl**+**Alt**+**W** > **1**打开**监视**窗口。

   您可以通过选择窗口**2、3**或**4**来打开其他 **"监视"** 窗口。 **3**

1. 在 **"监视"** 窗口中，选择一个空行，并`a`键入变量 。 对 和`c``b`执行相同的操作。

   ![监视变量](../debugger/media/watchvariables.png "手表变量")

1. 根据需要选择 **"调试** > **步骤"** 或按**F11**以继续调试。 当您循环浏览`for`循环时，"**监视"** 窗口中的变量值会发生变化。

>[!NOTE]
>仅对于C++，
>- 您可能需要限定变量名称的上下文或使用变量名称的表达式。 上下文是变量所在的函数、源文件或模块。 如果必须限定上下文，请使用 **"监视"** 窗口中 **"名称**"中的[上下文运算符 （C++）](../debugger/context-operator-cpp.md)语法。
>
>- **$您可以使用\<寄存器&nbsp;名称>** 或**@&nbsp;寄存器名称>将寄存器名称和变量名称添加到"监视"窗口中的"名称"中>。 \<** **Name** **Watch** 有关详细信息，请参阅 [Pseudovariables](../debugger/pseudovariables.md)。

## <a name="use-expressions-in-a-watch-window"></a>在"监视"窗口中使用表达式

您可以在 **"监视"** 窗口中观察调试器识别的任何有效表达式。

例如，对于上一节中的代码，您可以通过在`(a + b + c) / 3`**"监视"** 窗口中输入来获取三个值的平均值：

![观看表达式](../debugger/media/watchexpression.png "观看表达式")

在**Watch**窗口中计算表达式的规则通常与计算代码语言中的表达式的规则相同。 如果表达式存在语法错误，则预期与代码编辑器中的编译器错误相同。 例如，前面的表达式中的拼写错误在 **"监视"** 窗口中生成此错误：

![监视表达式错误](../debugger/media/watchexpressionerror.png "监视表达式错误")

**"监视"** 窗口中可能会出现一个带有两个波浪线图标的圆圈。 此图标表示调试器不会由于潜在的跨线程依赖关系而计算表达式。 评估代码需要应用中的其他线程暂时运行，但由于您处于中断模式，因此应用中的所有线程通常都会停止。 允许其他线程暂时运行可能会对应用的状态产生意外影响，调试器可能会忽略这些线程上的断点和异常等事件。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-watch-window"></a>在"监视"窗口中搜索

您可以使用每个窗口上方的搜索栏在 **"监视"** 窗口的"名称"、"值"和"类型"列中搜索关键字。 点击 ENTER 或选择其中一个箭头以执行搜索。 要取消正在进行的搜索，请选择搜索栏中的"x"图标。

使用左箭头和右箭头（分别使用 Shift_F3 和 F3）在找到的匹配项之间导航。

![在监视窗口中搜索](../debugger/media/ee-search-watch.png "在监视窗口中搜索")

要使搜索更加彻底，请使用 **"监视"** 窗口顶部的 **"搜索更深**"下拉菜单来选择要搜索到嵌套对象的深度级别。 

## <a name="pin-properties-in-the-watch-window"></a>"监视"窗口中的固定属性

>[!NOTE]
> .NET 核心 3.0 或更高版本支持此功能。

您可以使用"**可固定属性**"工具在"监视"窗口中按其属性快速检查对象。  要使用此工具，请将鼠标悬停在属性上，然后选择显示或右键单击的引脚图标，并在生成的上下文菜单中选择 **"固定成员"作为"收藏夹**"选项。  这将该属性气泡到对象的属性列表的顶部，并且属性名称和值显示在 **"值"** 列中。  要取消固定属性，请再次选择固定图标，或在上下文菜单中选择 **"取消固定成员"作为"收藏夹**"选项。

!["监视"窗口中的固定属性](../debugger/media/basic-pin-watch.gif ""监视"窗口中的固定属性")

在"监视"窗口中查看对象的属性列表时，还可以切换属性名称并筛选出非固定属性。  您可以通过选择监视窗口上方的工具栏中的按钮来访问这两个选项。

::: moniker-end

### <a name="refresh-watch-values"></a><a name="bkmk_refreshWatch"></a>刷新手表值

计算表达式时 **，"监视"** 窗口中可能会出现刷新图标（圆形箭头）。 刷新图标指示错误或过期的值。

要刷新值，请选择刷新图标，或按空格键。 调试器尝试重新计算该表达式。 但是，您可能不希望或能够重新评估表达式，具体取决于未计算该值的原因。

将鼠标悬停在刷新图标上，或查看 **"值"** 列，了解表达式未计算的原因。 原因包括：

- 计算表达式时发生错误，如上一个示例所示。 可能会出现超时，或者变量可能出自范围。

- 表达式具有一个函数调用，该调用可能会在应用中触发副作用。 请参阅[表达式副作用](#bkmk_sideEffects)。

- 禁用属性和隐式函数调用的自动计算。

如果刷新图标由于禁用属性和隐式函数调用而出现，则可以通过在**工具** > **选项** > **调试** > **一般**中选择**启用属性计算和其他隐式函数调用**来启用它。

要演示使用刷新图标：

1. 在**工具** > **选项** > **Debugging**调试 > **一般**中，清除**启用属性计算和其他隐式函数调用**复选框。

1. 输入以下代码，在 **"监视"** 窗口中，在`list.Count`属性上设置监视。

   ```csharp
   static void Main(string[] args)
   {
       List<string> list = new List<string>();
       list.Add("hello");
       list.Add("goodbye");
   }
   ```

1. 开始调试。 **"监视"** 窗口显示类似以下内容的消息：

   ![刷新手表](../debugger/media/refreshwatch.png "刷新手表")

1. 要刷新值，请选择刷新图标，或按空格键。 调试器重新评估表达式。

### <a name="expression-side-effects"></a><a name="bkmk_sideEffects"></a>表达式副作用

评估某些表达式可能会更改变量的值，或者以其他方式影响应用的状态。 例如，计算下列表达式会更改 `var1`的值：

```csharp
var1 = var2
```

此代码可能会导致[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。 副作用可能会通过更改应用的操作方式使调试更加困难。

首次输入具有副作用的表达式仅计算一次。 之后，表达式在 **"监视"** 窗口中显示为灰色，并禁用进一步评估。 工具提示或**值**列说明表达式会导致副作用。 您可以通过选择值旁边的刷新图标来强制重新评估。

防止副作用指定的方法之一是关闭自动功能评估。 在**工具** > **选项** > **Debugging**调试 > **一般**中，取消选择**启用属性计算和其他隐式函数调用**。

仅对于 C#，当关闭属性或隐式函数调用的评估时，可以通过在 **"监视"** 窗口中将**ac**格式修改器添加到变量**Name**来强制评估。 请参阅 [C# 中的格式说明符](../debugger/format-specifiers-in-csharp.md)。

## <a name="use-object-ids-in-the-watch-window-c-and-visual-basic"></a><a name="bkmk_objectIds"></a>在"监视"窗口中使用对象指示（C# 和视觉基本）

有时，您希望观察特定对象的行为。 例如，您可能希望跟踪本地变量引用的对象，该变量已不在范围之内。 在 C# 和 Visual Basic 中，可以创建引用类型的特定实例的对象 ID，并在“监视”**** 窗口中和断点条件下使用它们。 对象 ID 由公共语言运行时 (CLR) 调试服务生成并与该对象关联。

> [!NOTE]
> 对象指示创建不阻止对象被垃圾回收的弱引用。 它们仅对当前调试会话有效。

在以下代码中，`MakePerson()`该方法使用局部变量`Person`创建 一个变量：

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

要找出`Person`方法中 的名称，`DoSomething()`可以在`Person`**"监视"** 窗口中添加对对象 ID 的引用。

1. 创建`Person`对象后，在代码中设置断点。

1. 开始调试。

1. 当执行在断点暂停时，通过选择 **"调试** > **Windows** > **局部变量**"打开 **"局部变量**"窗口。

1. 在 **"局部变量"** 窗口中，右键`Person`单击变量并选择 **"使对象 ID**"。

   您应该在 **"局部变量"** 窗口中**$** 看到一个美元符号 （ ） 加上一个数字，该窗口是对象 ID。

1. 通过右键单击对象 ID 并选择"**添加监视"** 将对象 ID 添加到 **"监视"** 窗口。

1. 在`DoSomething()`方法中设置另一个断点。

1. 继续调试。 当`DoSomething()`执行在 方法中暂停时，"**监视"** 窗口将显示`Person`该对象。

   > [!NOTE]
   > `Person.Name`如果要查看对象的属性，如 ，必须通过选择 **"工具** > **选项** > **调试** > **常规** > **启用属性"属性计算和其他隐式函数调用**来启用属性计算。

## <a name="dynamic-view-and-the-watch-window"></a>动态视图和监视窗口

某些脚本语言（例如 JavaScript 或 Python）使用动态或[鸭子](https://en.wikipedia.org/wiki/Duck_typing)类型，.NET 版本 4.0 和更高版本支持在正常调试窗口中难以观察到的对象。

**"监视"** 窗口将这些对象显示为动态对象，这些对象是从实现<xref:System.Dynamic.IDynamicMetaObjectProvider>接口的类型创建的。 动态对象节点显示动态对象的动态成员，但不允许编辑成员值。

要刷新**动态视图**值，请选择动态对象节点旁边的[刷新图标](#bkmk_refreshWatch)。

要仅显示对象的**动态视图**，请在 **"监视"** 窗口中的动态对象名称之后添加**动态**格式指定器：

- 对于 C#：`ObjectName, dynamic`
- 对于 Visual Basic：`$dynamic, ObjectName`

>[!NOTE]
>- 当您踏进下一行代码时，C# 调试器不会自动重新评估**动态视图中**的值。
>- 可视化基本调试器会自动刷新通过**动态视图**添加的表达式。
>- 计算“动态视图”**** 的成员可能会有[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。

**要插入将对象强制转换为动态对象的新监视变量，请：**

1. 右键单击**动态视图**的任何子级。
1. 选择 **"添加手表**"。 成为`object.name``((dynamic) object).name`并显示在新的 **"监视"** 窗口中。

调试器还会将对象的**动态视图**子节点添加到 **"自动"** 窗口。 要打开 **"自动"** 窗口，请在调试期间选择 **"调试** > **Windows** > **自动**"。

**动态视图**还增强了 COM 对象的调试。 当调试器到达在**System.__ComObject**中包装的 COM 对象时，它会为该对象添加**一个动态视图**节点。

## <a name="observe-a-single-variable-or-expression-with-quickwatch"></a>使用 QuickWatch 观察单个变量或表达式

您可以使用**QuickWatch**观察单个变量。

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

为了观察变量`a`，

1. 在 `a = a + b;` 行上设置一个断点。

1. 开始调试。 执行在断点处暂停。

1. 在代码中选择`a`变量。

1. 选择**调试** > **快速观看**，按**Shift**+**F9**，或右键单击并选择 **"快速观看**"。

   将显示 **"快速监视"** 对话框。 变量`a`位于"**表达式"** 框中，**值**为**1**。

   ![快速观察变量](../debugger/media/quickwatchvariable.png "快速观察变量")

1. 要使用变量计算表达式，请在 **"表达式"** 框中键入表达式`a + b`，然后选择 **"重计算**"。

   ![快速观察表达式](../debugger/media/quickwatchexpression.png "快速观察表达式")

1. 要将"**快速监视"** 中的变量或表达式添加到 **"监视"** 窗口，请选择"**添加监视**"。

1. 选择 **"关闭**"以关闭 **"快速监视"** 窗口。 **（QuickWatch**是一种模式对话框，因此只要它是打开的，您就无法继续调试。

1. 继续调试。 您可以在 **"监视"** 窗口中观察变量。

## <a name="see-also"></a>另请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [首先查看调试](../debugger/debugger-feature-tour.md)
- [调试器窗口](../debugger/debugger-windows.md)
