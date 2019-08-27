---
title: 如何：指定其他检测选项 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.advanced
helpviewer_keywords:
- instrumentation, options
- profiling tools, session options
- performance sessions, options
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c95add435824663e798d226e0be11ddbe06b8aba
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62539135"
---
# <a name="how-to-specify-additional-instrumentation-options"></a>如何：指定其他检测选项

还可以通过使用 Visual Studio IDE 或使用命令行工具来检测二进制文件。 如果从 IDE 内检测二进制文件，可以在检测期间通过向 [VSInstr](../profiling/vsinstr.md) 工具指定其他检测选项，控制收集的数据量。 这些选项在会话级别或目标级别可用。 例如，若要在检测过程中包括或排除特定函数，请在目标级别使用其他检测选项。

> [!IMPORTANT]
> 每个插入的探测都将稍微修改原始程序的行为。 此修改将导致分析时产生系统开销。 即使减去此系统开销的近似值，它仍然对多线程应用程序有细微计时影响。 [VSInstr](../profiling/vsinstr.md) 工具选项在分析期间帮助控制数据收集。

## <a name="to-specify-additional-instrumentation-option"></a>指定其他检测选项

1. 在“性能资源管理器”中，选择“性能会话”，然后右键单击并选择“属性”。

2. 在“属性页”中，单击“高级”属性。

3. 在“其他检测选项”框中键入选项。

     例如，使用 /CONTROL:THREAD 指定分析级别。 有关选项的完整列表，请参阅 [VSInstr](../profiling/vsinstr.md)。

4. 单击 **“确定”**。

## <a name="see-also"></a>请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
[来自命令行的配置文件](../profiling/using-the-profiling-tools-from-the-command-line.md)