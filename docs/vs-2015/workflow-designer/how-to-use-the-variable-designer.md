---
title: 如何：使用变量设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4744864824da5efb238e9af1a5a12fcef79ea4ff
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659079"
---
# <a name="how-to-use-the-variable-designer"></a>如何：使用变量设计器
变量设计器用于创建在数据绑定方案和条件语句中使用的变量。 通过单击设计画布左下角的 "**变量**" 按钮可访问该设计器。 设计器包含一个变量列表，该列表显示在表格窗体中并可按每个列标题进行排序（**默认**列除外）。 每个变量都包含名称、变量类型、作用域和默认值（如果有）。 名称和默认值是可编辑的文本字段，而类型和作用域是下拉项。 作用域是调用变量设计器时选择的活动。 如果无法在选定的范围内创建某个变量，则范围将默认为允许变量在其范围内创建的最靠近选定内容的上级活动。 [!INCLUDE[crabout](../includes/crabout-md.md)] 变量，请参阅[变量和参数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)。

 在用户显式使用其中一种排序控件、关闭并重新打开变量设计器或创建另一个变量后，才会应用排序顺序。

### <a name="to-create-a-new-variable"></a>创建新变量

1. 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中打开一个工作流或活动解决方案。

2. 在设计画布上，选择工作流中的一个活动。

3. 通过单击设计画布左下角的 "**变量**" 按钮打开变量设计器。 此时将显示变量设计器。

4. 单击标记为 "**创建变量**" 的空行。 这会使用以下默认值添加一个具有新变量的新行： variablex 作为**名称**，其中 x 是一个整数，其初始值为1，该值自动递增以创建唯一变量名，**字符串** **范围**的类型和**序列**。 不会添加**默认**值。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除某个变量，请单击该变量，然后按**delete**键。

## <a name="see-also"></a>请参阅
 [使用工作流设计器](../workflow-designer/using-the-workflow-designer.md)[变量和参数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)[如何：使用参数设计器](../workflow-designer/how-to-use-the-argument-designer.md)