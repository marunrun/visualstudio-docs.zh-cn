---
title: Throw 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Throw.UI
ms.assetid: 5e97c947-be39-4a1f-af04-000e2e09528a
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: db909618971eeab2d92506d1c29b06290aa9263b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976620"
---
# <a name="throw-activity-designer"></a>Throw 活动设计器
**引发**活动设计器用于创建和配置<xref:System.Activities.Statements.Throw>活动。  
  
## <a name="the-throw-activity"></a>Throw 活动  
 <xref:System.Activities.Statements.Throw> 活动会引发一个异常。  
  
### <a name="using-the-throw-activity-designer"></a>使用 Throw 活动设计器  
 **引发**活动设计器可在**错误处理**的类别**工具箱**，这通过单击来访问**工具箱**选项卡上的左侧和右侧[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **引发**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.Throw>默认值的活动**DisplayName**的 Throw。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**引发**活动设计器中或在**DisplayName**属性网格的框。 <xref:System.Activities.Statements.Throw.Exception%2A> 属性必须在属性网格上编辑。  
  
### <a name="the-throw-properties"></a>Throw 属性  
 下表列出 <xref:System.Activities.Statements.Throw> 属性并说明如何在设计器中使用它们。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Throw> 活动的可选友好名称。 默认值为 Throw。|  
|<xref:System.Activities.Statements.Throw.Exception%2A>|True|要引发的异常。 此异常必须派生自 <xref:System.Exception>。 若要指定此异常，请在属性网格中键入 Visual Basic 表达式。|  
  
## <a name="see-also"></a>请参阅  
 [集合](../workflow-designer/collection-activity-designers.md)   
 [重新引发](../workflow-designer/rethrow-activity-designer.md)   
 [Throw 活动设计器](../workflow-designer/throw-activity-designer.md)   
 [TryCatch](../workflow-designer/trycatch-activity-designer.md)