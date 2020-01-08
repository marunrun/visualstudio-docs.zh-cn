---
title: 如何：创建基本三维模型
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a0d97966-2df8-449b-a8cf-5a19684dc773
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce16e436172a7d369f2df8342f6b027b574056ab
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589521"
---
# <a name="how-to-create-a-basic-3d-model"></a>如何：创建基本三维模型

本文说明如何使用模型编辑器创建基本三维模型。 包含以下活动：

- 将对象添加到场景中

- 选择面和边缘

- 转换选定内容

- 使用“细分面”  和“延伸面”  工具

- 使用“三角测量”  命令

## <a name="create-a-basic-3d-model"></a>创建基本三维模型
可使用模型编辑器创建和修改游戏或应用的三维模型和场景。 下列步骤说明如何使用模型编辑器创建房屋的简化三维模型。 简化模型可用作仍在创建的最终艺术资产的替代物、用作冲突检测的网格或用作在所表示的对象太远而无法从更详细的呈现中获益时要使用的详细程度低的模型。

完成后，模型应类似于：

![简约建筑的已完成模型](../designers/media/gfx_model_demo_house_final.png)

开始前，请确保显示“属性”  窗口和“工具箱”  。

### <a name="to-create-a-simplified-3d-model-of-a-house"></a>创建房屋的简化三维模型

1. 创建要使用的三维模型。 若要了解如何向项目添加模型，请参阅[模型编辑器](../designers/model-editor.md)中的“入门”部分。

2. 将立方体添加到场景中。 在“工具箱”  窗口的“形状”  下，选择“立方体”  ，然后将其移动到设计图面。

3. 切换到面选择。 在“模型编辑器”工具栏上，选择“选择面”  。

4. 细分立方体的顶部。 在面选择模式下，选择立方体一次将其激活以供选择，然后选择立方体的顶部以选择顶部面。 在“模型编辑器”工具栏上，选择“细分面”  。 这会向立方体的顶部添加新顶点，这些顶点将立方体拆分为四个大小相等的分区。

    ![已对立方体的顶端进行细分](../designers/media/gfx_model_demo_house_subdiv.png)

5. 延伸立方体的两条相邻边 - 例如，立方体的前边和右边。 在面选择模式下，选择立方体一次将其激活以供选择，然后选择立方体的一边。 按住 Ctrl 键，选择与首先选择的立方体边相邻的另一个边，然后在“模型编辑器”工具栏上选择“延伸面”   。

    ![已延伸立方体的两侧](../designers/media/gfx_model_demo_house_extrude.png)

6. 扩展其中一个延伸。 选择刚延伸的某个面，然后在“模型编辑器”工具栏上选择“平移”  工具，并按延伸的方向移动平移操控程序。

    ![已进一步延伸立方体的一侧。](../designers/media/gfx_model_demo_house_extend.png)

7. 对模型进行三角测量。 在“模型编辑器”工具栏上，依次选择“高级” > “工具” > “三角化”    。

8. 创建房子的屋顶。 选择“模型编辑器”工具栏上的“选择边”  切换到边选择模式，然后选择立方体将其激活。 选择此处显示的边时，请按住 Ctrl 键  ：

    ![将形成屋顶顶端的边缘](../designers/media/gfx_model_demo_house_edges.png)

    选择边后，请在“模型编辑器”工具栏上选择“平移”  工具，然后将平移操控程序上移来创建房子的屋顶。

   简化的房子模型已完成。 下面是应用了平面着色的最终模型：

   ![简约建筑的已完成模型](../designers/media/gfx_model_demo_house_final.png)

   下一步，可以将着色器应用于此三维模型。 有关详细信息，请参阅[如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)。

## <a name="see-also"></a>请参阅

- [如何：构建三维地形模型](../designers/how-to-model-3-d-terrain.md)
- [模型编辑器](../designers/model-editor.md)
- [着色器设计器](../designers/shader-designer.md)
