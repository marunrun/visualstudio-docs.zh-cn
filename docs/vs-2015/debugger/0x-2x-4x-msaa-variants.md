---
title: 0 x-2 x-4 msaa 变量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 668a6603-5082-4c78-98e6-f3dc871aa55b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f6cc62e4ba56cb7be461bbf3cee5435cb404b7fe
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439977"
---
# <a name="0x2x4x-msaa-variants"></a>0x/2x/4x MSAA 变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重写所有呈现器目标和交换链上的多重采样抗锯齿 (MSAA) 设置。  
  
## <a name="interpretation"></a>解释  
 通过在每个像素中的多个位置上进行采样，多重采样抗锯齿提高了视觉质量；MSAA 级别越高，采样越多，如果不使用 MSAA，则仅会从像素中心中采取一个样本。 在应用中启用 MSAA 通常会产生适度但可注意到的呈现性能开销，但是在某些工作负荷下或某些 GPU 上，它可能几乎不会产生任何影响。  
  
 如果你的应用已启用 MSAA，则较小的 MSAA 变体指示更高级别现有 MSAA 导致的相对性能开销。 具体来说，0x MSAA 变体指示在不使用 MSAA 时应用的相对性能。  
  
 如果你的应用尚未启用 MSAA，则 2x MSAA 和 4x MSAA 变体指示在应用中启用它们后的相对性能开销。 当开销处于可接受的低水平时，请考虑启用 MSAA 以增强应用的图像质量。  
  
> [!NOTE]
> 你的硬件可能无法针对所有格式完全支持 MSAA。 如果任何变体遇到无法解决的硬件限制问题，则在性能摘要表中它的列将为空白，并且会产生一条错误消息。  
  
## <a name="remarks"></a>备注  
 调用创建呈现器目标的 `ID3DDevice::CreateTexture2D` 时，这些变体将重写样本计数和 sample-quality 自变量。 具体而言，在以下情况下将重写这些参数：  
  
- 在 `D3D11_TEXTURE2D_DESC` 中传入的 `pDesc` 对象描述呈现器目标；即：  
  
  - BindFlags 成员设置 D3D11_BIND_TARGET 标志或 D3D11_BIND_DEPTH_STENCIL 标志。  
  
  - 将 Usage 成员设置为 D3D11_USAGE_DEFAULT。  
  
  - 将 CPUAccessFlags 成员设置为 0。  
  
  - 将 MipLevels 成员设置为 1。  
  
- 设备支持请求的呈现器目标格式（D3D11_TEXTURE2D_DESC::Format 成员）的请求样本计数（0、2 或 4）和样本质量 (0)，由 `ID3D11Device::CheckMultisampleQualityLevels` 确定。  
  
  如果 D3D11_TEXTURE2D_DESC::BindFlags 成员设置了 D3D_BIND_SHADER_RESOURCE 或 D3D11_BIND_UNORDERED_ACCESS 标志，则将创建两个版本的纹理；第一个版本将清除这些标志以用作呈现器目标，另一个版本是使这些标志保持不变以充当第一个版本的解析缓冲区的非 MSAA 纹理。 这是有必要的，因为将 MSAA 纹理用作着色器资源或用于无序访问可能无效，例如，充当它的着色器可能会产生不正确的结果，因为它会需要非 MSAA 纹理。 如果变体创建了辅助的非 MSAA 纹理，则无论何时从设备上下文中取消设置 MSAA 呈现器目标，其内容都将解析为非 MSAA 纹理。 同理，无论何时 MSAA 呈现器目标应绑定为着色器资源，或在无序访问视图中使用，都将绑定解析的非 MSAA 纹理。  
  
  这些变体还将重写通过使用 `IDXGIFactory::CreateSwapChain`、`IDXGIFactory2::CreateSwapChainForHwnd`、`IDXGIFactory2::CreateSwapChainForCoreWindow`、`IDXGIFactory2::CreateSwapChainForComposition` 和 `ID3D11CreateDeviceAndSwapChain` 创建的所有交换链上的 MSAA 设置。  
  
  这些更改的实际影响是，针对 MSAA 呈现器目标完成所有呈现，但是如果你的应用程序将其中一个呈现器目标或交换链缓冲区用作着色器资源视图或无序访问视图，则将从解析的呈现器目标的非 MSAA 副本中对数据进行采样。  
  
## <a name="restrictions-and-limitations"></a>限制和约束  
 在 Direct3D11 中，MSAA 纹理比非 MSAA 纹理更受限制。 例如，你无法在 MSAA 纹理上调用 `ID3D11DeviceContext::UpdateSubresource`，而且如果源资源和目标资源的样本计数和样本质量不匹配，则调用 `ID3D11DeviceContext::CopySubresourceRegion` 会失败，当此变体重写一种资源而非另一种资源的 MSAA 设置时，可能会发生这种情况。  
  
 当播放检测到这些种类的冲突时，它将尽最大努力尝试复制所需的行为，但是它可能无法准确匹配其结果。 虽然这种情况以歪曲这些变体的作用的方式影响变体性能并不常见，但是它是可能发生的（例如，像素着色器中的流控制由纹理的准确内容确定时），因为复制的纹理包含的内容可能不一致。  
  
## <a name="example"></a>示例  
 对于使用 `ID3D11Device::CreateTexture2D` 创建的呈现器目标，可通过使用如下代码重现这些变体：  
  
```  
D3D11_TEXTURE2D_DESC target_description;  
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;  
target_description.SampleDesc.Count = 4; // 4x MSAA, can be 2 or 0 instead  
target_description.SampleDesc.Quality = 0;  
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);  
```  
  
## <a name="example"></a>示例  
 或者，对于使用 IDXGISwapChain::CreateSwapChain 或 D3D11CreateDeviceAndSwapChain 创建的交换链，可使用如下代码执行此操作：  
  
```  
DXGI_SWAP_CHAIN_DESC chain_description;  
chain_description.SampleDesc.Count = 4; // 4x MSAA, can be 2 or 0 instead  
chain_description.SampleDesc.Quality = 0;  
  
// Call IDXGISwapChain::CreateSwapChain or D3D11CreateDeviceAndSwapChain, etc.  
```
