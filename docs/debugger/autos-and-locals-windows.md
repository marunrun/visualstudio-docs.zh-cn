---
title: 检查变量 -“自动”和“局部变量”窗口 | Microsoft Docs
ms.custom: seodec18
ms.date: 10/18/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b159f631534135ac568fb03dbffa46ae0360fc47
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2019
ms.locfileid: "74904074"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows"></a>检查自动和局部变量窗口中的变量

在调试时，“自动变量”和“局部变量”窗口会显示变量值。  仅在调试会话期间，这两个窗口才可用。 “自动变量”窗口显示当前断点周围使用的变量。 “局部变量”窗口显示在局部范围内定义的变量，通常是当前函数或方法。 如果是首次尝试调试代码，那么在阅读本文前，可能需要阅读[零基础调试](../debugger/debugging-absolute-beginners.md)和[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

 “自动变量”窗口可用于 C#、Visual Basic、C++ 和 Python 代码，但不可用于 JavaScript 或 F#  。

若要打开“自动变量”窗口，请在调试时依次选择“调试” > “窗口” > “自动变量”，或按 Ctrl+Alt+V  >  A 调试       。

若要打开“局部变量”窗口，请在调试时选择“调试” > “窗口” > “局部变量”，或按 Alt+4     。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 的数据可视化效果](/visualstudio/mac/data-visualizations)。

## <a name="use-the-autos-and-locals-windows"></a>使用“自动”和“局部变量”窗口

数组和对象在“自动变量”和“局部变量”窗口中显示为树形控件。  选择变量名称左侧的箭头可展开视图，以显示字段和属性。 以下是“局部变量”窗口中 <xref:System.IO.FileStream?displayProperty=fullName> 对象的示例：

![Locals-FileStream](../debugger/media/locals-filestream.png "Locals-FileStream")

“局部变量”或“自动变量”窗口中的红色值表示自上次评估后值已更改。  此更改可能是在上一个调试会话中进行的，也可能是在窗口中更改了值。

调试器窗口中的默认数字格式为十进制。 若要将其更改为十六进制，请在“局部变量”或“自动”窗口中右键单击，然后选择“十六进制显示”。   此更改会影响所有调试器窗口。

## <a name="edit-variable-values-in-the-autos-or-locals-window"></a>在“自动”或“局部变量”窗口中编辑变量值

若要编辑“自动”或“局部变量”窗口中大多数变量的值，请双击该值并输入新值 。

你可以输入表达式作为一个值，例如 `a + b`。 调试器接受大多数合法的语言表达式。

在本机 C++ 代码中，你可能需要限定变量名的上下文。 有关详细信息，请参阅[上下文运算符（C++）](../debugger/context-operator-cpp.md)。

>[!CAUTION]
>在更改值和表达式之前，请确保你了解其后果。 一些可能存在的问题有：
>
>- 计算某些表达式可能会更改变量的值或以其他方式影响程序的状态。 例如，计算 `var1 = ++var2` 会更改 `var1` 和 `var2` 的值。 据说这些表达式具有[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))。 如果你不了解这些副作用，则可能会导致意外结果。
>
>- 编辑浮点值时，由于要将小数部分从十进制转换为二进制，因此所得的结果可能存在微小误差。 即使编辑看起来无关紧要，也会导致浮点变量中某些数据位发生变化。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-autos-or-locals-window"></a>在“自动”或“局部变量”窗口中搜索

你可以使用每个窗口上方的搜索栏，在“自动”或“局部变量”窗口的“名称”、“值”和“类型”列中搜索关键字 。 点击 Enter 或选择其中一个箭头执行搜索。 要取消正在进行的搜索，请选择搜索栏中的“x”图标。

使用左右箭头（分别为 Shift+F3 和 F3）浏览找到的匹配项。

![在“局部变量”窗口中搜索](../debugger/media/ee-search-locals.png "在“局部变量”窗口中搜索")

要使搜索更加彻底，请使用“自动”或“局部变量”窗口顶部的“深入搜索”下拉列表，选择要在嵌套对象中搜索的深度级别  。 

## <a name="pin-properties-in-the-autos-or-locals-window"></a>在“自动”或“局部变量”窗口中固定属性

> [!NOTE]
> .NET Core 3.0 或更高版本支持此功能。

