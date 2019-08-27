---
title: 如何：导出包含 mipmap 的纹理
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3d1ad14b-44fb-4cf0-a995-5e2f60026524
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5226903112d06d5efa362c61db938124eed8e68
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62897313"
---
# <a name="how-to-export-a-texture-that-contains-mipmaps"></a>如何：导出包含 mipmap 的纹理

在项目生成阶段，图像内容管道可从源图像生成 mipmap。 若要实现某些效果，有时必须手动指定每个 MIP 级别的图像内容。 无需手动指定每个 MIP 级别的图像内容时，在生成时生成 mipmap 可确保 mipmap 内容一直保持同步。还可避免在运行时生成 mipmap 的性能成本。

本文包含以下内容：

- 将源映像配置为由图像内容管道进行处理。

- 配置图像内容管道，生成 mipmap。

## <a name="export-mipmaps"></a>导出 mipmap

Mipmapping 为 3D 游戏或应用中的带纹理图面提供自动屏幕空间细节层次。 它可通过预先计算纹理的向下采样版本，增强游戏或应用的渲染性能。 通过预先计算下采样版本，每次采样时，不必对整个纹理进行向下采样。

### <a name="to-export-a-texture-that-has-mipmaps"></a>导出包含 mipmap 的纹理

1. 从基本纹理开始。 加载现有图像文件，或根据[如何：创建基本纹理](../designers/how-to-create-a-basic-texture.md)所述，创建一个纹理。 若要支持 mipmap，请指定一个宽度和高度尺寸都是 2 的同次幂的纹理，如 64x64、256x256 或 512x512。

2. 配置刚刚创建的纹理文件，使其由图像内容管道进行处理。 在“解决方案资源管理器”中，打开创建的纹理文件的快捷菜单，然后选择“属性”。 在“配置属性” > “常规”页上，将“项目类型”属性设置为“图像内容管道”。 请确保将“内容”属性设置为“是”，并且将“从生成中排除”设置为“否”。 选择“应用”。

   将出现“图像内容管道”配置属性页。

3. 配置图像内容管道，生成 mipmap。 在“配置属性” > “图像内容管道” > “常规”页上，将“生成 Mip”属性设置为“是(/generatemips)”。

4. 选择“确定”。

生成项目后，图像内容管道会将源图像从工作格式转换为指定的输出格式（包括 MIP 级别）。 将结果复制到项目的输出目录。