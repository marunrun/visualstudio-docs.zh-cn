---
title: 向 UML 模型元素添加构造型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, stereotypes
ms.assetid: 82545252-83ce-4e11-a419-61373be75d16
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5bba638a595a01f17e4b7e4f8269a69cb6e466a1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430487"
---
# <a name="add-stereotypes-to-uml-model-elements"></a>向 UML 模型元素添加构造型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以向 UML 模型元素添加构造型，以对其进行批注并为其提供专用属性。 要向模型元素添加构造型，必须在配置文件中定义构造型，并将该配置文件链接到包或包含模型元素的模型。 每个构造型只能添加到特定类型的模型元素，如 UML 类、用例或组件。  
  
 例如，如果要使用 «规范» 构造型定义 UML 类，必须在链接到标准配置文件 L2 的包或模型中创建该类。  
  
 默认情况下，每个模型均链接到 UML 标准配置文件 L2 和 L3。  
  
### <a name="to-link-a-profile-to-a-model-or-a-package"></a>将配置文件链接到模型或包  
  
1. 打开**UML 模型资源管理器**。 上**体系结构**菜单，依次指向**Windows**，然后单击**UML 模型资源管理器**。  
  
2. 找到包含要将配置文件中的构造型应用到的所有元素的包或模型。  
  
3. 右键单击包或模型，然后单击**属性**。  
  
4. 在中**属性**窗口中，将**配置文件**属性设置为包含你想要使用的构造型的配置文件。  
  
     配置文件的构造型会立即在该模型或包中的所有元素上可用。 如果包中包含其他包，构造型还会在这些包内的元素上可用。  
  
### <a name="to-add-stereotypes-to-model-elements-or-relationships"></a>向模型元素或关系添加构造型  
  
1. 右键单击模型元素或关系图上或在关系**UML 模型资源管理器**，然后单击**属性**。  
  
    > [!NOTE]
    > 要向多个元素添加相同构造型，可以选择多个元素，然后右键单击其中之一。  
  
2. 单击**构造型**属性，然后选择你想要应用的构造型。  
  
     对于大多数类型的元素和关系，所选择的构造型在模型元素的 «尖括号» 内显示。  
  
    > [!NOTE]
    > 如果无法看到**构造型**属性，或如果未显示所需的构造型，验证模型元素是内包或相应的配置文件链接到模型。  
  
3. 某些构造型允许你设置模型元素的其他属性的值。 若要查看这些属性，请展开**构造型**属性。  
  
### <a name="to-create-model-elements-within-a-package"></a>在包中创建模型元素  
  
1. 在 UML 类图中，或在创建包**UML 模型资源管理器**。  
  
2. 使用以下方式之一向包中添加模型元素：  
  
    - 在 UML 类图中，单击与某个元素对应的工具，然后在关系图上的包内单击。  
  
         \- 或 -  
  
    - 在 UML 模型资源管理器中右键单击包，指向**添加**，然后单击元素类型。  
  
         \- 或 -  
  
    - 在 UML 模型资源管理器中，将现有元素拖动到包中。  
  
         \- 或 -  
  
    - 将关系图链接到包，然后在关系图中创建元素。  
  
         要执行此操作，右键单击关系图的空白部分，然后单击**属性**。 在中**属性**窗口中，将**链接的包**到所需的包。  
  
         在关系图中创建的所有新元素都将在该包中定义。  
  
         只能对某些类型的关系图执行此操作。  
  
## <a name="see-also"></a>请参阅  
 [定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)   
 [自定义模型使用配置文件和构造型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)   
 [定义包和命名空间](../modeling/define-packages-and-namespaces.md)   
 [UML 类的构造型的颜色](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)
