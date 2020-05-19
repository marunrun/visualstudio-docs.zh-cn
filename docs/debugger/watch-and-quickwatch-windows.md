---
title: 对变量设置监视 | Microsoft Docs
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301013"
---
# <a name="watch-variables-with-watch-windows-and-quickwatch"></a>使用“监视”和“快速监视”窗口监视变量

调试时，可以使用“监视”和“快速监视”窗口来监视变量和表达式 。 仅在调试会话期间，这两个窗口才可用。

“监视”窗口在调试时可以一次显示多个变量。 “快速监视”对话框一次显示一个变量，且必须先关闭然后才能继续调试。

如果是首次尝试调试代码，那么在阅读本文前，可能需要阅读[零基础调试](../debugger/debugging-absolute-beginners.md)和[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="observe-variables-with-a-watch-window"></a>使用“监视”窗口观察变量

可以打开多个“监视”窗口，并在一个“监视”窗口中观察多个变量 。

例如，要对以下代码中的 `a`、`b`和 `c` 值设置监视，请执行以下操作：

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

1. 单击左边距，选择“调试” > “切换断点”，或按 F9，在 `c = a + b;` 行上设置断点  。

1. 选择绿色“启动”箭头或“调试” > “启动调试”，或者按 F5，启动调试   。 执行在断点处暂停。

1. 选择“调试” > “窗口” > “监视” > “监视 1”，或按 Ctrl+Alt+W > 1 打开“监视”窗口        。

   选择窗口 2、3 或 4 打开其他“监视”窗口   。

1. 在“监视”窗口中，选择一个空行，然后键入变量 `a`。 对 `b` 和 `c` 执行相同的操作。

   ![监视变量](../debugger/media/watchvariables.png "监视变量")

1. 根据需要，选择“调试” > “单步调试”或按 F11 来继续调试  。 在遍历 `for` 循环时，“监视”窗口中的变量值随之更改。

>[!NOTE]
>C++ 特定注意事项
>- 可能需要限定变量名的上下文或使用变量名的表达式。 上下文指变量所处的函数、源文件或模块。 如果需要限定上下文，请在“监视”窗口内的“名称”中使用[上下文运算符 (C++)](../debugger/context-operator-cpp.md) 语法 。
>
>- 可以使用 $\<register&nbsp;name> 或 @\<register&nbsp;name> 将寄存器名称或变量名称添加到“监视”窗口内的“名称”中   。 有关详细信息，请参阅 [Pseudovariables](../debugger/pseudovariables.md)。

## <a name="use-expressions-in-a-watch-window"></a>在“监视”窗口中使用表达式

你可以在“监视”窗口中观察调试器能识别的任何有效表达式。

例如，对于上一部分的代码，可以通过在“监视”窗口输入 `(a + b + c) / 3` 来获得这三个值的平均值：

![监视表达式](../debugger/media/watchexpression.png "监视表达式")

“监视”窗口中的表达式求值规则通常与代码语言中表达式的求值规则相同。 如果表达式存在语法错误，则在代码编辑器中将会出现相同的编译器错误。 例如，上一个表达式中的拼写错误会在“监视”窗口中生成此错误：

![监视表达式错误](../debugger/media/watchexpressionerror.png "监视表达式错误")

“监视”窗口中可能会出现带有双波浪线图标的圆圈。 此图标表示由于潜在的跨线程依赖关系，调试器不会对表达式求值。 对代码求值需要应用中的其他线程暂时运行，但由于处于中断模式，应用中的所有线程通常都会停止。 允许其他线程暂时运行可能会对应用状态产生意外影响，并且调试器可能会忽略断点和这些线程上的异常等事件。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-watch-window"></a>在“监视”窗口中搜索

你可以使用每个窗口上方的搜索栏，在“监视”窗口的“名称”、“值”和“类型”列中搜索关键字。 点击 Enter 或选择其中一个箭头执行搜索。 要取消正在进行的搜索，请选择搜索栏中的“x”图标。

使用左右箭头（分别为 Shift+F3 和 F3）浏览找到的匹配项。

![在“监视”窗口中搜索](../debugger/media/ee-search-watch.png "在“监视”窗口中搜索")

要使搜索更加彻底，请使用“监视”窗口顶部的“深入搜索”下拉列表，选择要在嵌套对象中搜索的深度级别 。 

## <a name="pin-properties-in-the-watch-window"></a>在“监视”窗口中固定属性

>[!NOTE]
> .NET Core 3.0 或更高版本支持此功能。

使用可固定属性工具，可以快速检查“监视”窗口中对象的属性。  要使用此工具，请将鼠标悬停在某个属性上，并选择出现的固定图标，或右键单击并选择所显示上下文菜单中的“将成员固定到收藏夹”选项。  这会将该属性以气泡形式显示到该对象的属性列表顶部，并且属性名称和值会显示在“值”列中。  要取消固定属性，请再次选择固定图标，或在上下文菜单中选择“取消将成员固定到收藏夹”选项。

![在“监视”窗口中固定属性](../debugger/media/basic-pin-watch.gif "在“监视”窗口中固定属性")

在“监视”窗口中查看对象的属性列表时，还可以切换属性名称并筛选出非固定属性。  你可以通过在“监视”窗口上方的工具栏中选择按钮来访问这两个选项。

::: moniker-end

### <a name="refresh-watch-values"></a><a name="bkmk_refreshWatch"></a> 刷新监视值

对表达式求值时，“监视”窗口中可能会出现刷新图标（环形箭头）。 监视图标指示错误或已过期的值。

要刷新值，请选择刷新图标或按空格键。 调试器尝试重新计算该表达式。 但是，你可能不希望或无法重新对表达式求值，这取决于未计算该值的原因。

将鼠标悬停在刷新图标上或查看“值”列，确定为对表达式求值的原因。 原因包括：

- 在对表达式求值时发生错误，如上一例所示。 可能超时，或者变量可能超出范围。

- 该表达式包含一个函数调用，可在应用中触发副作用。 请参阅[表达式副作用](#bkmk_sideEffects)。

- 自动属性求值和隐式函数调用已禁用。

如果因为禁用了自动属性求值和隐式函数调用而出现刷新图标，则可以通过在“工具” > “选项” > “调试” > “常规”中选择“启用属性求值和其他隐式函数调用”来启用它    。

刷新图标的使用方式如下：

1. 在“工具” > “选项” > “调试” > “常规”中，清除“启用属性求值和其他隐式函数调用”复选框    。

1. 输入以下代码，然后在“监视”窗口中，对 `list.Count` 属性设置监视。

   ```csharp
   static void Main(string[] args)
   {
       List<string> list = new List<string>();
       list.Add("hello");
       list.Add("goodbye");
   }
   ```

1. 开始调试。 “监视”窗口显示类似于以下消息的内容：

   ![刷新监视](../debugger/media/refreshwatch.png "刷新监视")

1. 要刷新值，请选择刷新图标或按空格键。 调试器会对表达式重新求值。

### <a name="expression-side-effects"></a><a name="bkmk_sideEffects"></a> 表达式副作用

对某些表达式求值可能会更改变量的值或对应用状态造成其他影响。 例如，计算下列表达式会更改 `var1`的值：

```csharp
var1 = var2
```

此代码可能会导致[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。 副作用会改变应用的运行方式，使调试变得更加困难。

具有副作用的表达式只会在首次输入时进行一次求值。 之后，表达式在“监视”窗口中显示为灰色，并禁用进一步的求值。 工具提示或“值”列说明了表达式会导致副作用。 可以通过选择值旁边显示的刷新图标来强制进行重新求值。

防止副作用的一种方法是禁用自动函数求值。 在“工具” > “选项” > “调试” > “常规”中，取消选择“启用属性求值和其他隐式函数调用”    。

禁用属性求值或隐式函数调用后，可通过将 ac 格式修饰符添加到“监视”窗口内的变量“名称”中来强制进行求值，但这仅适用于 C#  。 请参阅 [C# 中的格式说明符](../debugger/format-specifiers-in-csharp.md)。

## <a name="use-object-ids-in-the-watch-window-c-and-visual-basic"></a><a name="bkmk_objectIds"></a> 在“监视”窗口中使用“对象 ID”（C# 和 Visual Basic）

有时，你想要观察特定对象的行为。 例如，你可能想要在一个局部变量超出范围时跟踪一个由该变量引用的对象。 在 C# 和 Visual Basic 中，可以创建引用类型的特定实例的对象 ID，并在“监视”窗口中和断点条件下使用它们。 对象 ID 由公共语言运行时 (CLR) 调试服务生成并与该对象关联。

> [!NOTE]
> 对象 ID 创建不会阻止对象被垃圾回收的弱引用。 它们仅对当前调试会话有效。

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

要确定 `DoSomething()` 方法中 `Person` 的名称，可以在“监视”窗口中添加对 `Person` 对象 ID 的引用。

1. 创建 `Person` 对象后在代码中设置断点。

1. 开始调试。

1. 当执行在断点处暂停时，选择“调试” > “窗口” > “局部变量”来打开“局部变量”窗口   。

1. 在“局部变量”窗口中，右键单击 `Person` 变量，然后选择“生成对象 ID” 。

   你应该会在“局部变量”窗口中看到一个美元符号 ($) 加一个数字，这便是对象 ID 。

1. 右键单击对象 ID，然后选择“添加监视”，将对象 ID 添加到“监视”窗口 。

1. 在 `DoSomething()` 方法中设置另一个断点。

1. 继续调试。 当执行在 `DoSomething()` 方法处暂停时，“监视”窗口会显示 `Person` 对象。

   > [!NOTE]
   > 如果想要查看对象的属性（如 `Person.Name`），则必须通过选择“工具” > “选项” > “调试” > “常规” > “启用属性求值和其他隐式函数调用”来启用属性求值    。

## <a name="dynamic-view-and-the-watch-window"></a>动态视图和“监视”窗口

某些脚本语言（例如 JavaScript 或 Python）使用 dynamic 或 [duck](https://en.wikipedia.org/wiki/Duck_typing) 类型，.NET 4.0 及更高版本支持在一般调试窗口中难以观察的对象。

“监视”窗口将这些对象显示为动态对象，这些对象是从实现 <xref:System.Dynamic.IDynamicMetaObjectProvider> 接口的类型创建的。 动态对象节点显示动态对象的动态成员，但不允许编辑成员值。

要刷新“动态视图”值，请选择动态对象节点旁边的[刷新图标](#bkmk_refreshWatch)。

要仅显示对象的“动态视图”，请在“监视”窗口中的动态对象名称后添加 dynamic 格式说明符  ：

- 对于 C#：`ObjectName, dynamic`
- 对于 Visual Basic：`$dynamic, ObjectName`

>[!NOTE]
>- 在执行下一行代码时，C# 调试器不会自动重新计算“动态视图”中的值。
>- Visual Basic 调试器会自动刷新通过“动态视图”添加的表达式。
>- 计算“动态视图”的成员可能会有[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。

**要插入将对象强制转换为 dynamic 对象的新监视变量，请执行以下操作：**

1. 右键单击“动态视图”的任意子级。
1. 选择“添加监视”。 `object.name` 将变成 `((dynamic) object).name` 并显示在新的“监视”窗口中。

调试器还会将对象的“动态视图”子节点添加到“自动”窗口中 。 要打开“自动”窗口，请在调试时依次选择“调试” > “窗口” > “自动”   。

“动态视图”还可以提升 COM 对象的调试。 当调试器遇到包装在 System.__ComObject 中的 COM 对象时，会为该对象添加一个“动态视图”节点 。

## <a name="observe-a-single-variable-or-expression-with-quickwatch"></a>使用“快速监视”观察单个变量或表达式

你可以使用“快速监视”观察单个变量。

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

要观察 `a` 变量，请执行以下操作：

1. 在 `a = a + b;` 行上设置断点。

1. 开始调试。 执行在断点处暂停。

1. 在代码中选择变量 `a`。

1. 选择“调试” > “快速监视”，按 Shift+F9，或右键单击并选择“快速监视”    。

   此时将显示“快速监视”对话框。 `a` 变量位于“表达式”框中，值为 1  。

   ![快速监视变量](../debugger/media/quickwatchvariable.png "快速监视变量")

1. 要使用变量对表达式求值，请在“表达式”框中键入表达式（如 `a + b`），然后选择“重新求值” 。

   ![快速监视表达式](../debugger/media/quickwatchexpression.png "快速监视表达式")

1. 要将“快速监视”中的变量或表达式添加到“监视”窗口，请选择“添加监视”  。

1. 选择“关闭”以关闭“快速监视”窗口 。 （“快速监视”是一个模态对话框，因此只要该对话框处于打开状态，就无法继续进行调试）。

1. 继续调试。 你可以在“监视”窗口中观察变量。

## <a name="see-also"></a>请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [初探调试](../debugger/debugger-feature-tour.md)
- [调试器窗口](../debugger/debugger-windows.md)
