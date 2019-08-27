---
title: 工作流设计器-如何：使用变量设计器
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f90cbb58406df2410361bf9409c843b5c35b4331
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949039"
---
# <a name="how-to-use-the-variable-designer"></a>如何：使用变量设计器

变量设计器用于创建在数据绑定方案和条件语句中使用的变量。 通过单击来访问在设计器**变量**设计画布左下角的按钮。 该设计器包含一组这些变量显示在表格窗体中并可以按每一列标题排序除外**默认**列。 每个变量都包含名称、变量类型、作用域和默认值（如果有）。 名称和默认值是可编辑的文本字段，而类型和作用域是下拉项。 作用域是调用变量设计器时选择的活动。 如果无法在选定的范围内创建某个变量，则范围将默认为允许变量在其范围内创建的最靠近选定内容的上级活动。 有关详细信息，请参阅[变量和参数 (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)。

 在用户显式使用其中一种排序控件、关闭并重新打开变量设计器或创建另一个变量后，才会应用排序顺序。

## <a name="to-create-a-new-variable"></a>创建新变量

1. 在 Visual Studio 中打开工作流或活动解决方案。

2. 在设计画布上，选择工作流中的一个活动。

3. 通过单击打开变量设计器**变量**设计画布左下角的按钮。 此时将显示变量设计器。

4. 单击标记为空的行**变量创建**。 这会将新行添加使用新的变量使用以下默认值： 为 variablex**名称**其中 x 是一个整数，其初始值为 1 的自动递增，从而创建唯一变量名**字符串**有关**变量类型**，和**序列**有关**作用域**。 为添加任何值**默认**。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除变量，通过单击选择该变量，然后按**删除**密钥。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和参数](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
- [如何：使用参数设计器](../workflow-designer/how-to-use-the-argument-designer.md)