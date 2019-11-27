---
title: 16bpp 呈现目标格式变量 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a63261a4ef8a6304bec8c2bdde1d9ec9113405e
ms.sourcegitcommit: 8530d15aa72fe058ee3a3b4714c36b8638f8b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2019
ms.locfileid: "74188594"
---
# <a name="16-bpp-render-target-format-variant"></a>16 bpp 呈现器目标格式变量
将所有呈现器目标和后台缓冲区的像素格式设置为 DXGI_FORMAT_B5G6R5_UNORM。

## <a name="interpretation"></a>解释
 呈现器目标或后台缓冲区通常使用 32 bpp （32位/像素）格式，如 B8G8R8A8_UNORM。 32-bpp 格式会消耗大量内存带宽。 由于 B5G6R5_UNORM 格式是 16 bpp 格式，这是 32-bpp 格式的一半，因此使用它可以减轻内存带宽压力，但代价是降低了颜色保真度。

 如果此变体显示较大的性能提升，则可能表示你的应用消耗了太多内存带宽。 您可以显著提高性能，尤其是在所分析的帧具有大量过度绘制或 alpha 混合时。

当你的应用程序具有以下条件时，16 bpp 呈现目标格式可以减少内存带的使用情况：
- 不需要高保真色。
- 不需要 alpha 通道。
- 通常不具有平滑渐变（这在降低颜色保真下很容易受到条纹项目的过渡）。

降低内存带宽的其他策略包括：
- 减少过度绘制或 alpha 混合量。
- 减小帧缓冲区的尺寸。
- 减少纹理资源的尺寸。
- 减少纹理资源的压缩。

你必须照常考虑所有这些优化随附的图像质量利弊。

作为交换链一部分的应用程序具有不支持 16 bpp 的后台缓冲区格式（DXGI_FORMAT_B5G6R5_UNORM）。 这些交换链是使用 `D3D11CreateDeviceAndSwapChain` 或 `IDXGIFactory::CreateSwapChain`创建的。 若要解决此限制，请执行以下步骤：
1. 使用 `CreateTexture2D` 并呈现到该目标，创建 B5G6R5_UNORM 格式呈现目标。
2. 将呈现器目标作为源纹理绘制到呈现目标，从而将呈现器目标复制到交换链后台缓冲区。
3. 在交换链上调用。

   如果此策略通过将呈现器目标复制到交换链后台缓冲区来节省比使用的带宽更多的带宽，则改善呈现性能。

   使用平铺呈现技术的 GPU 体系结构可以使用 16 bpp 帧缓冲格式来查看显著的性能优势。 此改进是因为帧缓冲区中的更大部分可以适合每个磁贴的本地帧缓冲区缓存。 有时会在手机和 Tablet 计算机的 GPU 中找到磁贴呈现体系结构；它们极少出现在此适当位置以外。

## <a name="remarks"></a>备注
 每次调用创建呈现器目标的 `ID3D11Device::CreateTexture2D` 时，呈现器目标格式都将重置为 DXGI_FORMAT_B5G6R5_UNORM。 具体而言，当在 pDesc 中传递的 D3D11_TEXTURE2D_DESC 对象描述呈现器目标时将重写该格式；即：

- BindFlags 成员将设置 D3D11_BIND_REDNER_TARGET 标志。

- BindFlags 成员将清除 D3D11_BIND_DEPTH_STENCIL 标志。

- 将 Usage 成员设置为 D3D11_USAGE_DEFAULT。

## <a name="restrictions-and-limitations"></a>限制和约束
 因为 B5G6R5 格式不具有 alpha 通道，所以此变体不会保留 alpha 内容。 如果应用的呈现要求在呈现器目标中使用 alpha 通道，则不能够仅切换到 B5G6R5 格式。

## <a name="example"></a>示例
 使用如下所示的代码，可以为使用 `CreateTexture2D` 创建的呈现目标重新生成**16 Bpp 呈现目标格式**变量：

```cpp
D3D11_TEXTURE2D_DESC target_description;

target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```
