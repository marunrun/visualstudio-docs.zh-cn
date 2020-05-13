---
title: 处理游戏和应用的三维资产
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics
ms.assetid: 910d673b-c884-4eeb-9928-0e89f3d38cb6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aa9fc04df3e817730492353e54d74c1e46c3775e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589794"
---
# <a name="work-with-3d-assets-for-games-and-apps"></a>处理游戏和应用的 3D 资产

本文介绍 Visual Studio 工具，用于创建或修改基于 DirectX 的游戏和应用的三维模型、纹理和着色器。

## <a name="directx-app-development-in-visual-studio"></a>Visual Studio 中的 DirectX 应用开发

DirectX 应用通常将编程逻辑、DirectX API、高级别着色语言 (HLSL) 程序与音频和三维可视化资产合并在一起，以提供丰富的交互式多媒体体验。 Visual Studio 包括可用于处理图像和纹理、三维模型和着色器的工具，无需离开 IDE 使用其他工具。 Visual Studio 工具尤其适用于创建占位符资产，该资产可用于添加生产就绪资产前测试代码或生成原型，还可用于调试应用前，检查和修改生产就绪资产  。

以下是关于可在 Visual Studio 中处理的各种资产的详细信息。

### <a name="images-and-textures"></a>图像和纹理

图像和纹理能够在游戏和应用中提供颜色和可视化细节。 在三维图中，纹理具有多种格式、类型和几何形状，以满足不同用途。 例如，法线贴图提供每像素曲面法线以实现更具体的三维模型照明，多维数据集映射提供所有方向的纹理以用于 sky-boxing、反射和球面纹理映射等。 纹理可以提供 mipmap，支持不同级别细节的高效绘制，且支持不同的颜色通道和颜色排序。 纹理可以各种压缩格式存储，从而减少专用图形内存占用，有助于 GPU 更有效地访问纹理。

可以使用 Visual Studio 图像编辑器处理许多常用类型和格式的图像和纹理。

### <a name="3d-models"></a>三维模型

三维模型创建游戏和应用中的空间和形状。 按最小的方式，模型将三维空间中点的位置（称为顶点）和索引数据一起编码，以定义表示模型形状的线或三角形  。 其他可以与这些顶点关联的数据，例如：颜色信息、常规矢量或应用程序特定的属性。 每个模型还可以定义对象范围的属性，例如，哪一个着色器用于计算对象图面的外观，哪一个纹理应用于它。

使用 Visual Studio 模型编辑器可以处理多种常用格式的三维模型。

### <a name="shaders"></a>着色器

着色器是在图形处理单元 (GPU) 上运行的特定于域的小型程序。 着色器确定三维模型转换为屏幕形状的方式，以及这些形状中的每个像素的着色方式。 通过创建着色器并将它应用到游戏或应用中的对象，可以为该对象提供唯一外观。

可以使用 Visual Studio 着色器设计器，它是一个基于图形的着色器设计工具，用户可以在不懂 HLSL 编程的情况下创建自定义可视化效果。

> [!NOTE]
> 有关如何开始 DirectX 编程的详细信息，请参阅 [DirectX](/windows/win32/directx)。 有关如何调试基于 DirectX 的应用的详细信息，请参阅[图形诊断（调试 DirectX 图形）](../debugger/graphics/visual-studio-graphics-diagnostics.md)。

## <a name="directx-version-compatibility"></a>DirectX 版本兼容性

Visual Studio 使用 DirectX 呈现二维和三维资产。 可以选择 DirectX 11 呈现器或 Windows 高级光栅化平台 (WARP) 软件呈现器。 DirectX 11 呈现器在 DirectX 11 和 DirectX 10 GPU 上提供高性能、硬件加速呈现。 WARP 呈现器有助于确保资产适用于一系列计算机，其中包括没有新式图形硬件的计算机和具有集成图形硬件的计算机。 有关 WARP 的详细信息，请参阅 [Windows 高级光栅化平台 (WARP) 指南](/windows/win32/direct3darticles/directx-warp)。

## <a name="related-topics"></a>相关主题

|标题|说明|
|-----------|-----------------|
|[使用纹理和图像](../designers/working-with-textures-and-images.md)|介绍如何使用 Visual Studio 处理图像和纹理。|
|[使用三维模型](../designers/working-with-3-d-models.md)|介绍如何使用 Visual Studio 处理三维模型。|
|[使用着色器](../designers/working-with-shaders.md)|介绍如何使用 Visual Studio 着色器设计器创建和修改自定义着色器效果。|
|[在游戏或应用中使用三维资产](../designers/using-3-d-assets-in-your-game-or-app.md)|介绍如何使用通过图像编辑器、模型编辑器或着色器设计器创建的游戏或应用中的资产。|
