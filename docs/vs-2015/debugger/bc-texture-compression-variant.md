---
title: BC 纹理压缩变量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 2d0f5305-585b-4b01-bc9a-7a32d6e991da
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f0758d9eb5a003b0353ceb4fee21996d90685fa5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161693"
---
# <a name="bc-texture-compression-variant"></a>BC 纹理压缩变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对采用像素格式（B8G8R8X8、B8G8R8A8 或 R8G8B8A8 的变体）的纹理启用块压缩。  
  
## <a name="interpretation"></a>解释  
 基于块的压缩格式（例如 BC1、BC2 和 BC3）将比未压缩的图像格式占用明显更少的内存，因此也将消耗明显更少的内存带宽。 与使用 32 位/像素的未压缩格式相比，BC1（以前称为 DXT1）将达到 8:1 的压缩比，BC3（以前称为 DXT5）将达到 4:1 的压缩比。 BC1 和 BC3 之间的差异是，BC1 不支持 alpha 通道，而 BC3 支持块压缩的 alpha 通道。 不管高压缩比如何，典型纹理的图像质量仅发生了小幅下降。 但是，某些类型的纹理（例如，在较小区域中具有明显颜色变化的纹理）的块压缩可能会产生不可接受的结果。  
  
 如果你的纹理适用于基于块的压缩且无需完美的色彩保真度，请考虑使用块压缩格式，以便减少内存使用和消耗较少的带宽。  
  
## <a name="remarks"></a>备注  
 每次调用创建源纹理的 `ID3DDevice::CreateTexture2D` 时，你都可以通过使用基于块的压缩格式来压缩纹理。 具体而言，在以下情况下会压缩纹理：  
  
- 在 `D3D11_TEXTURE2D_DESC` 中传递的 `pDesc` 对象描述了不变的着色器资源；即：  
  
  - BindFlags 成员仅设置 D3D11_BIND_SHADER_RESOURCE 标志。  
  
  - 将 Usage 成员设置为 D3D11_USAGE_DEFAULT 或 D3D11_USAGE_IMMUTABLE。  
  
  - 将 CPUAccessFlags 成员设置为 0（无 CPU 访问）。  
  
  - SamplerDesc 成员将其 Count 成员设置为 1（不支持多重采样抗锯齿 (MSAA)）。  
  
- 为对 `CreateTexture2D` 的调用提供了初始数据。  
  
  以下是支持的源格式及其块压缩的格式。  
  
|原始格式（源格式）|压缩格式（目标格式）|  
|------------------------------|------------------------------|  
|`DXGI_FORMAT_B8G8R8X8_UNORM`|BC1（以前称为 DXT1）|  
|`DXGI_FORMAT_B8G8R8X8_UNORM_SRGB`|BC1|  
|`DXGI_FORMAT_B8G8R8X8_TYPELESS`|BC1|  
|`DXGI_FORMAT_B8G8R8A8_UNORM`|BC3（以前称为 DXT5）|  
|`DXGI_FORMAT_B8G8R8A8_UNORM_SRGB`|BC3|  
|`DXGI_FORMAT_B8G8R8A8_TYPELESS`|BC3|  
|`DXGI_FORMAT_R8G8B8A8_UNORM`|BC3|  
|`DXGI_FORMAT_R8G8B8A8_UNORM_SRGB`|BC3|  
|`DXGI_FORMAT_R8G8B8A8_TYPELESS`|BC3|  
  
 如果你的纹理具有未列出的格式，则该纹理未发生修改。  
  
## <a name="restrictions-and-limitations"></a>限制和约束  
 有时，采用 B8G8R8A8 或 R8G8B8A8 图像格式的变体创建的纹理实际上不会使用 alpha 通道，但是该变体无法知道是否使用了它。 为了保持正确性（如果使用了 alpha 通道），该变体始终将这些格式编码为效率较低的 BC3 格式。 当你未打算使用 alpha 通道时，通过使用 B8G8R8X8 图像格式的变体，可帮助“图形帧分析”更好地了解应用对此变体的潜在呈现性能，以便该变体可以使用效率更高的 BC1 格式。  
  
## <a name="example"></a>示例  
 此变量在运行时（调用 `CreateTexture2D` 之前）对纹理进行块压缩。 我们不建议将此方法用于成品代码，因为未压缩的纹理会消耗更多的磁盘空间，而且此额外步骤会显著增加应用中的加载次数（因为基于块的压缩需要大量计算要编码的资源）。 相反，我们建议你通过使用生成管道中包含的图像编辑器或图像处理器，在脱机状态下压缩纹理。 这些方法将降低磁盘空间要求、消除应用中的运行时开销并提供更多的处理时间，以便可以保持最佳图像质量。  
  
## <a name="see-also"></a>请参阅  
 [Half/Quarter 纹理维度变量](../debugger/half-quarter-texture-dimensions-variant.md)
