---
title: 如何：从命令提示符下创建探查器比较报告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 00548d16-eb5b-46f7-8a65-862f98a43831
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8c6dabbae5f2d3758aebe0562f99767ee6993d80
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179568"
---
# <a name="how-to-create-a-profiler-comparison-report-from-a-command-prompt"></a>如何：从命令提示符下创建探查器比较报告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以生成 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具报告，用于比较两个分析数据（.VSP 或 .VSPS）文件的性能数据。 报告显示从一个分析会话到另一个分析会话所发生的差异、性能回归和改进。 报告中的值表示基于指定的首个文件的基线的增量（或变化）。 此增量是通过确定旧值（基准值）与新分析所得结果值之差计算而得。 探查器数据的比较可基于代码中的函数、应用程序中的模块、行、指令指针 (IP) 和类型。  
  
 若要列出比较类别和字段的标识符，请键入以下命令行：  
  
 **VSPerfReport /querydifftables**  *VspFileName1* *VspFileName2*  
  
 使用以下语法创建比较报告：  
  
 **VSPerfReport /diff**  `VspFileName1` *VspFileName2* [ **/** `Options`]  
  
 可以向 VSPerfReport /diff 命令行添加下表中的选项。  
  
|选项|描述|  
|------------|-----------------|  
|DiffThreshold:[Value]|如果差异低于此百分比阀值，则忽略该差异。 此外，不会显示值低于此阈值的新数据。|  
|**DiffTable：** *TableName*|使用此表比较文件。 默认使用函数表。 指定 VSPerfReport /querydifftables 中列出的标识符。|  
|**DiffColumn：** *ColumnName*|使用此列对值进行比较。 默认情况下，使用独占样本百分比列。 指定 VSPerfReport /querydifftables 中列出的标识符。|
