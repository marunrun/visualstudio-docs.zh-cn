---
title: Add stereotypes to UML model elements | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, stereotypes
ms.assetid: 82545252-83ce-4e11-a419-61373be75d16
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67d489b1446e7205d72b53e160a8c7ca87f216d7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74292338"
---
# <a name="add-stereotypes-to-uml-model-elements"></a>向 UML 模型元素添加构造型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以向 UML 模型元素添加构造型，以对其进行批注并为其提供专用属性。 要向模型元素添加构造型，必须在配置文件中定义构造型，并将该配置文件链接到包或包含模型元素的模型。 每个构造型只能添加到特定类型的模型元素，如 UML 类、用例或组件。

 例如，如果要使用 «规范» 构造型定义 UML 类，必须在链接到标准配置文件 L2 的包或模型中创建该类。

 默认情况下，每个模型均链接到 UML 标准配置文件 L2 和 L3。

### <a name="to-link-a-profile-to-a-model-or-a-package"></a>将配置文件链接到模型或包

1. Open **UML Model Explorer**. On the **Architecture** menu, point to **Windows**, and then click **UML Model Explorer**.

2. 找到包含要将配置文件中的构造型应用到的所有元素的包或模型。

3. Right-click the package or the model and then click **Properties**.

4. In the **Properties** window, set the **Profiles** property to the profiles that contain the stereotypes you want to use.

     配置文件的构造型会立即在该模型或包中的所有元素上可用。 如果包中包含其他包，构造型还会在这些包内的元素上可用。

### <a name="to-add-stereotypes-to-model-elements-or-relationships"></a>向模型元素或关系添加构造型

1. Right-click the model element or relationship, either on a diagram or in **UML Model Explorer**, and then click **Properties**.

    > [!NOTE]
    > 要向多个元素添加相同构造型，可以选择多个元素，然后右键单击其中之一。

2. Click the **Stereotypes** property and select the stereotypes that you want to apply.

     对于大多数类型的元素和关系，所选择的构造型在模型元素的 «尖括号» 内显示。

    > [!NOTE]
    > If you cannot see the **Stereotypes** property, or if the stereotype you want does not appear, verify that the model element is inside a package or a model to which the appropriate profile has been linked.

3. 某些构造型允许你设置模型元素的其他属性的值。 To see these properties, expand the **Stereotypes** property.

### <a name="to-create-model-elements-within-a-package"></a>在包中创建模型元素

1. Create a package either in a UML Class Diagram, or in **UML Model Explorer**.

2. 使用以下方式之一向包中添加模型元素：

    - 在 UML 类图中，单击与某个元素对应的工具，然后在关系图上的包内单击。

         \- 或 -

    - In UML Model Explorer, right-click the package, point to **Add**, and then click an element type.

         \- 或 -

    - 在 UML 模型资源管理器中，将现有元素拖动到包中。

         \- 或 -

    - 将关系图链接到包，然后在关系图中创建元素。

         To do this, right-click a blank part of the diagram and then click **Properties**. In the **Properties** window, set **Linked Package** to the package you want.

         在关系图中创建的所有新元素都将在该包中定义。

         只能对某些类型的关系图执行此操作。

## <a name="see-also"></a>请参阅
 [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md) [Customize your model with profiles and stereotypes](../modeling/customize-your-model-with-profiles-and-stereotypes.md) [Define packages and namespaces](../modeling/define-packages-and-namespaces.md)

