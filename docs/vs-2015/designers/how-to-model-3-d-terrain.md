---
title: 如何：构建三维地形模型 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: f779b1fd-82a9-4a11-8ab7-c1c9caabc883
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ab202ed97ce2056313eb661d51d7150bb9689829
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72664411"
---
# <a name="how-to-model-3-d-terrain"></a>如何：构建三维地形模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本文档说明如何使用模型编辑器创建三维地形模型。

 本文档演示了这些活动：

- 将对象添加到场景中

- 选择面和点

- 转换选定内容

- 使用“细分面”**** 工具

- 在设计图面中为对象添加框架

## <a name="creating-a-3-d-terrain-model"></a>创建三维地形模型
 细分平面以创建其他的面，然后对其顶点进行处理以创建有趣的地形特征，借此以创建三维地形。

 完成后，模型应类似于：

 ![3&#45;显示地形模型的 D 场景](../designers/media/digit-terrain-model.png "数字地形-模型")

 开始前，请确保显示“属性”**** 窗口和“工具箱”****。

#### <a name="to-create-a-3-d-terrain-model"></a>创建三维地形模型

1. 创建要使用的三维模型。 有关如何向项目添加模型的信息，请参阅 [模型编辑器](../designers/model-editor.md)中的入门部分。

2. 将平面添加到场景中。 在“工具箱”**** 中的“形状”**** 下，选择“平面”****，然后将其移到设计图面。

   > [!TIP]
   > 为了使平面对象更易于使用，可以在设计图面中对向其添加框架。 在“选择”**** 模式中，选择平面对象，然后在“模型编辑器”工具栏上，选择“框选对象”**** 按钮。

3. 进入面选择模式。 在“模型编辑器”工具栏上，选择“选择面”****。

4. 细分平面。 在面选择模式中，选择平面一次将其激活以供选择，然后再次选择它以仅选择其面。 在“模型编辑器”工具栏上，选择“细分面”****。 这会向平面添加新的顶点，这些顶点将平面拆分为四个大小相等的分区。

5. 创建更多细分面。 在选中新面的同时，再选择两次“细分面”****。 这总共将创建 64 个面。 通过创建更多的细分面，可让地形具有更多的细节。

6. 进入点选择模式。 在“模型编辑器”工具栏上，选择“选择点”****。

7. 修改点以创建地形特征。 在点选择模式中，选择其中一个点，然后在“模型编辑器”工具栏上选择“转换”**** 工具。 一个表示点的框显示在设计图面上。 使用绿色箭头移动框，从而修改点的高度。 对不同的点重复此步骤以创建有趣的地形特征。

   > [!TIP]
   > 可以一次性选择多个点以统一修改它们。

   地形模型已完成。 下面是应用了 Phong 着色的最终模型：

   ![3&#45;显示地形模型的 D 场景](../designers/media/digit-terrain-model.png "数字地形-模型")

   可以使用此地形模型演示[如何：创建基于几何图形的渐变着色器](../designers/how-to-create-a-geometry-based-gradient-shader.md)中所述的渐变着色器的效果。

## <a name="see-also"></a>另请参阅
 [模型编辑器](../designers/model-editor.md)
