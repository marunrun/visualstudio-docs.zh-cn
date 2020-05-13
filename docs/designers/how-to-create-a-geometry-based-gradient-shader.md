---
title: 如何：创建基于几何图形的渐变着色器
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4b204405-ba95-4c5e-bd51-ec033a3ebfb6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 96326910a04294e30c410cc96bf9c600bfb3f17c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589444"
---
# <a name="how-to-create-a-geometry-based-gradient-shader"></a>如何：创建基于几何图形的渐变着色器

本文演示如何使用着色器设计器和定向关系图着色器语言创建基于几何图形的渐变着色器。 此着色器将常量 RGB 颜色值按照世界空间中对象的每个点的高度进行缩放。

## <a name="create-a-geometry-based-gradient-shader"></a>创建基于几何图形的渐变着色器

您可以通过将像素的位置并入着色器中来实现基于几何图形的着色器。 在着色语言中，除了 2D 屏幕上的颜色和位置之外，像素还包含其他信息。 像素（在某些系统中称为片段  ）是值的一个集合，描述对应于像素的图面。 本文档中描述的着色器利用全局空间中三维对象的每个像素的高度，来影响片段的最终输出颜色。

开始前，请确保显示“属性”  窗口和“工具箱”  。

1. 创建要使用的 DGSL 着色器。 若要了解如何向项目添加 DGSL 着色器，请参阅[着色器设计器](../designers/shader-designer.md)中的“入门”部分。

2. 从“最终颜色”  节点断开“点颜色”  节点。 选择“点颜色”  节点的“RGB”  终端，然后选择“断开链接”  。 这为在下一步中添加的节点腾出空间。

3. 向关系图添加“乘法”  节点。 在“工具箱”  中的“数学”  下，选择“乘法”  ，然后将其移到设计图面。

4. 向关系图添加“遮罩向量”  节点。 在“工具箱”  中的“实用工具”  下，选择“遮罩向量”  ，然后将其移到设计图面。

5. 为“遮罩向量”  节点指定掩码值。 在“选择”  模式中，选择“遮罩向量”  节点，然后在“属性”  窗口中，将“绿色/Y”  属性设置为“True”  ，并将“红色/X”  、“蓝色/Z”  和“Alpha / W”  属性设置为“False”  。 在此示例中，“红色/X”  、“绿色/Y”  和“蓝色/Z”  属性对应于“世界位置”  节点的 x、y 和 z 分量，并且不使用“Alpha / W”  。 由于仅将“绿色/Y”  设置为“True”  ，因此在遮盖它后，仅保留输入向量的 y 分量。

6. 向关系图添加“世界位置”  节点。 在“工具箱”  中的“常量”  下，选择“世界位置”  ，然后将其移到设计图面。

7. 掩盖片段的世界空间位置。 在“选择”  模式中，将“世界位置”  的“输出”  终端移到“遮罩向量”  节点的“矢量”  终端。 此连接会掩盖片段的位置以忽略 x 和 z 分量。

8. 将 RGB 颜色常量乘以遮罩的世界空间位置。 将“点颜色”  节点的“RGB”  终端移到“乘法”  节点的“Y”  终端，然后将“遮罩向量”  节点的“输出”  终端移到“乘法”  节点的“X”  终端。 此连接按全局空间中的像素高度缩放颜色值。

9. 将缩放的颜色值连接到最终颜色。 将“乘法”  节点的“输出”  终端移到“最终颜色”  节点的“RGB”  终端。

下图显示了已完成的着色器关系图和应用于球体的着色器预览。

> [!NOTE]
> 在此图中，指定了橙色以更好地演示着色器的效果，但因为预览形状在世界空间中没有位置，所以无法在着色器设计器中完全预览该着色器。 必须在实际场景中预览着色器以演示完全效果。

![着色器图及其效果预览](../designers/media/digit-gradient-effect-graph.png)

某些形状可能会增强某些着色器的预览效果。 有关如何在着色器设计器中预览着色器的详细信息，请参阅[着色器设计器](../designers/shader-designer.md)中的“预览着色器”  。

下图显示了应用于在[如何：构建三维地形模型](../designers/how-to-model-3-d-terrain.md)中演示的三维场景的着色器（此着色器为本文档中所述的着色器）。 颜色的强度随着世界中点的高度而增加。

![应用于三维地形模型的渐变效果](../designers/media/digit-gradient-effect-result.png)

有关如何向三维模型应用着色器的详细信息，请参阅[如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)。

## <a name="see-also"></a>请参阅

- [如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [如何：导出着色器](../designers/how-to-export-a-shader.md)
- [如何：构建三维地形模型](../designers/how-to-model-3-d-terrain.md)
- [如何：创建灰度纹理着色器](../designers/how-to-create-a-grayscale-texture-shader.md)
- [着色器设计器](../designers/shader-designer.md)
- [着色器设计器节点](../designers/shader-designer-nodes.md)
