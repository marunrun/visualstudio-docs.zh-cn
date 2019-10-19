---
title: 如何：使用参数设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a436d33bbb7c791f3f192357fded779fa77d148d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659115"
---
# <a name="how-to-use-the-argument-designer"></a>如何：使用自变量设计器
与以前版本的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 相比，该参数设计器使数据流入和流出某个活动更容易。 通过单击设计画布左下角的 "**自变量**" 按钮可访问该设计器。 该设计器包含一个参数列表，该列表以表格形式显示，并可按每个列标题进行排序（"**默认值**" 列除外）。 每个自变量都包含名称、输入/输出/输入-输出/属性方向、类型和默认表达式值（如果有）。 名称和默认的表达式值都是可编辑的文本字段，类型和方向是下拉项。 [!INCLUDE[crabout](../includes/crabout-md.md)] 参数，请参阅[变量和参数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)。

### <a name="to-create-a-new-argument"></a>创建新自变量

1. 在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中打开一个工作流或活动解决方案。

2. 通过单击设计画布左下角的 "**参数**" 按钮打开参数设计器。 此时将显示参数设计器。

3. 单击标记为 "**创建参数**" 的行。 这会使用以下默认值添加一个具有新自变量的新行： "**名称**" 为 argumentx，其中 x 是一个整数，其初始值为 "1"，将自动递增以创建唯一的参数名称，并**在**"**方向**"**参数类型**的和**字符串**。 不会为**默认值**添加值。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除某个参数，请单击该参数，然后按**delete**键。

## <a name="see-also"></a>请参阅
 [使用工作流设计器](../workflow-designer/using-the-workflow-designer.md)[变量和参数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)