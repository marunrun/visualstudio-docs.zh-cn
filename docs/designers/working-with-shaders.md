---
title: 使用着色器
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 6b2ea1ed-b995-4e75-af19-c68fd37a3bc5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1f07b293447a10a7d39e24ef42b1faedc27c7d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892398"
---
# <a name="work-with-shaders"></a>使用着色器

可以使用 Visual Studio 中基于图形的着色器设计器来设计自定义着色器效果。 可以在基于 DirectX 的游戏或应用中使用这些着色器。

## <a name="shaders"></a>着色器

着色器是一种执行图形计算（例如顶点转换或像素着色）的计算机程序，并且通常在图形处理单元 (GPU) 上运行，而不是在 CPU 上运行。 因为现在大多数传统、固定功能图形管道的阶段是由着色器程序来执行，因此可以使用它们来创建特定于应用需求的管道。

最常见类型的着色器是顶点着色器和像素着色器；前者执行每顶点计算并替换不可编程的图形硬件中的固定功能转换和照明电路，后者执行确定像素颜色的每像素计算，并替换不可编程的图形硬件中的固定功能颜色组合器电路。 现代图形硬件使更多类型的着色器成为了可能 - 用于图形计算的外壳着色器、域着色器和几何着色器，以及用于非图形计算的计算着色器。 在这些阶段中，甚至没有一个阶段在不可编程的图形硬件中可用。 着色器最初是通过使用提供数据并行 (SIMD) 和以图形为中心的 (点积) 指令的类似汇编语言所创建的。 现在，着色器通常是通过使用类似于 C 的高级别语言所创建的，如 HLSL（高级着色器语言）。

可以使用着色器设计器以交互方式创建像素着色器，而不是通过输入和编译代码进行创建。 在着色器设计器中，着色器是由代表数据和操作的大量节点以及代表通过着色器流动的数据值和中间结果的节点之间的连接所定义的。 通过使用此方法和着色器设计器中的实时预览，可以更轻松地可视化着色器的执行并通过试验“发现”有趣的着色器变体。

## <a name="dgsl-documents"></a>DGSL 文档

着色器设计器以有向图着色器语言 (DGSL) 格式保存着色器，该格式是一种基于有向图标记语言 (DGML) 的 XML 格式。 可以在模型编辑器中直接对 3D 模型应用 DGSL 着色器。 但是，在应用中使用 DGSL 着色器之前，必须将其导出为 DirectX 理解的格式（例如 HLSL）。

由于 DGSL 与 DGML 兼容，因此可以使用旨在分析 DGML 文档的工具来分析 DGSL 着色器。 有关 DGML 的信息，请参阅[了解有向图形标记语言 (DGML)](../modeling/customize-code-maps-by-editing-the-dgml-files.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[着色器设计器](../designers/shader-designer.md)|描述如何使用 Visual Studio 着色器设计器处理着色器。|
|[着色器设计器节点](../designers/shader-designer-nodes.md)|讨论可用于实现图形效果的着色器设计器节点的种类。|
|[着色器设计器示例](../designers/shader-designer-examples.md)|提供转至演示如何使用着色器设计器来实现常见图形效果的主题的链接。|