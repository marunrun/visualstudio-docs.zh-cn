---
title: “性能资源管理器”窗口 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performanceexplorer
- vs.performance.explorer
helpviewer_keywords:
- performance tools, Performance Explorer
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: a365892f606da90c608e43b7ccce73b902ec0e98
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74772434"
---
# <a name="performance-explorer-window"></a>“性能资源管理器”窗口

通过 Visual Studio IDE 中的“性能资源管理器”  窗口，可以使用 Visual Studio 分析工具来配置和启动性能会话。 如果需要打开该窗口，请遵循[性能分析初学者指南](../profiling/beginners-guide-to-cpu-sampling.md)中的说明。

## <a name="performance-explorer-toolbar"></a>“性能资源管理器”工具栏

“性能资源管理器”  工具栏上提供了以下选项：

- **启动性能向导** - 显示性能向导，用于将新性能会话添加到“性能资源管理器”窗口。

- **新建性能会话** - 将空的性能会话添加到“性能资源管理器”窗口。

- **启动** -“启动”  命令按钮列表可用于启动立即启用分析（“启动并启用分析功能”  ）或挂起分析（“启动并暂停分析”  ）的目标应用程序。

- **方法** - 指定会话的分析方法是采样还是检测。

- **停止** - 立即退出目标应用程序和探查器。

- **附加/分离**- 显示“将探查器附加到进程”  对话框以选择要将探查器附加到的正在运行的进程。

## <a name="performance-explorer-window"></a>“性能资源管理器”窗口

“性能资源管理器”  窗口包含一个树控件，它显示一个或多个性能会话的二进制文件和报告数据文件。

- **会话名称** - 树控件的根包含会话的名称。 右键单击会话名称可设置会话属性或启动目标应用程序和探查器。

- **目标** - 显示要在会话中进行探查的二进制文件的名称。 右键单击“目标”  可添加或删除二进制文件、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目或网站。 右键单击目标名称可为单个二进制文件设置属性。

- **报告** - 显示为会话生成的探查器数据文件的名称。 右键单击“报告”  可添加现有报告或比较两个探查器数据文件。 右键单击报告名称可打开、删除或导出探查器数据文件。

## <a name="see-also"></a>另请参阅

[概述](../profiling/overviews-performance-tools.md)
[配置性能会话](../profiling/configuring-performance-sessions.md)
[控制数据收集](../profiling/controlling-data-collection.md)
