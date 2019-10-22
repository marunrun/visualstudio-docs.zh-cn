---
title: 半季度纹理维度变量 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 282e9bbb-51aa-4cd0-8e5c-0901268c29e5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 620300d1727adc41d5655bd33dde87ad592bba1c
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71252978"
---
# <a name="halfquarter-texture-dimensions-variant"></a>Half/Quarter 纹理维度变量
减小非呈现器目标的纹理上的纹理尺寸。

## <a name="interpretation"></a>解释
 较小的纹理占用较少内存，因此将消耗较少的内存带宽，并且可减轻 GPU 的纹理缓存上的压力。 但是，由于其细节较少可能会导致图像质量降低，在三维场景中或放大情况下仔细观察它们时尤为明显。

 如果此变体显示较大的性能提升，则可能表示你的应用消耗了太多内存带宽或使用了效率低下的纹理缓存，或者两者都有。 也可能表示可供你的纹理占用的 GPU 内存不足，这会导致纹理将分页到系统内存。

 如果你的应用消耗了太多内存带宽，或使用了效率低下的纹理缓存，请考虑减少你的纹理的大小（仅在你考虑了为相应纹理启用 Mip 贴图之后执行此操作）。 与较小的纹理相同，进行了 Mip 贴图的纹理将消耗较少的内存带宽（即使它们将占用更多 GPU 内存）并提高缓存使用率，但是它们不会减少纹理细节。 建议在任何增加的内存使用不会导致纹理分页到系统内存的情况下，使用 Mip 贴图。

 如果可供你的纹理占用的 GPU 内存不足，请考虑减小这些纹理的大小（仅在你考虑了压缩相应的纹理之后执行此操作）。 与较小的纹理相同，压缩的纹理将占用较少内存并降低分页到系统内存的需要，但却降低了它们的色彩保真度。 根据纹理的内容（例如，在较小区域中具有明显色彩变体的纹理），压缩并不适用于所有纹理，但是对于很多纹理而言，相比减小其大小，压缩可以更好地保留整体图像质量。

## <a name="remarks"></a>备注
 每次调用创建源纹理的 `ID3D11Device::CreateTexture2D` 时，纹理尺寸都将减小。 具体而言，当在 `pDesc` 中传递的 D3D11_TEXTURE2D_DESC 对象描述在呈现中使用的纹理时，纹理尺寸将减小；即：

- BindFlags 成员仅设置 D3D11_BIND_SHADER_RESOURCE 标志。

- MiscFlags 成员未设置 D3D11_RESOURCE_MISC_TILE_POOL 标志或 D3D11_RESOURCE_MISC_TILED 标志（未调整磁贴资源大小）。

- 纹理格式作为呈现器目标受支持（由 D3D11_FORMAT_SUPPORT_RENDER_TARGET 确定），减小纹理大小时需要此格式。 即使 BC1、BC2 和 BC3 格式作为呈现器目标不受支持，也支持这些格式。

  如果应用程序提供了初始数据，则此变体会在它创建纹理之前将纹理数据缩放到相应的大小。 如果提供了块压缩格式（例如，BC1、BC2 或 BC3）的初始数据，则会在将其用于创建较小纹理之前，对它进行解码、缩放和重新编码。 （基于块的压缩的本质是，与从之前尚未进行编码的缩放版本的纹理中生成块压缩纹理相比，额外的解码-缩放-编码过程几乎一直导致图像质量较低。）

  如果为纹理启用 Mip 贴图，则变体将相应地减少 Mip 级别数：缩小到一半大小时降低一级，缩小到四分之一大小时降低两级。

## <a name="example"></a>示例
 在调用`CreateTexture2D`之前，此变体将在运行时调整纹理的大小。 我们不建议将此方法用于成品代码，因为完整大小的纹理会消耗更多的磁盘空间，而且此额外步骤会增加应用中的加载次数（对于需要大量要编码的计算资源的压缩纹理而言尤其如此）。 相反，我们建议你通过使用生成管道中包含的图像编辑器或图像处理器，在脱机状态下调整纹理大小。 这些方法将降低磁盘空间需求、消除应用中的运行时开销并提供更多的处理时间，以便你可以在收缩或压缩纹理时保持最佳图像质量。

## <a name="see-also"></a>请参阅
- [Mip 贴图生成变量](mip-map-generation-variant.md)
- [BC 纹理压缩变量](bc-texture-compression-variant.md)