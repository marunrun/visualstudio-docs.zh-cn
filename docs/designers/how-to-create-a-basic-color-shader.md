---
title: 如何：创建基本颜色着色器
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c301328a-079a-49e8-b688-4749c01657c0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 162632f0043d23fb111a9e455c1100f9506924a8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589508"
---
# <a name="how-to-create-a-basic-color-shader"></a>如何：创建基本颜色着色器

本文演示如何使用着色器设计器和定向关系图着色器语言 (DGSL) 创建平面颜色着色器。 此着色器将最终颜色设置为常量 RGB 颜色值。

## <a name="create-a-flat-color-shader"></a>创建平面颜色着色器

可将 RGB 颜色常量的颜色值写入最终输出颜色来实现平面颜色着色器。

开始前，请确保显示“属性”  窗口和“工具箱”  。

1. 创建要使用的 DGSL 着色器。 若要了解如何向项目添加 DGSL 着色器，请参阅[着色器设计器](../designers/shader-designer.md)中的“入门”部分。

2. 删除“点颜色”  节点。 使用“选择”工具选择“点颜色”节点，然后在菜单栏上选择“编辑” > “删除”     。

3. 将“颜色常量”  节点添加到关系图。 在“常量”  的“工具箱”  中，选择“颜色常量”  ，然后将其移到设计图面。

4. 为“颜色常量”  节点指定颜色值。 使用“选择”  工具选择“颜色常量”  节点，然后在“属性”  窗口的“输出”  属性中指定颜色值。 为橙色指定 (1.0, 0.5, 0.2, 1.0) 中的值。

5. 将颜色常量连接到最终颜色。 若要创建连接，请将“颜色常量”  节点的“RGB”  终端移到“最终颜色”  节点的“RGB”  终端，然后将“颜色常量”  节点的“Alpha”  终端移到“最终颜色”  节点的“Alpha”  终端。 这些连接将最终颜色设置为上一步中定义的颜色常量。

下图显示了已完成的着色器关系图和应用于立方体的着色器预览。

> [!NOTE]
> 在图中，指定橙色以更好地展示着色器的效果。

![三维模型上的着色器图及其结果](../designers/media/digit-flat-color-effect.png)

某些形状可能会增强某些着色器的预览效果。 若要深入了解如何在着色器设计器中预览着色器，请参阅[着色器设计器](../designers/shader-designer.md)。

## <a name="see-also"></a>请参阅

- [如何：向三维模型应用着色器](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [如何：导出着色器](../designers/how-to-export-a-shader.md)
- [着色器设计器](../designers/shader-designer.md)
- [着色器设计器节点](../designers/shader-designer-nodes.md)
