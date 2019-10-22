---
title: 如何：创建基本纹理着色器 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 5af113fb-6415-4be0-8b23-10fddb10e80a
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 59a926ab35e04aa120bc57250c3e5b2712858aa5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664488"
---
# <a name="how-to-create-a-basic-texture-shader"></a>如何：创建基本纹理着色器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本文档演示如何使用着色器设计器和定向关系图着色器语言 (DGSL) 创建单纹理着色器。 此着色器直接将最终颜色设置为从纹理中采样的 RGB 和 alpha 值。

 本文档演示了这些活动：

- 移除着色器关系图中的节点

- 将节点添加到关系图

- 设置着色器参数

- 设置参数可见性

- 连接节点

## <a name="creating-a-basic-texture-shader"></a>创建基本纹理着色器
 可通过将纹理样本的颜色和 alpha 值直接写入最终输出颜色，实现基本的单纹理着色器。

 开始前，请确保显示“属性”  窗口和“工具箱”  。

#### <a name="to-create-a-basic-texture-shader"></a>创建基本纹理着色器

1. 创建要使用的 DGSL 着色器。 若要了解如何向项目添加 DGSL 着色器，请参阅[着色器设计器](../designers/shader-designer.md)中的“入门”部分。

2. 删除“点颜色”  节点。 在“选择”  模式下，选择“点颜色”  节点，然后在菜单栏上选择“编辑”  和“删除”  。 这为在下一步中添加的节点腾出空间。

3. 将“纹理样本”  节点添加到关系图。 在“工具箱”  中的“纹理”  下选择“纹理样本”  ，然后将其移到设计图面。

4. 将“纹理坐标”  节点添加到关系图。 在“工具箱”  中的“纹理”  下选择“纹理坐标”  ，然后将其移到设计图面。

5. 选择要应用的纹理。 在“选择”  模式中，选择“纹理样本”  节点，然后在“属性”  窗口中通过“文件名”  属性指定要使用的纹理。

6. 使纹理可公开访问。 选择“纹理样本”  节点，然后在“属性”  窗口中将“访问”  属性设置为“公共”  。 现可利用其他工具（如**模型编辑器**）设置纹理。

7. 将纹理坐标连接到纹理样本。 在“选择”  模式下，将“纹理坐标”  节点的“输出”  终端移到“纹理样本”  节点的“UV”  终端。 此连接在指定坐标处对纹理进行采样。

8. 将纹理样本连接到最终颜色。 将“纹理示例”  节点的“RGB”  终端移到“最终颜色”  节点的“RGB”  终端，然后将“纹理示例”  节点的“Alpha”  终端移到“最终颜色”  节点的“Alpha”  终端。

   下图显示了已完成的着色器关系图和应用于立方体的着色器预览。

> [!NOTE]
> 在此插图中，飞机用作预览形状，并且已指定一个纹理以更好地演示着色器的效果。

 ![着色器图及其效果预览](../designers/media/digit-texture-effect.png "|::ref1::|")

 某些形状可能会增强某些着色器的预览效果。 若要深入了解如何在着色器设计器中预览着色器，请参阅[着色器设计器](../designers/shader-designer.md)

## <a name="see-also"></a>另请参阅
 [如何：将着色器应用于三维模型](../designers/how-to-apply-a-shader-to-a-3-d-model.md)[图像编辑器](../designers/image-editor.md)[着色器](../designers/shader-designer.md)设计器设计器[节点](../designers/shader-designer-nodes.md)
