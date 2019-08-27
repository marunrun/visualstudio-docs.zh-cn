---
title: 工作流设计器-Persist 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c97d916d00d1c976b4e27381f55e42cbb7cb0db
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004119"
---
# <a name="persist-activity-designer"></a>Persist 活动设计器

**Persist**活动设计器用于创建和配置<xref:System.Activities.Statements.Persist>活动。

## <a name="the-persist-activity"></a>Persist 活动

<xref:System.Activities.Statements.Persist> 活动用于将工作流保存到磁盘中（如有可能）。 <xref:System.Activities.Statements.Persist> 活动无法在非持久性区域中执行，例如，在 <xref:System.Activities.Statements.TransactionScope> 活动中。 如果在非持久性作用域中使用 <xref:System.Activities.Statements.Persist> 活动，则在运行时会引发异常。

### <a name="using-the-persist-activity-designer"></a>使用 Persist 活动设计器

**Persist**活动设计器可在**运行时**类别**工具箱**，这通过单击来访问**工具箱**选项卡 (或者，选择**工具箱**从**视图**菜单或 CTRL + ALT + X。)

**Persist**活动设计器可以从拖动**工具箱**只要通常放置活动的例如内放置到工作流设计器图面和<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.Persist>默认值的活动**DisplayName**的保留。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**Persist**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-persist-properties"></a>Persist 属性

下表列出 <xref:System.Activities.Statements.Persist> 属性并说明如何在设计器中使用它们。 可以在属性网格中编辑这些属性，其中一些可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Persist> 活动的友好名称。 默认值为 Persist。 虽然显示名称不是绝对必需的，但最好使用显示名称。|

## <a name="see-also"></a>请参阅

- [运行时](../workflow-designer/runtime-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)