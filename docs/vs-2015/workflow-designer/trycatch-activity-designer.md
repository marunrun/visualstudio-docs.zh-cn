---
title: TryCatch 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TryCatch.UI
- System.Activities.Statements.Catch`1.UI
ms.assetid: 02a326c2-4009-442f-b7cb-e42121fd2992
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fb155cc7bbf4efbda54666f91f2db3f92e6c378c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697078"
---
# <a name="trycatch-activity-designer"></a>TryCatch 活动设计器
**TryCatch**活动设计器用于创建和配置<xref:System.Activities.Statements.TryCatch>活动。  
  
## <a name="the-trycatch-activity"></a>TryCatch 活动  
 <xref:System.Activities.Statements.TryCatch>活动包含<xref:System.Activities.Statements.TryCatch.Try%2A>活动、 一系列**捕获\<TException >** 和<xref:System.Activities.Statements.TryCatch.Finally%2A>活动。 一个<xref:System.Activities.Statements.Catch%601>类型的**TException**包含<xref:System.Activities.Statements.Catch%601.ExceptionType%2A>和<xref:System.Activities.Statements.Catch%601.Action%2A>。 将它们结合使用可实现典型的基于异常的错误处理机制。 <xref:System.Activities.Statements.TryCatch> 活动尝试执行其 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动。 如果<xref:System.Activities.Statements.TryCatch.Try%2A>活动会引发任何异常<xref:System.Activities.Statements.TryCatch>活动使用其**捕获 < TException\>** 集合来匹配该异常。 如果没有匹配项，则<xref:System.Activities.Statements.Catch%601.Action%2A>的相应**捕获\<TException >** 作为错误处理异常的逻辑的执行。 如果 <xref:System.Activities.Statements.TryCatch.Try%2A> 节中的活动已成功完成或 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中的活动已成功完成，则 <xref:System.Activities.Statements.TryCatch> 活动执行其 <xref:System.Activities.Statements.TryCatch.Finally%2A> 活动。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][异常](https://msdn.microsoft.com/library/065205cc-52dd-4f30-9578-b17d8d113136)。  
  
### <a name="using-the-trycatch-activity-designer"></a>使用 TryCatch 活动设计器  
 **TryCatch**活动设计器可在**错误处理**类别**工具箱**，这通过单击来访问**工具箱**选项卡的左侧[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单中或 CTLR + ALT + X。)  
  
 **TryCatch**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建具有 TryCatch 的默认 <xref:System.Activities.Statements.TryCatch> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**TryCatch**活动设计器中或在**DisplayName**属性网格的框。 其他属性必须编辑上的图面**TryCatch**活动设计器。  
  
 单击右上角的展开按钮**TryCatch**设计器才能看到**尝试**，**捕获**，以及**最后**中展开的视图。 若要添加 catch，请单击**添加新捕获**按钮**TryCatch**设计器。 该按钮将变为类型组合框。 选择一个异常类型，然后按 Enter 键添加该 catch。 添加后**捕获**，catch 区域将展开，活动可以放入以定义该 catch 的执行逻辑。 请注意，在展开的 catch 区域右侧有一个文本框。 可以使用此文本框为异常变量命名。 异常变量仅可用于在同一活动**捕获**。  
  
 **TryCatch**设计器不支持编辑**捕获**。 如果你想要更改的异常类型，则必须删除**捕获**并添加新帐户。 一个**捕获**可以通过选中它然后删除它或使用删除**删除**通过右键单击上下文菜单上的菜单。  
  
### <a name="the-trycatch-properties"></a>TryCatch 属性  
 下表显示<xref:System.Activities.Statements.TryCatch>属性并说明如何在设计器中使用。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.TryCatch> 活动的可选友好名称。 默认值是 TryCatch。|  
|<xref:System.Activities.Statements.TryCatch.Try%2A>|False|在 <xref:System.Activities.Statements.TryCatch> 执行时首先执行的活动。|  
|<xref:System.Activities.Statements.TryCatch.Catches%2A>|False|集合**捕获**元素时要检查<xref:System.Activities.Statements.TryCatch.Try%2A>活动会引发异常。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|  
|<xref:System.Activities.Statements.TryCatch.Finally%2A>|False|执行完 <xref:System.Activities.Statements.TryCatch.Try%2A> 以及 <xref:System.Activities.Statements.TryCatch.Catches%2A> 集合中的任何必要活动时要执行的活动。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|  
  
## <a name="see-also"></a>请参阅  
 [集合](../workflow-designer/collection-activity-designers.md)   
 [重新引发](../workflow-designer/rethrow-activity-designer.md)   
 [Throw](../workflow-designer/throw-activity-designer.md)