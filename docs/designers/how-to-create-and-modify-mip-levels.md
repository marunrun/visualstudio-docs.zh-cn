---
title: 如何：创建和修改 MIP 级别
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f64d4369-2307-4175-a39a-2e45506f7fa1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0e9764bdfb476d9e2c4aa8ab2c04ee3aaa4f222a
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769059"
---
# <a name="how-to-create-and-modify-mip-levels"></a>如何：创建和修改 MIP 级别
本文档演示如何使用“图像编辑器”  生成并修改纹理空间详细级别 (LoD) 的 MIP 级别  。

## <a name="generating-mip-levels"></a>生成 MIP 级别
*Mipmapping* 是一种技术，用于通过预先计算并以不同大小存储纹理的多个副本来提高呈现速度并减少纹理对象上的混叠项。 每个副本（称为 MIP 级别）的宽度和高度均为前一副本的一半。 当在对象的表面上呈现纹理时，将自动选择与纹理表面的屏幕空间区域对应最为紧密的 MIP 级别。 这意味着图形硬件不必筛选尺寸过大的纹理来维持一致的视觉质量。 尽管存储 MIP 级别的内存开销比存储单独的原始纹理的内存开销要高大约 33%，但随之而来的是性能和图像质量上的提升。

#### <a name="to-generate-mip-levels"></a>生成 MIP 级别

1. 如[如何：创建基本纹理](../designers/how-to-create-a-basic-texture.md)中所述，从基本纹理开始。 为了获得最佳结果，请指定宽度和高度为 2 的幂（例如，256、512、1024 等）的纹理。

2. 生成 MIP 级别。 在“图像编辑器模式”工具栏上，依次选择“高级” > “工具” > “生成 Mip”。

     请注意，“转到下一 Mip 级别”  和“转到上一 Mip 级别”  按钮现在将出现在“图像编辑器模式”  工具栏上。 如果显示“属性”  窗口，则还可以注意到，只读属性“Mip 级别”  和“Mip 级别计数”  现在将出现在图像属性中。

## <a name="modifying-mip-levels"></a>修改 MIP 级别
若要实现特殊效果或在特定的详细级别提高图像质量，可以单独修改每个 MIP 级别。 例如，可以在某一距离（对应于更小的 MIP 级别更远的距离）为纹理对象提供不同的外观，或者可以确保即使处于较小的 MIP 级别，包含文本或符号的纹理仍保持清晰。

#### <a name="to-modify-an-individual-mip-level"></a>修改单个 MIP 级别

1. 选择想要修改的 MIP 级别。 在“图像编辑器模式”  工具栏上，使用“转到下一 MIP 级别”  和“转到上一 MIP 级别”  按钮在 MIP 级别之间进行选择。

2. 选择想要修改的 MIP 级别后，可以使用绘图工具对其进行修改，而不会更改其他 MIP 级别的内容。 “图像编辑器”  工具栏上提供了绘图工具。 选择工具后，可以在“属性”  窗口中更改其属性。 有关绘图工具及其属性的信息，请参阅[图像编辑器](../designers/image-editor.md)。

> [!NOTE]
> 如果无需修改单个 MIP 级别的内容（可能会执行此操作以实现某些效果），建议在生成时从源纹理生成 mipmap。 这有助于确保 MIP 级别与源纹理保持同步，因为对某一 MIP 级别的修改不会自动传播到其他级别。 有关如何在生成时生成 mipmap 的详细信息，请参阅[如何：导出包含 Mipmap 的纹理](../designers/how-to-export-a-texture-that-contains-mipmaps.md)。

## <a name="see-also"></a>另请参阅

- [如何：创建基本纹理](../designers/how-to-create-a-basic-texture.md)
