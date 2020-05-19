---
title: 16bpp 呈现器目标格式变体 | Microsoft Docs
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2019
ms.locfileid: "74188594"
---
# <a name="16-bpp-render-target-format-variant"></a>16 bpp 呈现器目标格式变体
将所有呈现器目标和后台缓冲区的像素格式设置为 DXGI_FORMAT_B5G6R5_UNORM。

## <a name="interpretation"></a>解释
 呈现器目标或后台缓冲区通常使用 32 bpp（32 位/像素）格式，例如 B8G8R8A8_UNORM。 32-bpp 格式可能消耗大量内存带宽。 由于 B5G6R5_UNORM 格式是 16-bpp 格式，它的大小是 32-bpp 格式大小的一半，因此使用它可以减轻内存带宽上的压力，但是会以降低色彩保真度为代价。

 如果此变体显示较大的性能提升，则可能表示你的应用消耗了太多内存带宽。 你可以获得显著的性能提升，尤其是在所分析的帧具有大量过度绘制或 alpha 值混合处理时。

当应用程序符合以下条件时，16-bpp 呈现器目标格式可以减少内存带宽使用量：
- 不需要高保真度色彩重现。
- 不需要 alpha 通道。
- 不会经常包含平滑渐变（在降低的色彩保真度下容易出现带状干扰问题）。

其他减少内存带宽的策略包括：
- 减少过度绘制量或 alpha 值混合处理。
- 缩小帧缓冲区的尺寸。
- 缩小纹理资源的尺寸。
- 减少纹理资源的压缩。

你必须照常考虑所有这些优化随附的图像质量利弊。

属于交换链一部分的应用程序采用不支持 16 bpp 的后台缓冲区格式 (DXGI_FORMAT_B5G6R5_UNORM)。 这些交换链是使用 `D3D11CreateDeviceAndSwapChain` 或 `IDXGIFactory::CreateSwapChain` 创建的。 若要解决此限制，请执行以下步骤：
1. 使用 `CreateTexture2D` 创建 B5G6R5_UNORM 格式的呈现器目标并呈现到该目标。
2. 通过将呈现器目标用作源纹理来绘制全屏的四个部分，将该呈现器目标复制到交换链后台缓冲区上。
3. 在交换链上调用 Present。

   如果与将呈现器目标复制到交换链后台缓冲区所消耗的带宽相比，此策略节省了更多带宽，则呈现性能将得到提升。

   通过使用 16 bpp 帧缓冲区格式，使用磁贴呈现技术的 GPU 体系结构可以获得显著的性能提升。 这种提升是因为每个磁贴的本地帧缓冲区缓存能够容纳更大一部分帧缓冲区。 有时会在手机和 Tablet 计算机的 GPU 中找到磁贴呈现体系结构；它们极少出现在此适当位置以外。

## <a name="remarks"></a>备注
 每次调用创建呈现器目标的 `ID3D11Device::CreateTexture2D` 时，呈现器目标格式都将重置为 DXGI_FORMAT_B5G6R5_UNORM。 具体而言，当在 pDesc 中传递的 D3D11_TEXTURE2D_DESC 对象描述呈现器目标时将重写该格式；即：

- BindFlags 成员将设置 D3D11_BIND_REDNER_TARGET 标志。

- BindFlags 成员将清除 D3D11_BIND_DEPTH_STENCIL 标志。

- 将 Usage 成员设置为 D3D11_USAGE_DEFAULT。

## <a name="restrictions-and-limitations"></a>限制和约束
 因为 B5G6R5 格式不具有 alpha 通道，所以此变体不会保留 alpha 内容。 如果应用的呈现要求在呈现器目标中使用 alpha 通道，则不能够仅切换到 B5G6R5 格式。

## <a name="example"></a>示例
 通过使用如下代码，可为使用 `CreateTexture2D` 创建的呈现器目标重现 16 bpp 呈现器目标格式变体：

```cpp
D3D11_TEXTURE2D_DESC target_description;

target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```