使用可固定属性工具，可以快速检查“自动”或“局部变量”窗口中对象的属性。  要使用此工具，请将鼠标悬停在某个属性上，并选择出现的固定图标，或右键单击并选择所显示上下文菜单中的“将成员固定到收藏夹”选项。  这会将该属性以气泡形式显示到该对象的属性列表顶部，并且属性名称和值会显示在“值”列中。  要取消固定属性，请再次选择固定图标，或在上下文菜单中选择“取消将成员固定到收藏夹”选项。

![在“局部变量”窗口中固定属性](../debugger/media/basic-pin.gif "在“局部变量”窗口中固定属性")

在“自动”或“局部变量”窗口中查看对象的属性列表时，还可以切换属性名称并筛选出非固定属性。  你可以通过在“自动”或“局部变量”窗口上方的工具栏中选择按钮来访问每个选项。

![筛选器收藏夹属性](../debugger/media/filter-pinned-properties-locals.png "筛选器收藏夹属性")
![切换属性名称](../debugger/media/toggle-property-names.gif "切换属性名称")

::: moniker-end

## <a name="change-the-context-for-the-autos-or-locals-window"></a>更改“自动”或“局部变量”窗口的上下文

可使用“调试位置”工具栏选择所需的函数、线程或进程，这将更改“自动”和“局部变量”窗口的上下文。  

要启用“调试位置”工具栏，请单击工具栏区域的空白部分，然后从下拉列表中选择“调试位置”，或选择“视图” > “工具栏” > “调试位置”    。

设置断点并开始调试。 命中断点时，执行将暂停，你可以在“调试位置”工具栏中查看位置。

![“调试位置”工具栏](../debugger/media/debuglocationtoolbar.png "“调试位置”工具栏")

## <a name="variables-in-the-autos-window-c-c-visual-basic-python"></a><a name="bkmk_whatvariables"></a> “自动”窗口中的变量（C#、C++、Visual Basic 和 Python）

不同的代码语言在“自动”窗口中显示不同的变量。

- 在 C# 和 Visual Basic 中，“自动”窗口显示当前或前一行中使用的任何变量。 例如，在 C# 或 Visual Basic 代码中，声明以下四个变量：

   ```csharp
       public static void Main()
       {
          int a, b, c, d;
          a = 1;
          b = 2;
          c = 3;
          d = 4;
       }
   ```

   在 `c = 3;` 行上设置断点并启动调试器。 当执行暂停时，“自动”窗口将显示：

   ![Autos-CSharp](../debugger/media/autos-csharp.png "Autos-CSharp")

   `c` 的值为 0，因为尚未执行 `c = 3` 行。

- 在 C++ 中，“自动”窗口将显示当前行（执行暂停的行）前面至少三行使用的变量。 例如，在 C++ 代码中，声明六个变量：

   ```C++
       void main() {
           int a, b, c, d, e, f;
           a = 1;
           b = 2;
           c = 3;
           d = 4;
           e = 5;
           f = 6;
       }
   ```

    在 `e = 5;` 行上设置断点并运行调试器。 当执行停止时，“自动”窗口将显示：

    ![Autos-C++](../debugger/media/autos-cplus.png "Autos-C++")

    未初始化变量 `e`，因为尚未执行 `e = 5` 行。

## <a name="view-return-values-of-method-calls"></a><a name="bkmk_returnValue"></a> View return values of method calls
 在 .NET 和 C++ 代码中，当你单步跳过或单步跳出方法调用时，可以在“自动”窗口检查返回值。 当方法调用返回值不存储在局部变量中时，查看这些值非常有用。 一个方法可以用作参数，也可以用作其他方法的返回值。

 例如，下面的 C# 代码将添加两个函数的返回值：

```csharp
static void Main(string[] args)
{
    int a, b, c, d;
    a = 1;
    b = 2;
    c = 3;
    d = 4;
    int x = sumVars(a, b) + subtractVars(c, d);
}

private static int sumVars(int i, int j)
{
    return i + j;
}

private static int subtractVars(int i, int j)
{
    return j - i;
}
```

要在“自动”窗口中查看 `sumVars()` 和 `subtractVars()` 方法调用的返回值，请执行以下操作：

1. 在 `int x = sumVars(a, b) + subtractVars(c, d);` 行上设置断点。

1. 开始调试，且当执行在断点处暂停时，选择“单步跳过”或按 F10 。 你应在“自动”窗口中看到以下返回值：

  ![自动窗口返回值 C#](../debugger/media/autosreturnvaluecsharp2.png "自动窗口返回值 C#")

## <a name="see-also"></a>请参阅

- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [初探调试](../debugger/debugger-feature-tour.md)
- [调试器窗口](../debugger/debugger-windows.md)
