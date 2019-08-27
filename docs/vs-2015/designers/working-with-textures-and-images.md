---
title: 使用纹理和图像 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: b9fbc8fa-66d1-4055-8460-24d8b8fbe43e
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 89c8fd489c29fc9b352c34011349ff447e48adb4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690083"
---
# <a name="working-with-textures-and-images"></a>使用纹理和图像
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中使用图像编辑器来创建和修改纹理和图像。 如同用 DirectX 应用程序开发的应用程序一样，图像编辑器支持丰富的纹理和图像格式。  
  
> [!NOTE]
> 图像编辑器不支持低色彩图像，例如图标或光标。 若要创建或修改这种图像，请使用[适用于图标的图像编辑器](https://msdn.microsoft.com/library/586d2b8b-0348-4883-a85d-1ff0ddbf14dd)。  
  
## <a name="textures-and-images"></a>纹理和图像  
 简单地说，纹理和图像只是用于在图形应用中提供可视细节的数据表。 纹理或图像提供的细节取决于其用法，颜色样本、Alpha（透明度）值、法线与高度值是常见的示例。 纹理与图像之间的主要差别在于，前者连同形状的表示形式（通常是 3D 模型）来呈现整个对象或场景，而图像通常是对象或场景的独立表示形式。  
  
 纹理的常见类型包括：  
  
 纹理图  
 纹理图包含已组织成一维、二维或三维矩阵的颜色值。 它们用于针对受影响的对象提供颜色细节。 颜色一般使用 RGB（红、绿、蓝）颜色通道来编码，可能包含表示透明度的第四个通道，即 Alpha。 较不常见的情况是，颜色可能以其他颜色方案来编码，或者第四个通道可能包含 Alpha 以外的数据，例如高度。  
  
 法线图  
 法线图包含曲面法线。 它们用于针对受影响的对象提供照明细节。 法线通常使用红、绿、蓝分量进行编码，以存储向量的 x、y 和 z 维。 但是，还有其他编码 - 例如，基于极坐标的编码。  
  
 高度图  
 高度图包含高度字段数据。 它们用于针对受影响的对象提供几何细节 - 使用着色器代码计算所需的效果 - 或者提供用例的数据点，例如地形生成。 高度值通常使用纹理中的一个通道进行编码。  
  
 立方体图  
 立方体图可能包含不同类型的数据（例如，颜色或法线），但是已在立方体的表面组织成六个纹理。 因此，对立方体图进行采样的方式不是通过提供纹理坐标，而是提供原点在立方体中心的向量；样本是取自向量与立方体交集的点。 使用立方体图可以提供用于计算反射的环境近似值（称为 *环境映射*），或者提供失真度比基本、二维纹理低的纹理给球面对象。  
  
 可以通过与纹理包含的数据类型或者与纹理维度或“形状”正交的方法来编码和压缩任何纹理。 但是，不同的编码和压缩方法可为不同类型的数据产生更好的效果。  
  
 你可以使用图像编辑器来创建和修改纹理和图像，就像使用其他图像编辑器一样。 图像编辑器还提供用于处理 3D 图形的 mipmap 及其他功能，并支持 DirectX 所能支持的许多高度压缩与硬件加速的纹理格式。  
  
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|-----------|-----------------|  
|[图像编辑器](../designers/image-editor.md)|介绍如何使用图像编辑器处理纹理和图像。|  
|[图像编辑器示例](../designers/image-editor-examples.md)|提供演示如何使用图像编辑器执行常见图像处理任务的主题的链接。|
