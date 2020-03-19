---
title: 如何：开始和结束性能数据收集 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.summarypage
helpviewer_keywords:
- profiling tools, launching sessions
- performance sessions, launching
- performance sessions, ending
- profiling tools, ending sessions
ms.assetid: 9f6eb0d5-d9e9-4bec-b627-445065610bce
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: da75306018cf19855c7cb7f74ac3ffc4e84bcd9a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74774506"
---
# <a name="how-to-start-and-end-performance-data-collection"></a>如何：启动和停止性能数据收集
启动分析之前，必须将要分析的目标二进制文件添加到性能会话中。 若要添加目标，请在“性能资源管理器”中右键单击“目标”，然后单击“添加目标二进制文件”    。 在“添加目标二进制文件”对话框中，选择文件名，然后单击“打开”   。 将添加一个新的二进制文件。

### <a name="to-start-profiling"></a>启动分析

1. 在“性能资源管理器”窗口中右键单击性能会话的名称，然后选择以下选项之一  ：

    - **启动并启用分析功能** — 启动应用程序并立即开始分析。

    - **启动并暂停分析** — 启动应用程序，但不开始分析。 可以通过在“数据收集控制”窗口中选择“恢复收集”来启动分析   。 有关详细信息，请参阅[如何：暂停和恢复性能数据收集](../profiling/how-to-pause-and-resume-performance-data-collection.md)。

### <a name="to-end-profiling"></a>结束分析

- 结束分析会话的首选方法是退出应用程序。 若要立即停止分析，请在“性能资源管理器”工具栏上单击“停止”   。

## <a name="see-also"></a>另请参阅
- [控制数据收集](../profiling/controlling-data-collection.md)
- [如何：暂停和恢复性能数据收集](../profiling/how-to-pause-and-resume-performance-data-collection.md)
