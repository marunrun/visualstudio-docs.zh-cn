---
title: 使用历史调试检查应用程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 629b5d93-39b2-430a-b8ba-d2a47fdf2584
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: efabc8cd185daed4f018e3e4209e391b5bc39f44
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350441"
---
# <a name="inspect-your-app-with-intellitrace-historical-debugging-in-visual-studio-c-visual-basic-c"></a>在 Visual Studio 中使用 IntelliTrace 历史调试检查应用程序 (C#，Visual Basic、 c + +)

可以使用[历史调试](../debugger/historical-debugging.md)向后和向前移动来浏览应用程序的执行情况，以查看其执行状态。

Visual Studio 企业版中可使用 IntelliTrace，但专业版或社区版中无法使用。

## <a name="navigate-your-code-with-historical-debugging"></a>使用历史调试浏览代码

让我们从有 Bug 的简单程序开始。 在 C# 控制台应用程序中，添加以下代码：

```csharp
static void Main(string[] args)
{
    int testInt = 0;
    int resultInt = AddAll(testInt);
    Console.WriteLine(resultInt);
}
private static int AddAll(int j)
{
    for (int i = 0; i < 20; i++)
    {
        j = AddInt(j);
    }
    return j;
}

private static int AddInt(int add)
{
    if (add == 10)
    {
        return add += 25;
    }
    return ++add;
}
```

假定调用 `AddAll()` 后，`resultInt` 的预期值为 20（`testInt` 递增 20 次后的结果）。 （同时假定你看不到 `AddInt()` 中的 bug）。但实际结果为 44。 如何在不单步执行 `AddAll()` 10 次的情况下找到 Bug？ 可以使用历史调试更快、更轻松地查找 bug。 操作方法如下：

1. 在“工具”>“选项”>“IntelliTrace”>“常规”中，请确保启用了 IntelliTrace，然后选择“IntelliTrace 事件和调用信息” 。 如果不选择此选项，则无法看到导航线（如下所述）。

2. 在 `Console.WriteLine(resultInt);` 行上设置断点。

3. 开始调试。 代码执行到断点处。 在“局部变量”窗口中，可以看到 `resultInt` 的值是 44。

4. 打开“诊断工具”窗口（“调试”>“显示诊断工具”） 。 代码窗口应如下所示：

    ![断点处的代码窗口](../debugger/media/historicaldebuggingbreakpoint.png "HistoricalDebuggingBreakpoint")

5. 你应该在左边距旁边看到一个双箭头，就在断点上方。 此区域称为导航条，用于历史调试。 单击该箭头。

    在代码窗口中，应该看待前面的代码行 (`int resultInt = AddIterative(testInt);`) 变为粉红色。 在窗口上方，应该看到一条消息，告知你现在处于历史调试模式中。

    代码窗口现在如下所示：

    ![历史调试模式下的代码窗口](../debugger/media/historicaldebuggingback.png "HistoricalDebuggingBack")

6. 现在，可以单步执行 `AddAll()` 方法（按 **F11** 或导航条中的“单步执行”按钮）。 单步前进（按 **F10** 或导航条中的“转到下一个调用”）。 粉红线现在位于 `j = AddInt(j);` 行。 在这种情况下，按 **F10** 不会单步执行到下一行代码， 而是会单步执行到下一个函数调用。 历史调试在调用之间移动，并跳过不包含函数调用的代码行。

7. 现在单步执行到 `AddInt()` 方法。 应该立即看到此代码中的 Bug。

## <a name="next-steps"></a>后续步骤

此过程仅粗略介绍使用历史调试可以完成的事项。

- 若要在调试时查看快照，请参阅[使用 IntelliTrace 检查以前的应用状态](../debugger/view-historical-application-state.md)。
- 要了解有关不同设置和导航线中不同按钮的效果的详细信息，请参阅 [IntelliTrace 功能](../debugger/intellitrace-features.md)。
