---
title: 如何：收集 Windows 事件跟踪 (ETW) 数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.events
helpviewer_keywords:
- event trace providers, performance tools
- profiling tools, event trace providers
- performance tools, enabling event trace providers
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2fa0547682351d1a7ba4efe4ce3b4350b906462c
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779020"
---
# <a name="how-to-collect-event-tracing-for-windows-etw-data"></a>如何：收集 Windows 事件跟踪 (ETW) 数据

Windows 事件跟踪 (ETW) 是有效的内核级别跟踪工具，该工具可启用探查器日志内核或应用程序定义的事件。 从事件提供程序收集的数据只能使用 [VSPerfReport](../profiling/vsperfreport.md) 命令行工具的 /**Summary:ETW** 选项进行查看。 此报表可用于确定应用程序中出现性能问题的位置。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="to-enable-event-trace-providers"></a>启用事件跟踪提供程序

1. 在“性能资源管理器”  中，右键单击性能会话，然后单击“属性”  。

2. 在“属性页”  中，单击“Windows 事件”  属性。

3. 在“选择从中收集数据的事件跟踪提供程序”  列表中，选择要用来分析应用程序的事件提供程序。

## <a name="see-also"></a>请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
