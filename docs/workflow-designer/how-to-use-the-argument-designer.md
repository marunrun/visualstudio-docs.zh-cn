---
title: 工作流设计器-如何：使用参数设计器
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2903c69e3cf50f3ed0392239ee8848a79eb50e20
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75584551"
---
# <a name="how-to-use-the-argument-designer"></a>如何：使用自变量设计器

利用参数设计器，可以轻松地将数据流入和流出活动。 通过单击设计画布左下角的 "**参数**" 按钮访问设计器。 该设计器包含一个参数列表，该列表以表格形式显示，并可按每个列标题进行排序（"**默认值**" 列除外）。 每个自变量都包含名称、输入/输出/输入-输出/属性方向、类型和默认表达式值（如果有）。 名称和默认的表达式值都是可编辑的文本字段，类型和方向是下拉项。 有关详细信息，请参阅[变量和参数（.net）](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)。

## <a name="to-create-a-new-argument"></a>创建新自变量

1. 在 Visual Studio 中打开工作流或活动解决方案。

2. 通过单击设计画布左下角的 "**参数**" 按钮打开参数设计器。 此时将显示参数设计器。

3. 单击标记为 "**创建参数**" 的行。 这会使用以下默认值添加一个具有新自变量的新行： argumentx 作为**名称**，其中 x 是一个整数，其初始值为1，其初始值为1，自动递增以创建唯一的参数名称，**在中**为**方向**，**字符串**用于**参数类型**。 不会为**默认值**添加值。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除某个参数，请单击该参数，然后按**delete**键。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和参数](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
