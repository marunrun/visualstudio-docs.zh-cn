---
title: “层交互”视图 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.tierinteraction
helpviewer_keywords:
- Tier Interactions view
ms.assetid: bb4fb21c-f3f7-473a-8b5e-442da4c2c445
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bd60c855bacaf62beec47c9f977d0ab220ce7ca6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145522"
---
# <a name="tier-interactions-view"></a>“层交互”视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

层交互分析提供有关多层应用程序函数执行时间的附加信息，这些应用程序通过 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 服务与数据库进行通信。 仅针对同步函数调用收集数据。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]  
  
  “交互”视图在两个窗格中显示层交互数据：  
  
- 主窗格是层次结构树。 顶层行包含 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 页面或进程的数据库连接的聚合数据。 子节点包含父级的数据库连接的聚合数据。  
  
- 在主窗格中单击某个数据库调用节点时，该数据库调用的实例的数据会显示在详细信息窗格中。  
  
  时间显示为毫秒数或 CPU 时钟计时周期数。 若要更改显示的时间单位，请单击“工具”  菜单，单击“选项”  ，然后选择“将时间值显示为”  选项中的一个。  
  
## <a name="master-pane"></a>主窗格  
  
|列|描述|  
|------------|-----------------|  
|**名称**|-   对于顶层行，是分析的进程或网页的名称。<br />-   对于数据库连接行，是承载数据库的服务器的名称。|  
|**数据库**|数据库的名称（仅限数据库连接行）。|  
|**计数**|进程、网页或数据库连接生成的请求的总数。|  
|**总运行时间**|执行来自进程、网页或数据库连接的任何一个请求所用的总时间。|  
|**最大运行时间**|执行来自进程、网页或数据库连接的任何一个请求所用的最大时间。|  
|**最小运行时间**|执行来自进程、网页或数据库连接的任何一个请求所用的最小时间。|  
|**平均运行时间**|执行来自进程、网页或数据库连接的请求所用的平均时间。|  
  
## <a name="database-connection-details-pane"></a>“数据库连接详细信息”窗格  
  
|列|描述|  
|------------|-----------------|  
|**命令文本**|请求的 SQL 查询。|  
|**查询计数**|运行查询的次数。|  
|**总运行时间**|执行查询的实例所用的总时间。|  
|**最大运行时间**|执行查询的实例所用的最大时间。|  
|**最小运行时间**|执行查询的实例所用的最小时间。|  
|**平均运行时间**|执行查询的实例所用的平均时间。|
