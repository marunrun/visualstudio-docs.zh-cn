---
title: 16bpp Render Target Format Variant | Microsoft Docs
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
# <a name="16-bpp-render-target-format-variant"></a>16 bpp Render Target Format Variant
将所有呈现器目标和后台缓冲区的像素格式设置为 DXGI_FORMAT_B5G6R5_UNORM。

## <a name="interpretation"></a>解释
 A render target or back buffer typically uses a 32 bpp (32 bits per pixel) format such as B8G8R8A8_UNORM. 32-bpp formats can consume a large amount of memory bandwidth. Because the B5G6R5_UNORM format is a 16-bpp format that's half the size of 32-bpp formats, using it can relieve pressure on memory bandwidth, but at the cost of reduced color fidelity.

 如果此变体显示较大的性能提升，则可能表示你的应用消耗了太多内存带宽。 You can gain significant performance improvement, especially when the profiled frame had a significant amount of overdraw or alpha-blending.

A 16-bpp render target format can reduce memory band with usage when your application has the following conditions:
- Doesn't require high-fidelity color reproduction.
- Doesn't require an alpha channel.
- Doesn't often have smooth gradients (which are susceptible to banding artifacts under reduced color fidelity).

Other strategies to reduce memory bandwidth include:
- Reduce the amount of overdraw or alpha-blending.
- Reduce the dimensions of the frame buffer.
- Reduce dimensions of texture resources.
- Reduce compressions of texture resources.

你必须照常考虑所有这些优化随附的图像质量利弊。

Applications that are a part of a swap chain have a back buffer format (DXGI_FORMAT_B5G6R5_UNORM) that doesn't support 16 bpp. These swap chains are created by using `D3D11CreateDeviceAndSwapChain` or `IDXGIFactory::CreateSwapChain`. To work around this limitation, do the following steps:
1. Create a B5G6R5_UNORM format render target by using `CreateTexture2D` and render to that target.
2. Copy the render target onto the swap-chain backbuffer by drawing a full-screen quad with the render target as your source texture.
3. Call Present on your swap chain.

   If this strategy saves more bandwidth than is consumed by copying the render target to the swap-chain backbuffer, then rendering performance is improved.

   GPU architectures that use tiled rendering techniques can see significant performance benefits by using a 16 bpp frame buffer format. This improvement is because a larger portion of the frame buffer can fit in each tile's local frame buffer cache. 有时会在手机和 Tablet 计算机的 GPU 中找到磁贴呈现体系结构；它们极少出现在此适当位置以外。

## <a name="remarks"></a>备注
 每次调用创建呈现器目标的 `ID3D11Device::CreateTexture2D` 时，呈现器目标格式都将重置为 DXGI_FORMAT_B5G6R5_UNORM。 具体而言，当在 pDesc 中传递的 D3D11_TEXTURE2D_DESC 对象描述呈现器目标时将重写该格式；即：

- BindFlags 成员将设置 D3D11_BIND_REDNER_TARGET 标志。

- BindFlags 成员将清除 D3D11_BIND_DEPTH_STENCIL 标志。

- 将 Usage 成员设置为 D3D11_USAGE_DEFAULT。

## <a name="restrictions-and-limitations"></a>限制和约束
 因为 B5G6R5 格式不具有 alpha 通道，所以此变体不会保留 alpha 内容。 如果应用的呈现要求在呈现器目标中使用 alpha 通道，则不能够仅切换到 B5G6R5 格式。

## <a name="example"></a>示例
 The **16 bpp Render Target Format** variant can be reproduced for render targets created by using `CreateTexture2D` by using code like this:

```cpp
D3D11_TEXTURE2D_DESC target_description;

target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```
