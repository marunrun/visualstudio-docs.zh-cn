---
title: 绘制形状和路径
titleSuffix: Blend for Visual Studio
ms.date: 07/31/2019
ms.topic: conceptual
ms.assetid: d5378c59-e2e5-49f0-91f1-aa82d984a33c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 29c74f74bbee19e414b3ee32948f3ca5338e8d53
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "82921153"
---
# <a name="draw-shapes-and-paths"></a>绘制形状和路径

在 XAML 设计器中，“形状”** 正是你所期望的内容。 例如：矩形、圆或椭圆。 *路径* 是更加灵活的形状版本。 你可以执行某些操作，如重新调整它们的形状，或将它们合并在一起以形成新形状。

形状和路径使用矢量图形，因此它们可很好地按高分辨率显示进行缩放。

## <a name="draw-a-shape"></a>绘制形状

在“资产”**** 窗口中查找形状。

![“资产”窗口上的“形状”类别](media/blend-shapes.png)

将所需的任何形状拖到美工板上。 然后，使用形状的图柄缩放、旋转、移动或扭曲形状。

![控点](../designers/media/84261e83-3091-4490-ab58-4218b188439e.png)

## <a name="draw-a-path"></a>绘制路径

路径是一系列连接的直线和曲线。 使用路径可创建“资产”**** 窗口中未提供的有趣形状。

可以使用线条、笔或铅笔绘制路径。 可以在“工具”**** 窗口中找到这些工具。

### <a name="draw-a-straight-line"></a>绘制直线

使用“笔”**** 工具或“线条”**** 工具。

**使用“笔”工具**

在美工板上，单击一次以定义开始点，然后再次单击以定义线条末尾。

**使用“线条”工具**

在美工板上，从所需线条起始位置处拖动，然后在所需线条结束位置处释放。

### <a name="draw-a-curve"></a>绘制曲线

使用“笔”**** 工具。

在美工板上，单击一次以定义线条的起点，然后单击并拖动指针以创建所需的曲线。

如果要闭合路径，请单击线条上的第一个点。

### <a name="change-the-shape-of-a-curve"></a>更改曲线的形状

使用“路径选择”**** 工具。

单击形状，然后拖动形状上的任何点以更改曲线形状。

### <a name="draw-a-free-form-path"></a>绘制任意形状的路径

使用“铅笔”**** 工具。

在美工板上，如同使用真正的铅笔一样绘制任意形状的路径。

### <a name="remove-part-of-a-path"></a>删除路径的一部分

使用“路径选择”**** 工具。

选择包含要删除的段的路径，然后单击“删除” **** 按钮。

### <a name="remove-a-point-in-a-path"></a>删除路径中的点

使用“选择”**** 工具，以选中路径。 然后，使用 "**笔**" 工具单击你要删除的点。

### <a name="add-a-point-to-a-path"></a>向路径添加点

使用“选择”**** 工具，以选中路径。 使用 "**笔**" 工具单击路径上要添加点的任何位置。

## <a name="convert-a-shape-to-a-path"></a>将形状转换为路径

若要采用与修改路径相同的方式来修改形状，请将形状转换为路径。 选择形状，然后选择 "**格式化** > **路径** > " "**转换为路径**"。

**观看短片：** ![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.png) [使用路径：将形状转换为路径](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=147)。

> [!NOTE]
> ****“转换为路径”当前不适用于 `TargetPlatformVersion` 至少为 10.0.16299.0 或更高版本的 UWP 应用。

## <a name="combine-paths"></a>合并路径

可以将路径和形状合并到单个路径中。

![合并路径](../designers/media/2df17a5d-a338-4ef4-96c5-dae51cc1ca8a.png)

|||||
|-|-|-|-|
|![合并之前的两个形状](../designers/media/b1_1.png)|合并之前的两个形状|![Intersect](../designers/media/b1_4.png)|Intersect|
|![相并](../designers/media/b1_2.png)|相并|![相斥](../designers/media/b1_5.png)|排除重叠|
|![除](../designers/media/b1_3.png)|除|![减](../designers/media/b1_6.png)|减|

**观看短片：** ![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.png) [使用路径：合并路径](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=195)。

## <a name="create-a-compound-path"></a>创建复合路径

创建复合路径时，会从结果中减去路径的任何相交部分，生成的路径会采取最底部路径的视觉属性。

可以在创建之后随时分离复合路径。

![中断复合路径](../designers/media/2157a8aa-d9a7-4de4-8de5-b10d28f08a84.png)

**观看短片：** ![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.png) [使用路径：创建复合路径](https://www.youtube.com/watch?v=Io5bC0-nH6Q)。

## <a name="create-a-clipping-path"></a>创建剪切路径

剪切路径是应用于另一个对象的路径或形状，可隐藏遮蔽对象处于剪切路径之外的部分。

![剪切路径](../designers/media/22471e98-a841-4f39-a3ef-36090cf5a625.png)

**观看短片：** ![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.png) [使用路径：创建剪切路径](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=232)。
