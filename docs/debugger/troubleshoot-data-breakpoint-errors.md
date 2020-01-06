---
title: 错误：无法设置数据断点 |Microsoft Docs
ms.date: 12/3/2019
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.unable_to_set_data_breakpoint
dev_langs:
- CSharp
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, data breakpoint
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: wardengnaw
ms.author: waan
manager: caslan
ms.workload:
- multiple
ms.openlocfilehash: 18fa63f2a6f4b6d789bad6f813cb3956a636a2d2
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404088"
---
# <a name="troubleshooting-data-breakpoint-errors"></a>数据断点错误疑难解答
此页面将引导您解决在使用 "当值发生更改时中断" 时出现的常见错误

## <a name="diagnosing-unable-to-set-data-breakpoint-errors"></a>诊断 "无法设置数据断点" 错误
> [!IMPORTANT]
> .NET Core 3.0 和更高的支持托管数据断点。 可在[此处](https://dotnet.microsoft.com/download)下载最新版本。

下面是使用托管数据断点时可能发生的错误列表。 它们包含有关发生错误的原因以及解决错误的可能解决方案或解决方法的其他说明。

- *"目标进程使用的 .NET 版本不支持数据断点。数据断点需要 .NET Core 3.0 + 在 x86 或 x64 上运行。 "*

    - 对托管数据断点的支持从 .NET Core 3.0 开始。 目前在3.0 的 .NET Core .NET Framework 或版本中不支持此方法。 
    
    - **解决方案**：这样做的解决方案是将项目升级到 .net Core 3.0。

- *"无法在托管堆上找到此值，因此无法对其进行跟踪。"*
    - 在堆栈上声明的变量。
        - 我们不支持为堆栈上创建的变量设置数据断点，因为此变量在函数退出后将无效。
        - **解决方法**：在使用变量的行上设置断点。

    - 不是从下拉列表中展开的变量的 "当值发生更改时中断"。
        - 调试器需要知道包含要跟踪的字段的对象。垃圾回收器可能会在堆中四处移动对象，以便调试器需要知道保存要跟踪的变量的对象。 
        - **解决**方法：如果你使用的是要在其中设置数据断点的对象中的方法，请打开一个帧并使用 `locals/autos/watch` 窗口展开对象，并为所需的字段设置数据断点。

- *"静态字段或静态属性不支持数据断点"。*
    
    - 目前不支持静态字段和属性。 如果你对此功能感兴趣，请提供[反馈](#provide-feedback)。

- *"无法跟踪结构的字段和属性。"*

    - 目前不支持结构的字段和属性。 如果你对此功能感兴趣，请提供[反馈](#provide-feedback)。

- *"属性值已更改，不能再进行跟踪。"*

    - 属性可能会更改在运行时计算它的方式，如果发生这种情况，属性所依赖的变量的数目会增加，并且可能会超出硬件限制。 请参阅下面的`"The property is dependent on more memory than can be tracked by the hardware."`。

- *"属性依赖于硬件无法跟踪的内存。"*
    
    - 每个体系结构都具有一组可以支持的字节数和硬件数据断点，并且你希望在其上设置数据断点的属性已超过该限制。 请参阅[数据断点硬件限制](#data-breakpoint-hardware-limitations)表，了解所使用的体系结构支持的硬件数据断点和字节数。 
    - **解决方法**：在属性内可能发生更改的值上设置数据断点。

- *"使用旧C#的表达式计算器时不支持数据断点"。*

    - 仅在非旧C#表达式计算器上支持数据断点。 
    - **解决方案**：通过转到 " C# `Debug -> Options`" `Debugging -> General` 取消选中 "`"Use the legacy C# and VB expression evaluators"`，禁用旧的表达式计算器。

## <a name="data-breakpoint-hardware-limitations"></a>数据断点硬件限制

你的程序在其上运行的体系结构（平台配置）的硬件数据断点数量有限。 下表列出了可用于每个体系结构的寄存器数。

| 体系结构 | 支持的硬件数据断点数 | 最大字节大小|
| :-------------: |:-------------:| :-------------:|
| x86 | 4 | 4 |
| x64 | 4 | 8 |
| ARM | 1 | 4 |
| ARM64 | 2 | 8 |

## <a name="provide-feedback"></a>提供反馈
有关此功能的任何问题或建议，请通过 "帮助" > 发送反馈 > 在 IDE 或[开发人员社区](https://developercommunity.visualstudio.com/)中[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [.Net Core 3.0 中的 "值更改时中断"](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)。
- [DevBlog：值更改时中断： Visual Studio 2019 中 .NET Core 的数据断点](https://devblogs.microsoft.com/visualstudio/break-when-value-changes-data-breakpoints-for-net-core-in-visual-studio-2019/)
