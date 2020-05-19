---
title: Point/Bilinear/Trilinear/Anisotropic 纹理过滤变量
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 57d14fc9-b5f7-45ee-9717-48086886742d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 314ec61da7ed61cc8bdd573e201d98a53862a32c
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66262923"
---
# <a name="point-bilinear-trilinear-and-anisotropic-texture-filtering-variants"></a>Point、Bilinear、Trilinear 和 Anisotropic 纹理过滤变量
重写相应纹理取样器上的筛选模式。

## <a name="interpretation"></a>解释
 不同的纹理采样方法具有不同的性能开销和图像质量。 按照增加开销（提高视觉质量）的顺序，筛选模式如下：

1. 点筛选（能耗最低、视觉质量最差）

2. 双线性筛选

3. 三线性筛选

4. 各向异性筛选（能耗最高、视觉质量最佳）

   如果每个变体的性能开销巨大，或随占用性能更多的筛选模式而增加，则你可以在其开销和提高图像质量之间进行权衡。 根据你的评估，你可以接受其他性能开销以提高视觉质量，或者接受降低了的视觉质量以达到更高的帧速率或回收你可以通过其他方式使用的性能。

   如果你发现无论筛选模式如何，性能开销都可忽略或很稳定（例如，当你面向的 GPU 具有充足的着色器吞吐量和内存带宽时），则请考虑使用各向异性筛选，以在应用中达到最佳图像质量。

## <a name="remarks"></a>备注
 这些变体将在调用 `ID3D11DeviceContext::PSSetSamplers` 时重写取采样器状态，其中应用程序提供的取样器的筛选模式为以下模式之一：

- `D3D11_FILTER_MIN_MAG_MIP_POINT`

- `D3D11_FILTER_MIN_MAG_POINT_MIP_LINEAR`

- `D3D11_FILTER_MIN_POINT_MAG_LINEAR_MIP_POINT`

- `D3D11_FILTER_MIN_POINT_MAG_MIP_LINEAR`

- `D3D11_FILTER_MIN_LINEAR_MAG_MIP_POINT`

- `D3D11_FILTER_MIN_LINEAR_MAG_POINT_MIP_LINEAR`

- `D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT`

- `D3D11_FILTER_MIN_MAG_MIP_LINEAR`

- `D3D11_FILTER_ANISOTROPIC`

  在“点纹理筛选”变体中，应用程序提供的筛选模式将替换为 `D3D11_FILTER_MIN_MAG_MIP_POINT`；在“双线性纹理筛选”变体中，将替换为 `D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT`；在“三线性纹理筛选”变体中，将替换为 `D3D11_FILTER_MIN_MAG_MIP_LINEAR`  。

  在“各向异性纹理筛选”变体中，应用程序提供的筛选模式将替换为 `D3D11_FILTER_ANISOTROPIC`，且最大各向异性将设置为 16。

## <a name="restrictions-and-limitations"></a>限制和约束
 在 Direct3D 中，功能级别 9.1 指定最大各向异性为 2x。 因为“各向异性纹理筛选”变体尝试以独占方式使用 16x 各向异性，所以当帧分析在功能级别 9.1 的设备上运行时播放将失败。 受此约束影响的现代设备包括基于 ARM 的 Surface RT 和 Surface 2 Windows 平板电脑。 仍然可能在某些计算机中找到的较旧 GPU 也可能会受影响，但是将它们普遍视为已过时且它们越来越不常见。

## <a name="example"></a>示例
 通过使用如下代码，可重现“点纹理筛选”变体：

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_MIN_MAG_MIP_POINT;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```

## <a name="example"></a>示例
 通过使用如下代码，可重现“双线性纹理筛选”变体：

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```

## <a name="example"></a>示例
 通过使用如下代码，可重现“三线性纹理筛选”变体：

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_MIN_MAG_MIP_LINEAR;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```

## <a name="example"></a>示例
 通过使用如下代码，可重现“各向异性问题筛选”变体：

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_ANISOTROPIC;
sampler_description.MaxAnisotropy = 16;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```
