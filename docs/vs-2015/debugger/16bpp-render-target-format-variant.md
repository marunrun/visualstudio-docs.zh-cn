---
title: 16bpp 呈现目标格式变量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7b315c7ab9bb10d039e81ba26b1beb9c4447a205
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157573"
---
# <a name="16bpp-render-target-format-variant"></a>16bpp 呈现目标格式变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将所有呈现器目标和后台缓冲区的像素格式设置为 DXGI_FORMAT_B5G6R5_UNORM。  
  
## <a name="interpretation"></a>解释  
 呈现器目标和后台缓冲区通常使用 32bpp（32 位/像素）格式，例如 B8G8R8A8_UNORM。 32bpp 格式可能消耗大量内存带宽。 因为 B5G6R5_UNORM 格式是 16bpp 格式，它的大小是 32bpp 格式大小的一半，因此使用它可以减轻内存带宽上的压力，但是会以降低色彩保真度为代价。  
  
 如果此变体显示较大的性能提升，则可能表示你的应用消耗了太多内存带宽。 当分析帧遇到大量过度绘制或包含许多 alpha 混合时，性能提升可能会格外明显。  
  
 如果你的应用所呈现的这些类场景不需要高保真度色彩重现、不需要呈现器目标具有 alpha 通道，并且不会经常包含平滑渐变（在降低的色彩保真度下容易出现带状干扰问题），则请考虑使用 16bpp 呈现器目标格式，以减少内存带宽使用量。  
  
 如果在你的应用中呈现的场景要求高保真度色彩重现或 alpha 通道，或经常包含平滑渐变，则请考虑使用其他策略减少内存带宽使用量，例如，减少过度绘制量或 alpha 混合、缩小帧缓冲区的尺寸，或者通过启用压缩或缩小其尺寸来修改纹理资源以消耗较少的内存带宽。 你必须照常考虑所有这些优化随附的图像质量利弊。  
  
 如果你的应用受益于切换到 16bpp 后台缓冲区，但是它是你的交换链的一部分，则你必须采用其他步骤，因为通过使用 `D3D11CreateDeviceAndSwapChain` 或 `IDXGIFactory::CreateSwapChain` 创建的交换链不支持 DXGI_FORMAT_B5G6R5_UNORM 后台缓冲区格式。 相反，你必须使用 `CreateTexture2D` 创建 B5G6R5_UNORM 格式的呈现器目标并呈现到该目标。 然后，在交换链上调用 Present 之前，通过将呈现器目标用作源纹理来绘制全屏的四个部分，将该呈现器目标复制到交换链后台缓冲区上。 虽然这是将消耗一些内存带宽的额外步骤，但是大多数呈现操作将消耗较少带宽，因为它们会影响 16bpp 呈现器目标；如果与通过将呈现器目标复制到交换链后台缓冲区所消耗的带宽相比，此步骤节省了更多带宽，则呈现性能得到了提高。  
  
 通过使用 16bpp 帧缓冲区格式，使用磁贴呈现技术的 GPU 体系结构可以获得显著的性能改进，因为更大一部分的帧缓冲区能够符合每个磁贴的本地帧缓冲区缓存。 有时会在手机和 Tablet 计算机的 GPU 中找到磁贴呈现体系结构；它们极少出现在此适当位置以外。  
  
## <a name="remarks"></a>备注  
 每次调用创建呈现器目标的 `ID3D11Device::CreateTexture2D` 时，呈现器目标格式都将重置为 DXGI_FORMAT_B5G6R5_UNORM。 具体而言，当在 pDesc 中传递的 D3D11_TEXTURE2D_DESC 对象描述呈现器目标时将重写该格式；即：  
  
- BindFlags 成员将设置 D3D11_BIND_REDNER_TARGET 标志。  
  
- BindFlags 成员将清除 D3D11_BIND_DEPTH_STENCIL 标志。  
  
- 将 Usage 成员设置为 D3D11_USAGE_DEFAULT。  
  
## <a name="restrictions-and-limitations"></a>限制和约束  
 因为 B5G6R5 格式不具有 alpha 通道，所以此变体不会保留 alpha 内容。 如果应用的呈现要求在呈现器目标中使用 alpha 通道，则不能够仅切换到 B5G6R5 格式。  
  
## <a name="example"></a>示例  
 **16bpp 呈现器目标格式**变体可以通过使用创建的呈现器目标重现`CreateTexture2D`通过使用如下代码：  
  
```  
D3D11_TEXTURE2D_DESC target_description;  
  
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;  
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;  
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);  
```
