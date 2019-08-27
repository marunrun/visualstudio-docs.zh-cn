---
title: DA0030：收集数据库项目的层交互度量值 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0030
- vs.performance.rules.DA0030
- vs.performance.30
ms.assetid: 42b2f69d-0cfa-4854-82c4-589c3d8b4557
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9a4b140c1859d3a3a17eb2f48eb02a60a3e9d50c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152631"
---
# <a name="da0030-gather-tier-interaction-measurements-for-database-projects"></a>DA0030：收集数据库项目的层交互度量值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

规则 Id |DA0030 |  
|类别 |分析工具使用情况 |  
|分析方法 |采样 |  
|消息 |收集多层应用程序的交互度量值将有助于您了解数据库使用模式和关键数据访问延迟。 尝试在启用“层交互分析”选项的情况下再次分析应用程序。|  
|规则类型 |信息 |  
  
## <a name="cause"></a>原因  
 对 <xref:System.Data> 方法的调用在分析数据中占很大比例，并且用户未收集分析运行中的层交互数据。 请考虑再次进行分析并添加层交互数据。  
  
## <a name="rule-description"></a>规则说明  
 每当位于 System.Data 命名空间（包括 <xref:System.Data.Linq><xref:System.Data.Linq>）中的函数中出现重大活动时，都将触发此规则。  
  
 多层应用程序将分层的服务用于其演示文稿和数据层。 通常，数据层是运行数据库管理系统（如 Microsoft Sql Server）的单独进程。 数据层甚至可能通过应用程序其余部分在单独的计算机上运行。 采样分析很少涉及在进程外运行或远程运行的函数和服务。  
  
 分析工具可收集多层应用程序的计时信，这些应用程序通过对 ADO.NET 服务的异步调用与 Microsoft Sql Server 数据层交互。 必须显式启用层交互分析。 它不是默认打开的。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 此规则仅供参考，可能不需要采取纠正措施。  
  
 有关如何从 Visual Studio IDE 向分析数据添加层交互数据的信息，请参阅[收集层交互数据](../profiling/collecting-tier-interaction-data.md)。 有关如何从命令行添加层交互数据的信息，请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)。
