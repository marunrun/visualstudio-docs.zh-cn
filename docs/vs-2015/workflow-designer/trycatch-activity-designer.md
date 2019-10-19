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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b26bb37d1ddeabb77b1399c6cbce5ae55b59702c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654665"
---
# <a name="trycatch-activity-designer"></a>TryCatch 活动设计器
" **TryCatch** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.TryCatch> 活动。

## <a name="the-trycatch-activity"></a>TryCatch 活动
 "@No__t_0" 活动包含一个 "<xref:System.Activities.Statements.TryCatch.Try%2A>" 活动、"**捕获 > \<TException**的集合" 和 "<xref:System.Activities.Statements.TryCatch.Finally%2A>" 活动。 **TException**类型的 <xref:System.Activities.Statements.Catch%601> 包含 <xref:System.Activities.Statements.Catch%601.ExceptionType%2A> 和 <xref:System.Activities.Statements.Catch%601.Action%2A>。 将它们结合使用可实现典型的基于异常的错误处理机制。 <xref:System.Activities.Statements.TryCatch> 活动尝试执行其 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动。 如果 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动引发任何异常，则 <xref:System.Activities.Statements.TryCatch> 活动将使用其**Catch < TException \>** 集合来匹配该异常。 如果存在匹配项，则会执行相应的**Catch \<TException >** 的 <xref:System.Activities.Statements.Catch%601.Action%2A>，作为异常的错误处理逻辑。 如果 <xref:System.Activities.Statements.TryCatch.Try%2A> 节中的活动已成功完成或 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中的活动已成功完成，则 <xref:System.Activities.Statements.TryCatch> 活动执行其 <xref:System.Activities.Statements.TryCatch.Finally%2A> 活动。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][异常](https://msdn.microsoft.com/library/065205cc-52dd-4f30-9578-b17d8d113136)。

### <a name="using-the-trycatch-activity-designer"></a>使用 TryCatch 活动设计器
 " **TryCatch** " 活动设计器可在 "**工具箱**" 的 "**错误处理**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡进行访问（或者 **，从** **"视图**" 菜单，或 CTLR + ALT + X。）

 可以将 " **TryCatch** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建具有 TryCatch 的默认 <xref:System.Activities.Statements.TryCatch> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 " **TryCatch** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 其他属性必须在**TryCatch**活动设计器的图面上进行编辑。

 单击**TryCatch**设计器右上角的展开按钮，查看展开视图中的"Try **"、"catch" 和**" **Finally** " 框。 若要添加 catch，请在**TryCatch**设计器中单击 "**添加新的 catch** " 按钮。 该按钮将变为类型组合框。 选择一个异常类型，然后按 Enter 键添加该 catch。 添加**catch**后，catch 区域将展开，并且可以将活动拖放到捕获中，以定义捕获的执行逻辑。 请注意，在展开的 catch 区域右侧有一个文本框。 可以使用此文本框为异常变量命名。 异常变量仅可用于同一**捕获**中的活动。

 **TryCatch**设计器不支持编辑**捕获**。 如果要更改异常类型，则必须删除**Catch**并添加一个新的。 可以通过选择并删除捕获，或使用通过右键单击访问的上下文菜单上的 "**删除**" 菜单来删除**捕获**。

### <a name="the-trycatch-properties"></a>TryCatch 属性
 下表显示 <xref:System.Activities.Statements.TryCatch>properties，并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.TryCatch> 活动的可选友好名称。 默认值是 TryCatch。|
|<xref:System.Activities.Statements.TryCatch.Try%2A>|False|在 <xref:System.Activities.Statements.TryCatch> 执行时首先执行的活动。|
|<xref:System.Activities.Statements.TryCatch.Catches%2A>|False|@No__t_1 活动引发异常时要检查的**捕获**元素的集合。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|
|<xref:System.Activities.Statements.TryCatch.Finally%2A>|False|执行完 <xref:System.Activities.Statements.TryCatch.Try%2A> 以及 <xref:System.Activities.Statements.TryCatch.Catches%2A> 集合中的任何必要活动时要执行的活动。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|

## <a name="see-also"></a>请参阅
 [集合](../workflow-designer/collection-activity-designers.md)[再次](../workflow-designer/rethrow-activity-designer.md)[引发引发](../workflow-designer/throw-activity-designer.md)