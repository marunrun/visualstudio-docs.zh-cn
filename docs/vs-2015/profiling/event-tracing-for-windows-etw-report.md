---
title: Windows 事件跟踪 (ETW) 报告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Event tracing for Windows profiling report
- ETW profiling report
ms.assetid: 81e88162-b88a-40b6-8b85-a232c8096a47
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bc0e139644a0b3df29109c1543140e57c5378f31
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444008"
---
# <a name="event-tracing-for-windows-etw-report"></a>Windows 事件跟踪 (ETW) 报告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows 事件跟踪 (ETW) 报告列出 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具的性能会话中所录制的 ETW 事件。 在二进制 (.etl) 文件中收集 ETW 数据。  
  
> [!NOTE]
> 不能在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 接口中显示 ETW 报告。  
  
- 要了解如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 接口中的分析工具收集 ETW，请参阅[如何：Windows (ETW) 数据收集事件跟踪](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)。  
  
- 有关如何使用 [VSPerfCmd](../profiling/vsperfcmd.md) 命令行工具收集 ETW 数据的信息，请参阅[事件](../profiling/events-vsperfcmd.md)。  
  
- 使用 VSReport/Summary:ETW 命令生成 ETW 报告。 有关详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。  
  
|列|描述|  
|------------|-----------------|  
|**时间戳**|标识事件发生的时间。|  
|**进程 ID**|标识生成事件的进程。|  
|**线程 ID**|标识生成事件的线程。|  
|**说明**|标识事件提供程序。|  
|**Type**|标识事件类型。|  
|**属性**|事件的属性。 每个事件都是一个括在括号内的以逗号分隔的名称/值对。|
