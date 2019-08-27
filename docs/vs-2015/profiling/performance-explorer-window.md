---
title: “性能资源管理器”窗口 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performanceexplorer
- vs.performance.explorer
helpviewer_keywords:
- performance tools, Performance Explorer
ms.assetid: cb6a6efc-93a5-49a2-8d03-6969b5f3b6d7
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a370ae802408ecc821de4cd15824f9d1fca42b75
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195524"
---
# <a name="performance-explorer-window"></a>“性能资源管理器”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 集成开发环境 (IDE) 中的“性能资源管理器”  窗口，您可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具来配置和启动性能会话。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
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
  
- **目标** - 显示要在会话中进行探查的二进制文件的名称。 右键单击“目标”  可添加或删除二进制文件、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目或网站。 右键单击目标名称可为单个二进制文件设置属性。  
  
- **报告** - 显示为会话生成的探查器数据文件的名称。 右键单击“报告”  可添加现有报告或比较两个探查器数据文件。 右键单击报告名称可打开、删除或导出探查器数据文件。  
  
## <a name="see-also"></a>另请参阅  
 [概述](../profiling/overviews-performance-tools.md)   
 [配置性能会话](../profiling/configuring-performance-sessions.md)   
 [控制数据收集](../profiling/controlling-data-collection.md)
