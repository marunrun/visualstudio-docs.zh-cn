---
title: 如何：创建基本纹理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 0222e8bf-d29f-421b-9b1f-123d500fa179
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bd1a9a2a269c173ef9dcb47b39921073802fe1ee
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438414"
---
# <a name="how-to-create-a-basic-texture"></a>如何：创建基本纹理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本文档说明如何使用图像编辑器创建基本纹理。  
  
 本文档演示了这些活动：  
  
- 设置纹理的大小  
  
- 设置前景色和背景色  
  
- 使用 alpha 通道（透明度）  
  
- 使用“填充”和“椭圆形”工具  
  
- 设置工具属性  
  
## <a name="creating-a-basic-texture"></a>创建基本纹理  
 可使用图像编辑器创建和修改游戏或应用的图像和纹理。  
  
 以下步骤显示如何创建表示“靶心”目标的纹理。完成后，该纹理应如下图所示。 为了更好地演示纹理中的透明度，已将图像编辑器配置为使用绿色的方格棋盘图案来显示它。  
  
 ![显示为绿色的透明“靶心”目标](../designers/media/digit-bullseye-texture-in-editor.png "Digit-Bullseye-Texture-In-Editor")  
  
 开始前，请确保显示“属性”窗口”。 在工作时，可以使用“属性”窗口设置图像的大小、更改工具属性以及指定颜色。  
  
#### <a name="to-create-a-bullseye-target-texture"></a>创建“靶心”目标纹理  
  
1. 创建要使用的纹理。 有关如何向项目中添加纹理的信息，请参阅[图像编辑器](../designers/image-editor.md)中的“入门”部分。  
  
2. 将图像大小设置为 512x512 像素。 在“属性”窗口中，将“宽度”和“高度”属性的值设置为 `512`。  
  
3. 在“图像编辑器”工具栏上，选择“填充”工具。 “属性”窗口现在显示“填充”工具的属性以及图像属性。  
  
4. 将前景色设置为完全透明的黑色。 在“属性”窗口的“颜色”属性组中，选择“前景色”。 将颜色选取器旁边的“R”、“G”、“B”和“A”属性的值设置为 `0`。  
  
5. 在“图像编辑器”工具栏上，选择“填充”工具，然后按住 Shift 键并选择图像中的任意点。 使用 Shift 键让填充颜色的 Alpha 值替换图像中的颜色；否则，Alpha 值将用于将填充颜色与图像中的颜色进行混合。  
  
   > [!IMPORTANT]
   > 此步骤和上一步中的颜色选择一起确保为要绘制的“靶心”目标纹理准备好了基本图像。 当用透明黑色填充图像时（因为目标的边框是黑色的），目标周围将没有混叠的项。  
  
6. 在“图像编辑器”工具栏上，选择“椭圆形”工具。  
  
7. 将前景色设置为完全不透明的黑色。 将“R”、“G”和“B” 属性的值设置为 `0`，将“A”属性的值设置为 `255`。  
  
8. 将背景色设置为完全不透明的白色。 在“属性”窗口的“颜色”属性组中，选择“背景”。 将 **R**、**G**、**B** 和 **A** 属性的值设置为 `255`。  
  
9. 设置椭圆形边框的宽度。 在“属性”窗口的“外观”属性组中，将“宽度”属性的值设置为 `8`。  
  
10. 确保已启用抗锯齿。 在“属性”窗口的“外观”属性组中，确保设置了“抗锯齿”属性。  
  
11. 使用“椭圆形”工具，从像素坐标 `(3, 3)` 到像素坐标 `(508, 508)` 绘制一个圆。 为了更轻松地绘制圆形，可以在绘制时按住 Shift 键。  
  
    > [!NOTE]
    > 当前指针位置的像素坐标显示在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 状态栏上。  
  
12. 更改背景色。 将“R”设置为 `44`、将“G” 设置为 `165`、将“B” 设置为 `211`、将“A” 设置为 `255`。  
  
13. 从像素坐标 `(64, 64)` 到像素坐标 `(448, 448)` 绘制另一个圆。  
  
14. 将背景色更改为完全不透明的白色。 将“R”、“G”、“B”和“A”设置为 `255`。  
  
15. 从像素坐标 `(128, 128)` 到像素坐标 `(384, 384)` 绘制另一个圆。  
  
16. 更改背景色。 将“R”设置为 `255`、将“G” 和“B” 设置为 `64`，并将“A” 设置为 `255`。  
  
17. 从像素坐标 `(192, 192)` 到像素坐标 `(320, 320)` 绘制另一个圆。  
  
    “靶心”目标纹理是完整的。 下面是最终图像（以透明度显示）。  
  
    ![完整的“靶心”目标纹理](../designers/media/gfx-image-demo-bullseye.png "gfx_image_demo_bullseye")  
  
    作为下一步，可以为此纹理生成 MIP 级别。 有关详细信息，请参阅[如何：创建和修改 MIP 级别](../designers/how-to-create-and-modify-mip-levels.md)。  
  
## <a name="see-also"></a>请参阅  
 [图像编辑器](../designers/image-editor.md)
