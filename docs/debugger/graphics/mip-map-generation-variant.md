---
title: Mip 贴图生成变量 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3b4b3583-0b01-4f5d-aacb-3f96d19111d9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 06017a3feb3faa667b469c0075e561b2104785b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895594"
---
# <a name="mip-map-generation-variant"></a>Mip-map 生成变量
对非呈现器目标的纹理启用 mip 贴图。

## <a name="interpretation"></a>解释
Mip 贴图主要用于通过预先计算更小版本的纹理，来在缩减状态下消除纹理中的锯齿瑕疵。 虽然这些额外纹理会消耗 GPU 内存（大约比原始纹理多 33%），但是它们也更为高效，因为它们具有更多符合 GPU 纹理缓存的表面区域，并且其内容也会达到更高的使用率。

对于三维场景，我们建议在内存可用于存储额外纹理的情况下使用 mip 贴图，因为它们会提高呈现性能和图像质量。

如果此变体显示显著的性能提升，则表示你使用的是纹理，而未启用 mip 贴图，因此无法充分利用纹理缓存。

## <a name="remarks"></a>备注
每次调用创建源纹理的 `ID3D11Device::CreateTexture2D` 时，都强制执行 mip 贴图生成。 Mip 贴图生成时在传递的 D3D11_TEXTURE2D_DESC 对象，具体而言，将强制`pDesc`描述不变的着色器资源; 即：

- BindFlags 成员仅设置 D3D11_BIND_SHADER_RESOURCE 标志。

- 将 Usage 成员设置为 D3D11_USAGE_DEFAULT 或 D3D11_USAGE_IMMUTABLE。

- 将 CPUAccessFlags 成员设置为 0（无 CPU 访问）。

- SampleDesc 成员将其 Count 成员设置为 1（不支持多重采样抗锯齿 (MSAA)）。

- 将 MipLevels 成员设置为 1（无现有 mip 贴图）。

  当应用程序提供初始数据时，纹理格式必须支持自动 mip 贴图生成（由 D3D11_FORMAT_SUPPORT_MIP_AUTOGEN 确定），除非该格式为 BC1、BC2 或 BC3；否则，纹理不会发生修改，并且提供初始数据时也不会生成任何 mip 贴图。

  如果已为纹理自动生成 mip 贴图，则会在播放期间修改对 `ID3D11Device::CreateShaderResourceView` 的调用，以在纹理采样期间使用 mip 链。

## <a name="example"></a>示例
通过使用如下代码，可重现“Mip 贴图生成”变体：

```cpp
D3D11_TEXTURE2D_DESC texture_description;

// ...

texture_description.MipLevels = 0; // generate a full mipchain

std::vector<D3D11_SUBRESOURCE_DATA> initial_data(num_mips);

for (auto&& mip_level : initial_data)
{
    // fill mip_level with the application-supplied initial data
}

d3d_device->CreateTexture2D(&texture_description, initial_data.data(), &texture)
```

若要创建具有完整 mip 链的纹理，请将 `D3D11_TEXTURE2D_DESC::MipLevels` 设置为 0。 完整 mip 链中的 mip 级别数是 floor(log2(n) + 1），其中 n 是纹理的最大维度。

请记住，当你向 `CreateTexture2D` 提供初始数据时，你必须为每个 mip 级别提供一个 D3D11_SUBRESOURCE_DATA 对象。

> [!NOTE]
> 如果你希望提供你自己的 mip 级别内容而不是自动生成它们，你必须使用支持进行了 mip 贴图的纹理的图像编辑器创建纹理，然后加载该文件并将 mip 级别传递给 `CreateTexture2D`。

## <a name="see-also"></a>请参阅
[Half/Quarter 纹理维度变量](half-quarter-texture-dimensions-variant.md)
