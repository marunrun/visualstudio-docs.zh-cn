---
title: 错误 - 无法设置数据断点 | Microsoft Docs
ms.date: 12/3/2019
ms.topic: error-reference
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
ms.openlocfilehash: dab5e146d510601c6e93582b6b128abcd964b4a7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85459930"
---
# <a name="troubleshooting-data-breakpoint-errors"></a>数据断点错误疑难解答
此页面将引导你解决在使用“值发生更改时中断”时出现的常见错误

## <a name="diagnosing-unable-to-set-data-breakpoint-errors"></a>诊断“无法设置数据断点”错误
> [!IMPORTANT]
> .NET Core 3.0 和更高版本中支持托管数据断点。 可以在[此处](https://dotnet.microsoft.com/download)下载最新版本。

下面是使用托管数据断点时可能发生的错误的列表。 它们包含有关发生错误的原因以及解决错误的可能解决方案或解决方法的其他说明。

- “目标进程使用的 .NET 版本不支持数据断点。数据断点需要在 x86 或 x64 上运行的 .NET Core 3.0 及更高版本。”

    - 从 .NET Core 3.0 开始支持托管数据断点。 在 .NET Framework 以及低于 3.0 的 .NET Core 版本中，当前不支持该功能。 
    
    - **解决方案**；此错误的解决方案是将项目升级到 .NET Core 3.0。

- “托管堆上找不到此值，无法对其进行跟踪。”
    - 变量在堆栈上声明。
        - 我们不支持为堆栈上创建的变量设置数据断点，因为此变量在函数退出后将无效。
        - **解决方法**：在使用变量的行上设置断点。

    - 对变量使用“值发生更改时中断”（不是从下拉菜单展开）。
        - 调试器在内部需要知道包含要跟踪的字段的对象。垃圾回收器可能会在堆中四处移动对象，因此调试器需要知道保存要跟踪的变量的对象。 
        - **解决方法**：如果处于要对其设置数据断点的对象中的方法中，请向上移动一帧并使用 `locals/autos/watch` 窗口展开对象，然后为所需字段设置数据断点。

- “静态字段或静态属性不支持数据断点。”
    
    - 目前不支持静态字段和属性。 如果对此功能感兴趣，请提供[反馈](#provide-feedback)。

- “无法跟踪结构的字段和属性。”

    - 目前不支持结构的字段和属性。 如果对此功能感兴趣，请提供[反馈](#provide-feedback)。

- “属性值已更改，无法再进行跟踪。”

    - 属性可能会更改它在运行时的计算方式，如果发生这种情况，则属性所依赖的变量数会增加，并且可能会超出硬件限制。 请参阅下面的 `"The property is dependent on more memory than can be tracked by the hardware."`。

- “此属性依赖的内存比硬件可跟踪的内存要多。”
    
    - 每个体系结构都具有一定数量的可以支持的字节和硬件数据断点，你希望对其设置数据断点的属性已超过该限制。 请参阅[数据断点硬件限制](#data-breakpoint-hardware-limitations)表，以了解有多少硬件支持的数据断点和字节可用于所使用的体系结构。 
    - **解决方法**：在属性中对可能发生更改的值设置数据断点。

- “使用旧版 C# 表达式计算器时，不支持数据断点。”

    - 仅在非旧版 C# 表达式计算器上才支持数据断点。 
    - **解决方案**；通过转到 `Debug -> Options`，然后在 `Debugging -> General` 下取消选中 `"Use the legacy C# and VB expression evaluators"`，来禁用旧版 C# 表达式计算器。

## <a name="data-breakpoint-hardware-limitations"></a>数据断点硬件限制

用于运行程序的体系结构（平台配置）可使用的硬件数据断点数量有限。 下表指出每个体系结构可使用的寄存器数。

| 体系结构 | 硬件支持的数据断点数 | 最大字节大小|
| :-------------: |:-------------:| :-------------:|
| x86 | 4 | 4 |
| X64 | 4 | 8 |
| ARM | 1 | 4 |
| ARM64 | 2 | 8 |

## <a name="provide-feedback"></a>提供反馈
有关此功能的任何问题或建议，请通过 IDE 中的“帮助”>“发送反馈”>[“报告问题”](../ide/how-to-report-a-problem-with-visual-studio.md)或是在[开发人员社区](https://developercommunity.visualstudio.com/)中告知我们。

## <a name="see-also"></a>请参阅
- [在 .NET Core 3.0 中使用“值发生更改时中断”](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)。
- [DevBlog：值发生更改时中断：Visual Studio 2019 中用于 .NET Core 的数据断点](https://devblogs.microsoft.com/visualstudio/break-when-value-changes-data-breakpoints-for-net-core-in-visual-studio-2019/)
