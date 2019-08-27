---
title: “摘要”视图 - 资源争用视图 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Summary view
ms.assetid: 6da57b83-7b42-4d7c-9aea-8e0a830faf6b
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 65f659b64b6a1e29e1e25ae344dd8033e631de09
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157759"
---
# <a name="summary-view---resource-contention-view"></a>“摘要”视图 - 资源争用视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“摘要”视图显示有关应用程序中线程或进程在其中挂起、同时等待访问资源的事件的信息。  
  
 有关详细信息（包括通知链接和报告列表的说明），请参阅[“摘要”视图](../profiling/summary-view.md)。  
  
## <a name="timeline-graph"></a>时间线关系图  
 “摘要”视图中的时间线关系图显示在进行分析的时间内分析的应用程序的争用事件数。 可以使用时间线关系图将视图筛选到所选时间范围。 有关详细信息，请参阅[如何：从摘要时间线中筛选报表视图](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)。  
  
## <a name="most-contended-resources"></a>争用最激烈的资源  
 “争用最激烈的资源”  列出应用程序中导致最多争用事件的资源。 可以单击某个资源名以显示“争用”视图。 “争用”视图按线程提供资源争用的详细时间线。  
  
 “争用最激烈的资源”  包括每个资源的以下数据。  
  
|列|描述|  
|------------|-----------------|  
|**名称**|资源的名称。|  
|**争用数百分比**|属于针对此资源的争用的争用事件占分析数据中的所有争用事件的百分比。|  
  
## <a name="most-contended-thread"></a>争用最激烈的线程  
 “争用最激烈的线程”  列出应用程序中具有最大争用事件数的线程。 可以单击某个线程名以显示“争用”视图，该视图按线程提供资源争用的详细时间线。  
  
 “争用最激烈的线程”  包括每个线程的以下数据。  
  
|列|描述|  
|------------|-----------------|  
|**ID**|线程标识符。|  
|**名称**|拥有此线程的进程的名称。|  
|**争用数百分比**|属于针对此资源的争用的争用事件占分析数据中的所有争用事件的百分比。|
