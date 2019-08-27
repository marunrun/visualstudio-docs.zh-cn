---
title: 调试器中的格式说明符 (C#) | Microsoft Docs
ms.date: 11/21/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- expressions [C#], formatting values
- variables [debugger], watch variable symbols
- symbols, watch variable formatting
- QuickWatch dialog box, using format specifiers
- specifiers, watch variable format
- QuickWatch dialog box, format specifiers in C#
- specifiers
- watch variable symbols
- Watch window, format specifiers in C#
- format specifiers, debugger
- debugger, format specifiers recognized by
ms.assetid: 345c8589-5f36-4d34-a58c-e56271687dd6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: caaf36e286f1bdc664ebdbb10e3baf7ed28183e7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849839"
---
# <a name="format-specifiers-in-c-in-the-visual-studio-debugger"></a>Visual Studio 调试器中的 C# 格式说明符
你可以在其中一个值中显示的格式**监视**窗口是通过使用格式说明符。 此外可以使用中的格式说明符**即时**窗口中，**命令**窗口中，在[跟踪点](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)，并在源窗口中。 如果暂停这些窗口中的表达式，该结果将显示在[数据提示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)中指定的格式显示。

若要使用的格式说明符，输入变量表达式后跟一个逗号和适当的说明符。

## <a name="set-format-specifiers"></a>组格式说明符
我们将使用下面的示例代码：

```csharp
{
    int my_var1 = 0x0065;
    int my_var2 = 0x0066;
    int my_var3 = 0x0067;
}
```

添加`my_var1`变量**观看**调试时，窗口**调试** > **Windows** > **观看** > **观看 1**。 接下来，右键单击该变量，并选择**十六进制显示**。 现在**监视**窗口将显示值 0x0065。 若要查看此值为十进制整数而不是十六进制整数，添加十进制格式说明符 **、 d**中**名称**变量名之后的列。 **值**列现在显示**101**。

![WatchFormatCSharp](../debugger/media/watchformatcsharp.png "WatchFormatCSharp")

::: moniker range=">= vs-2019" 

可以查看并通过将逗号 （，） 追加到中的值从可用的格式说明符的列表中选择**监视**窗口。 

![FormatSpecCSharp](../debugger/media/vs-2019/format-specs-csharp.png "FormatSpecCSharp")

::: moniker-end

## <a name="format-specifiers"></a>格式说明符
下表描述了C#设置 Visual Studio 调试器的说明符的格式。

|说明符|格式|原始监视值|显示|
|---------------|------------|--------------------------|--------------|
|ac|强制计算一个表达式，其属性和隐式函数调用的隐式计算处于关闭状态时非常有用。|消息“用户已关闭隐式函数计算”|\<value>|
|d|十进制整数|0x0065|101|
|dynamic|使用“动态”视图显示指定对象|显示对象的所有成员，包括动态视图|仅显示动态视图|
|h|十六进制整数|61541|0x0000F065|
|nq|不带引号的字符串|"My String"|My String|
|nse|指定行为，不格式。 使用"无副作用"的表达式的计算结果。 如果表达式不能解释和才可以解析 （如函数调用） 评估，您将看到错误。|不适用|不适用|
|隐藏|显示所有公共成员和非公共成员|显示公共成员|显示所有成员|
|raw|以项在原始项节点中的显示格式来显示项。 只对代理对象有效。|字典\<T >|字典中的原始视图\<T >|
|results|与实现 IEnumerable 或 IEnumerable 的类型的变量一起使用\<T >，通常在查询表达式的结果。 仅显示包含查询结果的成员。|显示所有成员|显示满足查询条件的成员|

## <a name="see-also"></a>请参阅
- [“监视”和“快速监视”窗口](../debugger/watch-and-quickwatch-windows.md)
- [“自动”和“局部变量”窗口](../debugger/autos-and-locals-windows.md)
