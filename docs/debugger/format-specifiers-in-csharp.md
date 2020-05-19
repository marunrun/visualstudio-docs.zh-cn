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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849839"
---
# <a name="format-specifiers-in-c-in-the-visual-studio-debugger"></a>Visual Studio 调试器中的 C# 中的格式说明符
你可以使用格式说明符更改在“监视”窗口中显示值所用的格式。 还可在“即时”窗口、“命令”窗口、[跟踪点](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)和源窗口中使用格式说明符。 如果将鼠标悬停在这些窗口中的表达式上，结果将采用指定格式显示出现在[数据提示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)中。

若要使用格式说明符，请输入变量表达式，后跟一个逗号和适当的说明符。

## <a name="set-format-specifiers"></a>设置格式说明符
我们将使用以下示例代码：

```csharp
{
    int my_var1 = 0x0065;
    int my_var2 = 0x0066;
    int my_var3 = 0x0067;
}
```

调试期间，将 `my_var1` 变量添加到“监视”窗口，“调试” > “窗口” > “监视” > “监视 1”。 接下来，右键单击变量，然后选择“十六进制显示”。 现在，“监视”窗口显示值 0x0065。 若要看到表示为十进制整数而不是十六进制整数的此值，请在“名称”列的变量名之后添加十进制格式说明符“, d” 。 “值”列现在显示 101。

![WatchFormatCSharp](../debugger/media/watchformatcsharp.png "WatchFormatCSharp")

::: moniker range=">= vs-2019" 

可以通过将逗号 (,) 追加到“监视”窗口中的值来查看可用格式说明符列表并从中进行选择。 

![FormatSpecCSharp](../debugger/media/vs-2019/format-specs-csharp.png "FormatSpecCSharp")

::: moniker-end

## <a name="format-specifiers"></a>格式说明符
下表描述了适用于 Visual Studio 调试器的 C# 格式说明符。

|说明符|格式|原始监视值|显示|
|---------------|------------|--------------------------|--------------|
|ac|强制计算表达式，这在关闭属性的隐式计算和隐式函数调用时十分有用。|消息“用户已关闭隐式函数计算”|\<value>|
|d|十进制整数|0x0065|101|
|dynamic|使用“动态”视图显示指定对象|显示对象的所有成员，包括动态视图|仅显示动态视图|
|h|十六进制整数|61541|0x0000F065|
|nq|不带引号的字符串|"My String"|My String|
|nse|指定行为，而不是格式。 计算带有描述“无副作用”的表达式。 如果表达式无法进行解释，并且只能通过计算（如函数调用）来解析，则会看到错误。|不可用|不可用|
|隐藏|显示所有公共成员和非公共成员|显示公共成员|显示所有成员|
|raw|以项在原始项节点中的显示格式来显示项。 只对代理对象有效。|Dictionary\<T>|Dictionary\<T> 的原始视图|
|results|与实现 IEnumerable 或 IEnumerable\<T> 的类型的变量一起使用，通常是查询表达式的结果。 仅显示包含查询结果的成员。|显示所有成员|显示满足查询条件的成员|

## <a name="see-also"></a>请参阅
- [“监视”和“快速监视”窗口](../debugger/watch-and-quickwatch-windows.md)
- [“自动”和“局部变量”窗口](../debugger/autos-and-locals-windows.md)
