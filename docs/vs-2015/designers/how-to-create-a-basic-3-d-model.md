---
title: 如何：创建基本三维模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: a0d97966-2df8-449b-a8cf-5a19684dc773
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 834651f525ccb292f82d5cf0ab5a7068a1cf7f20
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197825"
---
# <a name="how-to-create-a-basic-3-d-model"></a>如何：创建基本三维模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本文档说明如何使用模型编辑器创建基本三维模型。  
  
 本文档演示了这些活动：  
  
- 将对象添加到场景中  
  
- 选择面和边缘  
  
- 转换选定内容  
  
- 使用“细分面”  和“延伸面”  工具  
  
- 使用“三角测量”  命令  
  
## <a name="creating-a-basic-3-d-model"></a>创建基本三维模型  
 可使用模型编辑器创建和修改游戏或应用的三维模型和场景。 下列步骤说明如何使用模型编辑器创建房子的简化三维模型。 简化模型可用作仍在创建的最终艺术资产的替代物、用作冲突检测的网格或用作在所表示的对象太远而无法从更详细的呈现中获益时要使用的详细程度低的模型。  
  
 完成后，模型应类似于：  
  
 ![已完成的简约建筑模型](../designers/media/gfx-model-demo-house-final.png "gfx_model_demo_house_final")  
  
 开始前，请确保显示“属性”  窗口和“工具箱”  。  
  
#### <a name="to-create-a-simplified-3-d-model-of-a-house"></a>创建房子的简化三维模型  
  
1. 创建要使用的三维模型。 若要了解如何向项目添加模型，请参阅[模型编辑器](../designers/model-editor.md)中的“入门”部分。  
  
2. 将立方体添加到场景中。 在“工具箱”  窗口的“形状”  下，选择“立方体”  ，然后将其移动到设计图面。  
  
3. 切换到面选择。 在“模型编辑器”工具栏上，选择“选择面”  。  
  
4. 细分立方体的顶部。 在面选择模式下，选择立方体一次将其激活以供选择，然后选择立方体的顶部以选择顶部面。 在“模型编辑器”工具栏上，选择“细分面”  。 这会向立方体的顶部添加新顶点，这些顶点将立方体拆分为四个大小相等的分区。  
  
    ![已细分处理立方体的顶端](../designers/media/gfx-model-demo-house-subdiv.png "gfx_model_demo_house_subdiv")  
  
5. 延伸立方体的两条相邻边 - 例如，立方体的前边和右边。 在面选择模式下，选择立方体一次将其激活以供选择，然后选择立方体的一边。 按住 Ctrl 键，选择与首先选择的立方体边相邻的另一个边，然后在“模型编辑器”工具栏上选择“延伸面”  。  
  
    ![已延伸立方体的两侧](../designers/media/gfx-model-demo-house-extrude.png "gfx_model_demo_house_extrude")  
  
6. 扩展其中一个延伸。 选择刚延伸的某个面，然后在“模型编辑器”工具栏上选择“平移”  工具，并按延伸的方向移动平移操控程序。  
  
    ![已进一步延伸立方体的一侧。](../designers/media/gfx-model-demo-house-extend.png "gfx_model_demo_house_extrude")  
  
7. 对模型进行三角测量。 在“模型编辑器”工具栏上，依次选择“高级”  、“工具”  和“三角化”  。  
  
8. 创建房子的屋顶。 选择“模型编辑器”工具栏上的“选择边”  切换到边选择模式，然后选择立方体将其激活。 当您选择此处显示的边时，请按住 Ctrl 键：  
  
    ![将形成屋顶顶端的边缘](../designers/media/gfx-model-demo-house-edges.png "gfx_model_demo_house_edges")  
  
    选择边后，请在“模型编辑器”工具栏上选择“平移”  工具，然后将平移操控程序上移来创建房子的屋顶。  
  
   简化的房子模型已完成。 下面是应用了平面着色的最终模型：  
  
   ![已完成的简约建筑模型](../designers/media/gfx-model-demo-house-final.png "gfx_model_demo_house_final")  
  
   下一步，您可以将着色器应用于此三维模型。 有关详细信息，请参阅[如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)。  
  
## <a name="see-also"></a>请参阅  
 [如何：三维地形模型](../designers/how-to-model-3-d-terrain.md)   
 [模型编辑器](../designers/model-editor.md)   
 [着色器设计器](../designers/shader-designer.md)
