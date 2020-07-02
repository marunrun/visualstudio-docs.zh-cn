---
title: 工作流设计器-如何：使用痕迹导航
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 4a688056-37dc-406a-9071-be2141e192fe
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a432d7cfc40ad6116f570d0e7beb4bfc5b40493
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817458"
---
# <a name="how-to-use-breadcrumb-navigation"></a>如何：使用痕迹导航

有三种主要方法可以更改工作流设计器中显示的活动集：

1. 双击以钻入子活动。

2. 单击痕迹栏上的按钮以导航到祖先活动。

3. 就地展开或折叠活动。

## <a name="using-breadcrumb-navigation"></a>使用痕迹导航

1. 双击工作流设计器的活动，将根活动更改为单击的活动。 然后，在根位置完全展开单击的活动，并在痕迹导航栏中显示其上级。 这有时称为钻入或钻出某个活动。

2. 若要导航到当前根活动的一个祖先，请单击痕迹栏中的相应活动。

## <a name="expanding-or-collapsing-an-activity-in-place"></a>就地展开或折叠活动

1. 单击活动上的 V 形将就地展开或折叠该活动。

2. 单击该按钮更改展开状态时，新的展开状态将保存在 XAML 中。

    > [!WARNING]
    > 并非所有活动都可就地展开。 在两种情况下不能就地展开活动：一种是活动的父级不允许其子级就地展开（例如，流程图中的活动不能就地展开），另一种是活动设计器不允许自身就地展开。 尽管工作流设计器中包含的所有活动设计器都没有后一种行为，但某些自定义活动可能会表现出这种行为。

## <a name="expanding-all-or-collapsing-all-activities"></a>展开或折叠所有活动

1. 使用用户界面中的 "**全部展开**" 和 "**全部折叠**" 按钮可展开或折叠当前痕迹根下的所有活动。 请注意，全部展开和全部折叠是全局状态。 这意味着，当你使用痕迹导航更改根活动时，"全部展开" 或 "全部折叠" 状态将保持不变，直到你单击 "**还原**"。

2. 应用 "全部展开" 或 "全部折叠" 状态后，可以单击显示的 "**还原**" 按钮，返回到之前应用于每个活动的状态。

    > [!WARNING]
    > 如果某个活动（如 <xref:System.Activities.Statements.Flowchart> ）已取消就地展开，则在**流程图**设计器中将禁用与 "**全部展开**" 和 "**全部折叠**" 按钮相关联的功能。 有关**流程图**设计器的详细信息，请参阅[流程图](../workflow-designer/flowchart-activity-designer.md)主题。

    > [!WARNING]
    > 全部展开还会在**Switch**和**TryCatch**活动设计器中产生特殊影响。 单击 "**全部展开**" 时，将显示所有的开关事例和所有 try/catch/finally 块。 单击 "**还原**" 或 "**全部折叠**" 会将这些设计器恢复为其默认状态，从中可以单击单个 case/块来查看其内容。
