---
title: UML 序列图描述控制流片段与 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.sequencediagram.combinedfragment.interactionoperand
- vs.teamarch.sequencediagram.combinedfragment
helpviewer_keywords:
- UML sequence diagrams, control flow
- UML sequence diagrams, fragments
- sequence diagrams, fragments
- sequence diagrams, control flow
ms.assetid: efcc0949-be7e-4cf4-99ef-47c36b3803ae
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c296be2e3a00efcdf48bdd6e4442e88fc32b3695
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422541"
---
# <a name="describe-control-flow-with-fragments-on-uml-sequence-diagrams"></a>使用 UML 序列图中的片段描述控制流
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 序列图中，可以通过 *组合片段* 显示循环、分支和其他备选项。  
  
 组合片段包括一个或多个 *交互操作数*，并且其中每个都包含了一个或多个消息、交互使用或组合片段。  
  
> [!NOTE]
> 本主题介绍序列图中的片段。 有关如何读取 UML 序列图的详细信息，请参阅[UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)。 有关如何绘制 UML 序列图的详细信息，请参阅[UML 序列图：指导原则](../modeling/uml-sequence-diagrams-guidelines.md)。  
  
 ![组合片段中的使用两个交互操作数](../modeling/media/uml-seqfragments.png "UML_SeqFragments")  
  
 图中显示的元素如下所示。  
  
1. 组合片段。 组合片段有好几种类型。 此示例是 Alt 组合片段，你可以使用它显示可能发生消息备选序列。  
  
2. 交互操作数。 每个组合片段都包含至少一个交互操作数，它可以包含消息、交互使用和较小的组合片段。 在此示例中，Alt 组合片段有两个交互操作数，显示了两个消息备选序列。  
  
3. 你可以通过单击其内部分别选择每个交互操作数。 此示例选择了顶部的交互操作数，因此，可以看见其边界。 通常，仅交互操作数之间的分隔线可见。  
  
    > [!NOTE]
    > 若要选择顶部的交互操作数，则不能在太靠近组合片段的顶部位置单击。  
  
4. 临界。 你可以为每个交互操作数提供一个临界。 描述将在其下执行交互操作数内的消息的条件。  
  
## <a name="creating-combined-fragments"></a>创建组合片段  
 有关可创建的片段种类的列表，请参阅 [组合片段的种类](#KindsOfFragment)。  
  
#### <a name="to-create-a-combined-fragment"></a>若要创建组合片段  
  
1. 选择一条消息或消息序列，它们都是在相同生命线或执行匹配项开始的消息。  
  
   > [!NOTE]
   > 如果选择多个消息时，它们必须形成不间断的序列。  
  
2. 右键单击其中一条消息，指向“外侧代码” ，然后单击想要的组合片段的种类，如“Alt 组合片段” 。  
  
    将显示新的组合片段。 标题指示所选的组合片段的种类，如“Alt” 。  
  
    在组合片段内，有包含所选消息的片段。  
  
   你可以将更多交互操作数添加到某些类型的组合片段。  
  
   重新排列组合片段中的消息后，请选择快捷菜单上的“重新排列布局”  以调整组合片段帧的大小。  
  
#### <a name="to-add-a-new-interaction-operand-to-a-combined-fragment"></a>若要将新的交互操作数添加到组合片段  
  
1. 右键单击交互操作数 (2) 内部、任何包含的片段外部和组合片段标题下的空白区域。  
  
2. 指向“添加” 。  
  
3. 单击“前面的交互操作数” ，或“后面的交互操作数” 。  
  
4. 通过使用消息工具或者通过复制并粘贴现有消息，可以在新的交互操作数内部添加消息。  
  
   可以设置交互操作数的“临界”  属性来描述执行其内部的消息的条件。 例如，在“循环”  组合片段中，可以使用临界指定循环继续的条件。 在“Alt”  组合片段中，可以为每个交互操作数指定单独的条件。  
  
#### <a name="to-set-the-guard-of-an-interaction-operand"></a>若要设置交互操作数的临界  
  
1. 单击交互操作数 (2) 内部、任意包含的片段外部的空白区域。  
  
    将在交互操作数周围以及临界条件周围显示选择边框。  
  
    “属性”  窗口中的标题将显示“交互操作数” 。  
  
2. 键入临界条件。  
  
    该条件将显示在片段 (4) 顶部附近。  
  
   你可以设置某些种类的组合片段的属性。  
  
#### <a name="to-set-or-view-the-properties-of-a-combined-fragment"></a>若要设置或查看组合片段的属性  
  
- 右键单击组合片段的标题，然后单击“属性” 。  
  
    > [!NOTE]
    > 不同种类的组合片段具有不同的属性。  
  
## <a name="KindsOfFragment"></a> 组合片段的种类  
  
### <a name="fragments-describing-control-flow"></a>描述控制流的片段  
 简单的序列图只显示一个典型的序列。 你可以使用以下类型的组合片段来描述可能发生在不同场合的变体。  
  
|片段类型|描述|  
|-------------------|-----------------|  
|**Opt**|可选。 包含一个可能或可能不会出现的序列。 你可以在临界中指定在其中出现的条件。|  
|**Alt**|包含片段列表，该列表包含了消息的备选序列。 在任何情况下，都只出现一个序列。<br /><br /> 你可以将临界放在每个片段中以指示其可以运行的条件。 如果其他任何临界不为 true，则 **else** 的临界将指示应运行的片段。 如果所有临界都为 false，并且没有任何 **else**，则不执行任何片段。|  
|**Loop**|片段会重复几次。 你可以在临界中指示在其中应重复的条件。<br /><br /> 循环组合片段具有“Min”  和“Max” 属性，这表示片段可以重复的次数最小值和最大值。 默认情况下没有限制。|  
|**中断**|如果执行此片段，则将放弃序列的其余部分。 你可以使用临界来指示在其中发生中断的条件。|  
|**Par**|并行。 片段中的事件可能交错。|  
|**Critical**|在 Par 或 Seq 片段中使用。 指示此片段中的消息不得与其他消息交错。|  
|**Seq**|有两个或多个操作数片段。 包含相同生命线的消息必须以片段的顺序出现。 如果不包含相同生命线，来自不同片段的消息可能会并行交错。|  
|**Strict**|有两个或多个操作数片段。 片段必须以指定的顺序出现。|  
  
### <a name="fragments-about-how-to-interpret-the-sequence"></a>关于如何解释序列的片段  
 默认情况下，序列图会说明一系列可能出现的消息。 在正在运行的系统中，未选择在序列图中显示的其他消息可能会出现。  
  
 以下片段类型可以用于更改此解释。  
  
|片段类型|描述|  
|-------------------|-----------------|  
|**请考虑**|指定此片段描述的消息列表。 其他消息可在正在运行的系统中出现，但此描述的目的意义不大。<br /><br /> 键入“消息”  属性中的列表。|  
|**忽略**|此片段未描述的消息列表。 它们可在正在运行的系统中出现，但此描述的目的意义不大。<br /><br /> 键入“消息”  属性中的列表。|  
|**Assert**|操作数片段指定唯一有效的序列。 通常用于“考虑”或“忽略”片段。|  
|**neg**|不可能在此片段中出现的序列。 通常用于“考虑”或“忽略”片段。|  
  
## <a name="see-also"></a>请参阅  
 [UML 序列关系图：指导原则](../modeling/uml-sequence-diagrams-guidelines.md)   
 [UML 序列关系图：引用](../modeling/uml-sequence-diagrams-reference.md)   
 [编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)
