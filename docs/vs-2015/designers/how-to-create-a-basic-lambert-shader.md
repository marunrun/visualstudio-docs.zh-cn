---
title: 如何：创建基本朗伯着色器 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: ec5c10fb-9600-4240-8280-d59451ea1d68
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 038b3e7db7f1e3b79ee3e41b6e256216a39b91bd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664554"
---
# <a name="how-to-create-a-basic-lambert-shader"></a>如何：创建基本朗伯着色器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本文档演示如何使用着色器设计器和定向关系图着色器语言 (DGSL) 创建实现经典朗伯照明模型的照明着色器。

 本文档演示了这些活动：

- 将节点添加到着色器关系图

- 断开节点

- 连接节点

## <a name="the-lambert-lighting-model"></a>朗伯照明模型
 朗伯照明模型将环境照明和方向照明应用到三维场景中的阴影对象。 环境分量在三维场景中提供基本照明级别。 方向分量提供来自定向（远）光源的额外照明。 环境照明会均匀影响场景中的所有表面，而不考虑其方向。 对于给定表面，它是表面的环境色和场景中环境照明的颜色和强度的结合产物。 定向照明根据相对于光源方向的表面方向，以不同方式影响场景中的每个表面。 它是表面的漫射颜色和方向，以及光源的颜色、强度和方向生成的结果。 直接面向光源的表面接收比例最大，直接背对的表面无接收比例。 在朗伯照明模型下，会结合环境分量和一个或多个定向分量来确定对象上每个点的总漫射颜色比例。

 开始前，请确保显示“属性”窗口和“工具箱”。

#### <a name="to-create-a-lambert-shader"></a>创建朗伯着色器

1. 创建要使用的 DGSL 着色器。 若要了解如何向项目添加 DGSL 着色器，请参阅[着色器设计器](../designers/shader-designer.md)中的“入门”部分。

2. 从“最终颜色”节点断开“点颜色”节点。 选择“点颜色”节点的“RGB”终端，然后选择“断开链接”。 让“Alpha”终端保持连接状态。

3. 向关系图添加“朗伯”节点。 在“工具箱”中的“实用工具”下选择“朗伯”，然后将其移到设计图面。 朗伯节点基于环境和漫射照明参数计算像素的总漫射颜色比例。

4. 将“点颜色”节点连接到“朗伯”节点。 在“选择”模式下，将“点颜色”节点的“RGB”终端移到“朗伯”节点的“漫射颜色”终端。 此连接为朗伯节点提供了像素的内插漫射颜色。

5. 将计算得出的颜色值连接到最终颜色。 将“朗伯”节点的“输出”终端移到“最终颜色”节点的“RGB”终端。

   下图显示了已完成的着色器关系图和应用于茶壶体的着色器预览。

> [!NOTE]
> 为了更好地演示该图着色器的效果，使用着色器的 **MaterialDiffuse** 参数指定了橙色。 游戏或应用可使用此参数为每个对象提供唯一的颜色值。 有关材质参数的信息，请参阅[着色器设计器](../designers/shader-designer.md)中的“预览着色器”部分。

 ![着色器关系图和其效果的预览。](../designers/media/digit-lambert-effect-graph.png "数字朗伯-图形")

 某些形状可能会增强某些着色器的预览效果。 若要深入了解如何在着色器设计器中预览着色器，请参阅[着色器设计器](../designers/shader-designer.md)中的“预览着色器”部分。

 下图显示了本文档中所述的应用于三维模型的着色器。

 ![应用于模型的朗伯照明。](../designers/media/digit-lambert-effect-result.png "数字朗伯-结果")

 若要深入了解如何将向三维模型应用着色器，请参阅[如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)。

## <a name="see-also"></a>请参阅
 [如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)[如何：导出着色](../designers/how-to-export-a-shader.md)器[如何：创建基本冯氏着色](../designers/how-to-create-a-basic-phong-shader.md)器[设计](../designers/shader-designer.md)器着色器设计器[节点](../designers/shader-designer-nodes.md)
