---
title: 如何：创建基本 Phong 着色器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: c7c69da8-142b-4d3b-9be9-4be0d5970b25
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7153c02f5cd3d494edb56b218512ba5de87f318a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438416"
---
# <a name="how-to-create-a-basic-phong-shader"></a>如何：创建基本 Phong 着色器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本文档演示如何使用着色器设计器和定向关系图着色器语言 (DGSL) 创建实现经典冯氏照明模型的照明着色器。  
  
 本文档演示了这些活动：  
  
- 将节点添加到着色器关系图  
  
- 断开节点  
  
- 连接节点  
  
## <a name="the-phong-lighting-model"></a>冯氏照明模型  
 冯氏照明模型扩展了朗伯照明模型，包括可反射图面属性的镜面高光。 反射分量提供用于朗伯照明模型的相同定向光源的其他照明，但是会以不同的方式处理其对最终颜色的比例。 镜面高光根据视图方向、光源方向和表面方向之间的关系，以不同的方式影响场景中的每个表面。 它是表面的反射颜色、反射强度和方向，以及光源的颜色、强度和方向共同产生的结果。 在观察者处直接反射光源的表面接收最大反射比例，反射远离观察者的光源的表面无接收比例。 在冯氏照明模型下，将结合一个或多个反射分量来确定对象上每个点的镜面高光颜色和强度，然后将其添加到朗伯照明模型的结果上以产生像素的最终颜色。  
  
 有关 Lambert 光照模型的详细信息，请参阅[如何：创建基本朗伯着色器](../designers/how-to-create-a-basic-lambert-shader.md)。  
  
 开始前，请确保显示“属性”窗口和“工具箱”。  
  
#### <a name="to-create-a-phong-shader"></a>创建冯氏着色器  
  
1. 按照以下方法创建 Lambert 着色器：[如何：创建基本朗伯着色器](../designers/how-to-create-a-basic-lambert-shader.md)。  
  
2. 从“最终颜色”节点断开“朗伯”节点。 选择“朗伯”节点的“RGB”终端，然后选择“断开链接”。 这为在下一步中添加的节点腾出空间。  
  
3. 向关系图添加“添加”节点。 在“工具箱”中的“数学”下选择“添加”，然后将其移到设计图面。  
  
4. 向关系图添加“反射”节点。 在“工具箱”中的“实用工具”下，选择“反射”，然后将其移到设计图面。  
  
5. 添加反射比例。 将“反射”节点的“输出”终端移到“添加”节点的“X”终端，然后将“朗伯”节点的“输出”终端移到“添加”节点的“Y”终端。 这些连接会组合像素的总漫射比例和总反射颜色比例。  
  
6. 将计算得出的颜色值连接到最终颜色。 将“添加”节点的“输出”终端移到“最终颜色”节点的“RGB”终端。  
  
   下图显示了已完成的着色器关系图和应用于茶壶体的着色器预览。  
  
> [!NOTE]
> 为了更好地演示该图中着色器的效果，使用着色器的 **MaterialDiffuse** 参数指定了橙色，并使用  **MaterialSpecular** 和 **MaterialSpecularPower**  参数指定了金属外观。 有关材质参数的信息，请参阅[着色器设计器](../designers/shader-designer.md)中的“预览着色器”部分。  
  
 ![着色器图及其效果预览](../designers/media/digit-lighting-graph.png "Digit-Lighting-Graph")  
  
 某些形状可能会增强某些着色器的预览效果。 若要深入了解如何在着色器设计器中预览着色器，请参阅[着色器设计器](../designers/shader-designer.md)中的“预览着色器”部分  
  
 下图显示了本文档中所述的应用于三维模型的着色器。 **MaterialSpecular** 属性设置为 (1.00, 0.50, 0.20, 0.00)，并将其 **MaterialSpecularPower** 属性设置为 16。  
  
> [!NOTE]
> **MaterialSpecular** 属性确定表面材质的表面光洁度。 高光泽表面（如玻璃或塑料）往往具有白色明亮阴影的反射颜色。 金属表面往往具有接近其漫射颜色的反射颜色。 缎面表面往往具有深灰色的反射颜色。  
>   
> **MaterialSpecularPower** 属性确定高光的强度。 高反射强度模拟更暗淡、更局部化的高光效果。 较低的反射强度模拟大幅度的强烈高光，其可能会过度饱和并遮掩整个表面的颜色。  
  
 ![应用于模型的冯氏照明](../designers/media/digit-lighting-model.png "Digit-Lighting-Model")  
  
 有关如何向三维模型应用着色器的详细信息，请参阅[如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)。  
  
## <a name="see-also"></a>请参阅  
 [如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)   
 [如何：导出着色器](../designers/how-to-export-a-shader.md)   
 [如何：创建基本朗伯着色器](../designers/how-to-create-a-basic-lambert-shader.md)   
 [着色器设计器](../designers/shader-designer.md)   
 [着色器设计器节点](../designers/shader-designer-nodes.md)
