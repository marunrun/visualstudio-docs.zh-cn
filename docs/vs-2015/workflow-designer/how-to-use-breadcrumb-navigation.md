---
title: 如何：使用痕迹导航 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 4a688056-37dc-406a-9071-be2141e192fe
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1c01e48e6aa34513e57b373150c605cb0a7f5b18
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659157"
---
# <a name="how-to-use-breadcrumb-navigation"></a>如何：使用痕迹导航
更改 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中显示的活动集的方法主要有三种：

1. 双击以钻入子活动。

2. 单击痕迹栏上的按钮以导航到祖先活动。

3. 就地展开或折叠活动。

### <a name="using-breadcrumb-navigation"></a>使用痕迹导航

1. 双击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的活动，将根活动改为单击的活动。 此时单击的活动将在根处完全展开，其祖先将显示在痕迹栏中。 这有时称为钻入或钻出某个活动。

2. 若要导航到当前根活动的一个祖先，请单击痕迹栏中的相应活动。

### <a name="expanding-or-collapsing-an-activity-in-place"></a>就地展开或折叠活动

1. 单击活动上的 V 形将就地展开或折叠该活动。

2. 单击该按钮更改展开状态时，新的展开状态将保存在 XAML 中。

    > [!WARNING]
    > 并非所有活动都可就地展开。 在两种情况下不能就地展开活动：一种是活动的父级不允许其子级就地展开（例如，流程图中的活动不能就地展开），另一种是活动设计器不允许自身就地展开。 虽然 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中包含的所有活动设计器都没有后一种行为，但有的自定义活动可能具有此行为。

### <a name="expanding-all-or-collapsing-all-activities"></a>展开或折叠所有活动

1. 使用用户界面中的 "**全部展开**" 和 "**全部折叠**" 按钮可展开或折叠当前痕迹根下的所有活动。 请注意，全部展开和全部折叠是全局状态。 这意味着，当你使用痕迹导航更改根活动时，"全部展开" 或 "全部折叠" 状态将保持不变，直到你单击 "**还原**"。

2. 应用 "全部展开" 或 "全部折叠" 状态后，可以单击显示的 "**还原**" 按钮，返回到之前应用于每个活动的状态。

    > [!WARNING]
    > 如果某个活动（如 <xref:System.Activities.Statements.Flowchart>）取消了展开功能，则在**流程图**设计器中将禁用与 "**全部展开**" 和 "**全部折叠**" 按钮相关联的功能。 [!INCLUDE[crabout](../includes/crabout-md.md)]**流程图**设计器，请参阅[流程图](../workflow-designer/flowchart-activity-designer.md)主题。

    > [!WARNING]
    > 全部展开还会在**Switch**和**TryCatch**活动设计器中产生特殊影响。 单击 "**全部展开**" 时，将显示所有的开关事例和所有 try/catch/finally 块。 单击 "**还原**" 或 "**全部折叠**" 会将这些设计器恢复为其默认状态，从中可以单击单个 case/块来查看其内容。