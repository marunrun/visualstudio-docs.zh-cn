---
title: 工作流设计器-如何：使用参数设计器
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8c333e78de17a3af5b4f7f0be46c19cf3120231d
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746898"
---
# <a name="how-to-use-the-argument-designer"></a>如何：使用参数设计器

自变量设计器轻松允许数据流入和流出活动。 通过单击访问设计器**自变量**设计画布左下角的按钮。 在设计器包含一系列参数显示在表格窗体，可以按每一列标题排序除外**默认值**列。 每个自变量都包含名称、输入/输出/输入-输出/属性方向、类型和默认表达式值（如果有）。 名称和默认的表达式值都是可编辑的文本字段，类型和方向是下拉项。 有关详细信息，请参阅[变量和参数 (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)。

## <a name="to-create-a-new-argument"></a>创建新自变量

1. 在 Visual Studio 中打开工作流或活动解决方案。

2. 通过单击打开自变量设计器**自变量**设计画布左下角的按钮。 此时将显示参数设计器。

3. 单击标记为空的行**创建自变量**。 这会将新行添加使用新的自变量，使用以下默认值： 为 argumentx**名称**其中 x 是一个整数，其初始值为 1 来创建唯一的参数名称，将自动递增**中**有关**方向**，和**字符串**有关**自变量类型**。 为添加任何值**默认值**。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除参数，通过单击选择该参数，然后按**删除**密钥。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和参数](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)