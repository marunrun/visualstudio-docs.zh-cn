---
title: 工作流设计器-如何：使用痕迹导航
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4a688056-37dc-406a-9071-be2141e192fe
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: de1004dd7a62fe4163147db4928783dd9a0dca98
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949495"
---
# <a name="how-to-use-breadcrumb-navigation"></a>如何：使用痕迹导航

有三种主要方式，若要更改的工作流设计器中显示的活动集：

1. 双击以钻入子活动。

2. 单击痕迹栏上的按钮以导航到祖先活动。

3. 就地展开或折叠活动。

## <a name="using-breadcrumb-navigation"></a>使用痕迹导航

1. 双击工作流设计器的根活动改为单击的活动的活动。 单击的活动已完全扩展根目录和其祖先将显示在痕迹导航栏中。 这有时称为钻入或钻出某个活动。

2. 若要导航到当前根活动的一个祖先，请单击痕迹栏中的相应活动。

## <a name="expanding-or-collapsing-an-activity-in-place"></a>就地展开或折叠活动

1. 单击活动上的 V 形将就地展开或折叠该活动。

2. 单击该按钮更改展开状态时，新的展开状态将保存在 XAML 中。

    > [!WARNING]
    > 并非所有活动都可就地展开。 在两种情况下不能就地展开活动：一种是活动的父级不允许其子级就地展开（例如，流程图中的活动不能就地展开），另一种是活动设计器不允许自身就地展开。 尽管所有工作流设计器中包含的活动设计器都没有后一种行为，但某些自定义活动可能会出现此行为。

## <a name="expanding-all-or-collapsing-all-activities"></a>展开或折叠所有活动

1. 使用**全部展开**并**折叠所有**要展开或折叠所有当前痕迹根下的活动的用户界面中的按钮。 请注意，全部展开和全部折叠是全局状态。 这意味着使用痕迹导航栏中，展开所有该根活动进行更改或全部折叠状态时仍然存在，您必须单击**还原**。

2. 已应用全部展开或折叠所有状态后，可以单击**还原**按钮，它可返回到查看以前应用于每个活动的状态。

    > [!WARNING]
    > 如果某个活动，如<xref:System.Activities.Statements.Flowchart>，已选择加入共就地展开，相关联的功能**全部展开**并**全部折叠**上禁用按钮**流程图**设计器。 有关详细信息**流程图**设计器，请参见[流程图](../workflow-designer/flowchart-activity-designer.md)主题。

    > [!WARNING]
    > 全部展开中也有特殊效果**交换机**并**TryCatch**活动设计器。 当您单击**全部展开**，显示所有 switch 事例和所有 try/catch/finally 块。 单击**还原**或**全部折叠**返回这些设计器为其默认状态，你可以单击单个事例/块来查看其内容。