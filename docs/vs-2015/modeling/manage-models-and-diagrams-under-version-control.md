---
title: 管理模型和版本控制下的关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- models, version control
ms.assetid: ca6443e3-6d11-4da8-aae7-ca7dcc410076
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 76e8c92707279979cec6406bd1bcd5ad44a1f315
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825785"
---
# <a name="manage-models-and-diagrams-under-version-control"></a>管理版本控制下的模型和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

管理包括代码图（.dgml 文件）在内的建模项目和关系图的不同版本，方法是 [使用 Team Foundation 版本控制或 Git](https://msdn.microsoft.com/library/33267cee-fe5f-4aa3-b2cd-6d22ceace314)；利用本地 Team Foundation Server 或利用 Visual Studio Team Services 在云中实施。  
  
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
> [!IMPORTANT]
> 当多个用户使用同一个建模项目时，请务必小心。 了解如何才能 [在中型或大型项目中组织模型](../modeling/structure-your-modeling-solution.md)。  
  
## <a name="ModelingProjects"></a> 建模项目中的文件  
 多个用户可能会同时处理一个建模项目，假设他们处理的是不同的文件。  
  
 若要避免或解决不同用户所做更改之间的冲突，则一定要了解模型是如何存储在文件中的。  
  
- 每个包都存储在单独的 **.uml** 文件中，并保存在 **ModelDefinition** 项目文件夹中。 模型也有一个 **.uml** 文件。 如果删除或损坏其中一个文件，则相应的包或模型将会丢失。  
  
- 每个关系图都存储在两个文件中。 例如，类图具有：  
  
  - **DiagramName.classdiagram** - 如果删除或损坏了此文件，则该关系图将会丢失，但其中显示的类和关联将仍在模型中，并可在 UML 模型资源管理器中查看。  

  - **DiagramName.classdiagram.layout** - 如果删除了此文件，则这些形状将仍会显示在关系图中，但会丢失其大小和位置。 每个布局文件都隶属于关系图文件。 若要查看它，请在解决方案资源管理器中单击关系图文件旁边的 [+]。  
  
> [!NOTE]
> 请务必保持文件之间的一致性。 例如，如果使用源控件回滚 .uml 文件中的更改，则应该同时回滚 .*diagram 和 .layout 文件中的相应更改。 中表示的元素。\*如果它们不在.uml 文件中还表示，关系图文件将会丢失。  
  
## <a name="Shared"></a> 处理共享建模项目  
 若要最大程度减少某个项目不同部分中并发工作之间的冲突：  
  
- 将建模项目分为表示不同工作区域的包。 将整个模型移到包中，而不是将其留在根模型中。 有关详细信息，请参阅[定义包和命名空间](../modeling/define-packages-and-namespaces.md)。  
  
- 不同的用户不应同时处理同一个包或关系图。  
  
- 如果正在使用配置文件，请确保每个人都已安装相同的配置文件。 请参阅[自定义模型使用配置文件和构造型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)。  
  
- 若要帮助确保仅更改正在处理的包：  
  
  - 设置 UML 类、组件或用例关系图的“LinkedPackage”  属性。  

  - 在 UML 模型资源管理器中，请在创建好时就将活动或互动拖动到包中。 当在活动或序列关系图中创建第一个节点时，这个元素将出现在 UML 模型资源管理器中。  
  
- 为了帮助跟踪包，可重命名包文件来反映实际的包名称。  
  
- 在 [!INCLUDE[esprscc](../includes/esprscc-md.md)]中，始终对完整的建模项目执行“签入”  和“获取最新版本”  操作，请始终不要对单独文件执行这些操作。  
  
- 请总是在签入建模项目前及时执行“获取”  操作。  
  
- 执行“获取”  操作之前一定要关闭所有关系图。  
  
    > [!NOTE]
    > 如果在执行“获取”  操作时，某个文件处于打开状态，并且该操作造成本地更改，则将提示重新加载该文件。 在这种情况下，单击“否”  ，然后重新加载完整项目。 在“解决方案资源管理器”  中右击该建模项目节点，单击“卸载项目”  ，然后再单击“重新加载项目”  。  
  
### <a name="Exclusive"></a> 需要排他访问该模型的更改  
 在进行以下类型的更改之前，请确保在整个项目上具有签出锁定。  
  
- 重命名或删除从其他包中引用的元素。  
  
- 更改跨越包边界的关系的属性。  
  
- 若要了解有关签出锁定的信息，请参阅 [签出和编辑文件](https://msdn.microsoft.com/library/eb404d63-c448-4994-9416-3e6d50ec554a)。  
  
##### <a name="to-move-a-diagram-file-in-or-out-of-a-project-folder"></a>将关系图文件移入或移出项目文件夹  
  
1. 启动“Visual Studio 开发人员命令提示”  。  
  
2. 使用 **tf rename** 来移动关系图文件及其 **.layout** 文件：  
  
     `tf rename sourcePath targetPath`  
  
3. 在“解决方案资源管理器”中，右击该文件，然后单击“从项目中排除”  。  
  
4. 将该文件添加到目标文件夹。  
  
     在“解决方案资源管理器”中，右击目标文件夹或项目，指向“添加”  ，然后单击“现有项”  。 在对话框中，选择关系图文件，然后单击“添加”  。 将自动添加布局文件。  
  
    > [!NOTE]
    > 不能将该文件移到不同的项目中。  
  
## <a name="Merging"></a> 合并模型文件和关系图中的更改  
 在多个用户并发使用一个模型之后， [!INCLUDE[esprscc](../includes/esprscc-md.md)] 将提示合并模型文件中的更改。 按照前面几节中所述内容来处理单独项目将避免大部分合并。 通常，可自动安全合并剩余冲突。 以下类型的更改不会导致困难：  
  
- 生命线的类型。 当将生命线添加到交互（序列图）时，除非已从现有类型创建了生命线，否则其类型存储在根模型中。  
  
- 新活动和交互最初存储在根模型中。  
  
- 添加元素和关系。  
  
- 重命名或删除仅从自身包内引用的元素。  
  
## <a name="see-also"></a>请参阅  
 [分析体系结构和建模](../modeling/analyze-and-model-your-architecture.md)   
 [共享模型和导出关系图](../modeling/share-models-and-exporting-diagrams.md)
