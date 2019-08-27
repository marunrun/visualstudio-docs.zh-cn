---
title: Rethrow 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8b023a42da1c862927606c4bec0215120a5e5a11
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62937752"
---
# <a name="rethrow-activity-designer"></a>Rethrow 活动设计器
**重新引发**活动设计器用于创建和配置<xref:System.Activities.Statements.Rethrow>活动。  
  
## <a name="the-rethrow-activity"></a>Rethrow 活动  
 <xref:System.Activities.Statements.Rethrow> 活动引发先前已引发的异常。 此活动只能在 <xref:System.Activities.Statements.Catch> 活动的 <xref:System.Activities.Statements.TryCatch> 处理程序中使用。  
  
### <a name="using-the-rethrow-activity-designer"></a>使用 ReThrow 活动设计器  
 **重新引发**活动设计器可在**错误处理**的类别**工具箱**，这通过单击访问**工具箱**选项卡上的左侧和右侧[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **重新引发**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.Rethrow>默认值的活动**DisplayName**的 Throw。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**重新引发**活动设计器中或在**DisplayName**属性网格的框。  
  
### <a name="the-rethrow-properties"></a>Rethrow 属性  
 下表列出 <xref:System.Activities.Statements.Rethrow> 属性并说明如何在设计器中使用它们。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Rethrow> 活动的可选友好名称。 默认值为 Rethrow。|  
  
## <a name="see-also"></a>请参阅  
 [集合](../workflow-designer/collection-activity-designers.md)   
 [引发](../workflow-designer/throw-activity-designer.md)   
 [TryCatch](../workflow-designer/trycatch-activity-designer.md)