---
title: 工作流设计器-TryCatch 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TryCatch.UI
- System.Activities.Statements.Catch`1.UI
ms.assetid: 02a326c2-4009-442f-b7cb-e42121fd2992
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 079c25b2bbaa37432009f0eeade9673f8d0afd28
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62433946"
---
# <a name="trycatch-activity-designer"></a>TryCatch 活动设计器

**TryCatch**活动设计器用于创建和配置<xref:System.Activities.Statements.TryCatch>活动。

## <a name="the-trycatch-activity"></a>TryCatch 活动
 <xref:System.Activities.Statements.TryCatch>活动包含<xref:System.Activities.Statements.TryCatch.Try%2A>活动、 一系列**捕获\<TException >** 和<xref:System.Activities.Statements.TryCatch.Finally%2A>活动。 一个<xref:System.Activities.Statements.Catch%601>类型的**TException**包含<xref:System.Activities.Statements.Catch%601.ExceptionType%2A>和<xref:System.Activities.Statements.Catch%601.Action%2A>。 将它们结合使用可实现典型的基于异常的错误处理机制。 <xref:System.Activities.Statements.TryCatch> 活动尝试执行其 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动。 如果<xref:System.Activities.Statements.TryCatch.Try%2A>活动会引发任何异常<xref:System.Activities.Statements.TryCatch>活动使用其**捕获 < TException\>** 集合来匹配该异常。 如果没有匹配项，则<xref:System.Activities.Statements.Catch%601.Action%2A>的相应**捕获\<TException >** 作为错误处理异常的逻辑的执行。 如果 <xref:System.Activities.Statements.TryCatch.Try%2A> 节中的活动已成功完成或 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中的活动已成功完成，则 <xref:System.Activities.Statements.TryCatch> 活动执行其 <xref:System.Activities.Statements.TryCatch.Finally%2A> 活动。 有关详细信息，请参阅[Windows 工作流异常](/dotnet/framework/windows-workflow-foundation/exceptions)。

### <a name="using-the-trycatch-activity-designer"></a>使用 TryCatch 活动设计器

访问**TryCatch**中的活动设计器**错误处理**类别**工具箱**。

**TryCatch**活动设计器可以从拖动**工具箱**只要通常放置活动的例如内放置到工作流设计器图面和<xref:System.Activities.Statements.Sequence>。 这将创建具有 TryCatch 的默认 <xref:System.Activities.Statements.TryCatch> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**TryCatch**活动设计器中或在**DisplayName**属性网格的框。 其他属性必须编辑上的图面**TryCatch**活动设计器。

单击右上角的展开按钮**TryCatch**设计器才能看到**尝试**，**捕获**，以及**最后**中展开的视图。 若要添加 catch，请单击**添加新捕获**按钮**TryCatch**设计器。 该按钮将变为类型组合框。 选择一个异常类型，然后按 Enter 键添加该 catch。 添加后**捕获**，catch 区域将展开，活动可以放入以定义该 catch 的执行逻辑。 请注意，在展开的 catch 区域右侧有一个文本框。 可以使用此文本框为异常变量命名。 异常变量仅可用于在同一活动**捕获**。

**TryCatch**设计器不支持编辑**捕获**。 如果你想要更改的异常类型，则必须删除**捕获**并添加新帐户。 一个**捕获**可以通过选择它并将它删除或选择删除**删除**访问通过右键单击上下文菜单上。

### <a name="the-trycatch-properties"></a>TryCatch 属性

下表显示<xref:System.Activities.Statements.TryCatch>属性并说明如何在设计器中使用。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.TryCatch> 活动的可选友好名称。 默认值是 TryCatch。|
|<xref:System.Activities.Statements.TryCatch.Try%2A>|False|在 <xref:System.Activities.Statements.TryCatch> 执行时首先执行的活动。|
|<xref:System.Activities.Statements.TryCatch.Catches%2A>|False|集合**捕获**元素时要检查<xref:System.Activities.Statements.TryCatch.Try%2A>活动会引发异常。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|
|<xref:System.Activities.Statements.TryCatch.Finally%2A>|False|执行完 <xref:System.Activities.Statements.TryCatch.Try%2A> 以及 <xref:System.Activities.Statements.TryCatch.Catches%2A> 集合中的任何必要活动时要执行的活动。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|

## <a name="see-also"></a>请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [Rethrow](../workflow-designer/rethrow-activity-designer.md)
- [Throw](../workflow-designer/throw-activity-designer.md)