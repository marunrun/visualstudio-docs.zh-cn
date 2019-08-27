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
ms.openlocfilehash: 94775b717a3095d54d3fa52e3d2a5325dc3d21c5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896418"
---
# <a name="16-bpp-render-target-format-variant"></a>16 bpp 呈现目标格式变体
将所有呈现器目标和后台缓冲区的像素格式设置为 DXGI_FORMAT_B5G6R5_UNORM。

## <a name="interpretation"></a>解释
 呈现器目标和后台缓冲区通常使用 32 bpp （32 位 / 像素） 格式，例如 B8G8R8A8_UNORM。 32 bpp 格式可能消耗大量的内存带宽。 因为 B5G6R5_UNORM 格式是为 32 bpp 格式的一半大小的 16 bpp 格式，则使用它可以减轻内存带宽，但代价是会降低的色彩保真度的压力。

 如果此变体显示较大的性能提升，则可能表示你的应用消耗了太多内存带宽。 可以获得显著的性能改善，尤其是当分析的帧具有大量过度绘制或 alpha 值混合处理。

16-bpp 呈现器目标格式可以减少使用的内存外时你的应用程序需满足以下条件：
- 不需要高保真度色彩重现。
- 不需要 alpha 通道。
- Ofent 没有平滑渐变 （的易受降低的色彩保真度下具有带区项目）。

若要减少内存带宽其他策略包括：
- 减少过度绘制量或 alpha 值混合处理。
- 减小帧缓冲区的尺寸。
- 减少纹理资源的维度。
- 减少纹理资源的压缩的文档。

你必须照常考虑所有这些优化随附的图像质量利弊。

是一个交换链的一部分的应用程序具有不支持 16 bpp 的后台缓冲区格式 (DXGI_FORMAT_B5G6R5_UNORM)。 通过使用创建这些交换链`D3D11CreateDeviceAndSwapChain`或`IDXGIFactory::CreateSwapChain`。 若要解决此限制，请执行以下步骤：
1. 使用创建 B5G6R5_UNORM 格式呈现器目标`CreateTexture2D`并呈现到该目标。
2. 通过绘制与呈现器目标用作源纹理的全屏四核，将复制到交换链后台缓冲区上的呈现器目标。
3. 在交换链上调用 Present。

   如果此策略将保存不是通过将呈现器目标复制到交换链后台缓冲区占用更多带宽，则会提高呈现性能。

   使用呈现技术的 GPU 体系结构可以通过使用 16 bpp 帧缓冲区格式看到显著的性能优势。 此项改进是因为较大一部分的帧缓冲区能够符合每个磁贴的本地帧缓冲区高速缓存。 有时会在手机和 Tablet 计算机的 GPU 中找到磁贴呈现体系结构；它们极少出现在此适当位置以外。

## <a name="remarks"></a>备注
 每次调用创建呈现器目标的 `ID3D11Device::CreateTexture2D` 时，呈现器目标格式都将重置为 DXGI_FORMAT_B5G6R5_UNORM。 具体而言，当在 pDesc 中传递的 D3D11_TEXTURE2D_DESC 对象描述呈现器目标时将重写该格式；即：

- BindFlags 成员将设置 D3D11_BIND_REDNER_TARGET 标志。

- BindFlags 成员将清除 D3D11_BIND_DEPTH_STENCIL 标志。

- 将 Usage 成员设置为 D3D11_USAGE_DEFAULT。

## <a name="restrictions-and-limitations"></a>限制和约束
 因为 B5G6R5 格式不具有 alpha 通道，所以此变体不会保留 alpha 内容。 如果应用的呈现要求在呈现器目标中使用 alpha 通道，则不能够仅切换到 B5G6R5 格式。

## <a name="example"></a>示例
 **16 bpp 呈现器目标格式**变体可以通过使用创建的呈现器目标重现`CreateTexture2D`通过使用如下代码：

```cpp
D3D11_TEXTURE2D_DESC target_description;

target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```
