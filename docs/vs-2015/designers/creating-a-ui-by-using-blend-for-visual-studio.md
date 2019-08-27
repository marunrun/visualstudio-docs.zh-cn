---
title: 使用 Blend 创建 UI
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- Blend.Start.Dev12
ms.assetid: efd12263-cc2d-4081-a2bb-9a2cc17c442c
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7cd7f14158b7dee83767ee9295c8917cadd30fa5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695936"
---
# <a name="creating-a-ui-by-using-blend-for-visual-studio"></a>使用 Blend for Visual Studio 创建 UI
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Blend for Visual Studio 可帮助设计基于 XAML 的 Windows 桌面、Web、[Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/jj683071.aspx) 和 [Windows 应用商店](https://msdn.microsoft.com/library/windows/apps/jj129478.aspx)应用。 它提供了与 Visual studio 相同的基本 XAML 设计体验，并添加了可视化设计器，以用于高级任务，例如动画和行为。

 Blend for Visual Studio 随附 Visual Studio 提供，无需下载。 但需要在 Visual Studio 安装程序选中，以便在系统上安装。

 如果是初次接触 Blend for Visual Studio，则要花一些时间来熟悉工作区的特有功能。 本主题将作用快速教程。

> [!NOTE]
> 若要浏览共享的设计功能，例如美工板、“文档大纲”窗口和“设备”窗口，请参阅[使用 XAML 设计器创建 UI](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)。

 **主题内容**：

- [“工具”面板概览](#Tools)

- [“资产”面板概览](#Assets)

- [“对象和时间线”面板概览](#Objects)

- [“属性”面板概览](#Properties)

## <a name="Tools"></a>“工具”面板概览
 可在应用程序中通过 Blend for Visual Studio 的“工具”面板创建和修改对象。 可以通过使用鼠标选择工具并在美工板上进行绘制来创建对象。

 ![工具面板](../designers/media/blend5toolspanel.png "Blend5Toolspanel")

|||||
|-|-|-|-|
|![](../designers/media/b1-1.png "B1_1")|**选择工具** - 选择对象和路径。<br /><br /> 使用“直接选择”工具可选择嵌套对象和路径段。|![标注 A](../designers/media/b5-label-a.png "b5_label_A")|**渐变和画笔工具**|
|![](../designers/media/b1-2.png "B1_2")|**视图工具** - 调整美工板的视图，例如平移和缩放。|![标注 B](../designers/media/b5-label-b.png "b5_label_B")|**路径工具**|
|![](../designers/media/b1-3.png "B1_3")|**画笔工具** - 处理对象的可视特性，例如转换画笔、绘制对象，或者选择某对象属性将其应用到其他对象。|![标注 C](../designers/media/b5-label-c.png "b5_label_C")|**形状工具**|
|![](../designers/media/b1-4.png "B1_4")|**对象工具** - 在美工板上绘制最常用的对象，例如路径、形状、布局面板、文本和控件。|![标注 D](../designers/media/b5-label-d.png "b5_label_D")|**版式面板**|
|![](../designers/media/b1-5.png "B1_5")|**资产工具** - 访问“资产”面板并显示库中最近用过的资产。|![标注 E](../designers/media/b5-label-e.png "b5_label_E")|**文本控件**|
|||![标注 F](../designers/media/b5-label-f.png "b5_label_F")|**常见控件**|

 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [工具栏](https://www.youtube.com/watch?v=VkdUJcvoo54&list=PLBDF977B2F1DAB358&index=4)。

## <a name="Assets"></a>“资产”面板概览
 可在“资产”面板中找到所有控件，它类似于 Visual Studio 中的“工具箱”。 除控件外，“资产”面板还包括所有可添加到美工板的内容，例如样式、媒体、行为和效果等。

 ![资产面板](../designers/media/blend5-assets-panel.png "Blend5_Assets_panel")

|||
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**搜索框** - 可在“搜索”框中键入值来筛选资产列表。|
|![](../designers/media/b1-2.png "B1_2")|**网格模式和列表模式** - 在资产的“网格模式”视图和“列表模式”视图之间切换。|
|![](../designers/media/b1-3.png "B1_3")|**资产类别** - 单击类别或子类别查看该类别中资产的列表。|
|![](../designers/media/b1-4.png "B1_4")|**样式** - 显示资源字典中包含的所有样式。|
|![](../designers/media/b1-5.png "B1_5")|**说明** - 查看所选资产类别或子类别的说明。|

## <a name="Objects"></a>“对象和时间线”面板概览
 使用此面板可在美工板上组织对象以及（如果需要）对它们进行动画处理。

 ![动画模式中的“对象和时间线”面板](../designers/media/b5-object-timeline-animation.png "b5_object_timeline_animation")

|||
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**对象视图** - 查看文档的可视树。 可以深化到不同级别的详细信息。 还可以添加层以便进一步在美工板上组织对象。 通过这种方式可以将它们作为组进行锁定和隐藏。|
|![](../designers/media/b1-2.png "B1_2")|**记录模式指示器** - 查看是否在时间线中记录属性更改。|
|![](../designers/media/b1-3.png "B1_3")|**情节提要选取器** - 查看已创建的情节提要的列表。|
|![](../designers/media/b1-4.png "B1_4")|**关闭情节提要** - 关闭当前情节提要。|
|![](../designers/media/b1-5.png "B1_5")|**情节提要选项** - 创建、复制、反向、删除、重命名或关闭情节提要。|
|![](../designers/media/b1-6.png "B1_6")|**播放控件** - 在时间线中导航。 也可拖动播放指针来定位（或*推移*）时间线。|
|![](../designers/media/b1-7.png "B1_7")|**返回到范围** - 将对象视图的范围返回到上一个根对象或上一个范围。 仅当修改样式或模板时，才能执行此操作。|
|![](../designers/media/b1-8.png "B1_8")|**记录关键帧** - 记录所选对象属性在当前时间点的快照。|
|![](../designers/media/b1-9.png "B1_9")|**对齐选项** - 设置时间线对齐、对齐分辨率以及关闭时间线对齐。|
|![](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png "97fa60b9-0caf-4387-9225-b57510d32209")|**显示/隐藏**、**锁定/解除锁定** - 显示或隐藏对象视图的可见性和锁定选项。|
|![](../designers/media/b1-11.png "B1_11")|**播放指针在时间线上的位置** - 以毫秒为单位显示当前时间。 也可以直接在此字段中输入时间值以跳到特定的时间点。 精度取决于“对齐选项”中设置的对齐分辨率。|
|![](../designers/media/b1-12.png "B1_12")|**播放指针** - 确定动画所处的时间点。 可以在时间线中拖动播放指针，以便预览动画。|
|![](../designers/media/b1-13.png "B1_13")|**时间线上设置的关键帧** - 更改特点时间点的属性值。|
|![](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png "d839d12c-07a1-4127-a830-4a8e7069f4fe")|**更改对象顺序** - 设置对象的显示顺序。 单击此按钮可在结构视图中按 Z 顺序（从前到后）或按标记顺序（在“XAML”视图中出现的顺序）排列对象。|
|![](../designers/media/b1-15.png "B1_15")|**时间线缩放** - 设置时间线的缩放分辨率。 通过放大，可以编辑动画的更多细节；而通过缩小，可更全面地显示在更长时间段内发生的情况。 如果进行放大，但无法在所需时间位置设置关键帧，请验证设置的对齐分辨率是否足够高。|
|![标注 16](../designers/media/b5-label-16.png "b5_label_16")|**时间线构成区域** - 查看时间线，并通过拖动关键帧或通过其快捷菜单移动关键帧。|

## <a name="Properties"></a>“属性”面板概览
 使用此面板可查看和修改对象的属性。 还可以直接在美工板上设置它们。 若如此操作，则“属性”面板中将反映出属性更改。

 ![属性面板](../designers/media/blend5-properties-panel.png "Blend5_properties_panel")

 **类别** - 展开和折叠类别的属性。 单击“展开”![](../designers/media/6375953d-074c-421a-bbb3-6f5055b67b64.png "6375953d-074c-421a-bbb3-6f5055b67b64") 和“折叠”![折叠](../designers/media/b5-collapse-button.png "b5_collapse_button") 可显示或隐藏类别详细信息。

|                                                                                                         |                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                 ![](../designers/media/b1-1.png "B1_1")                                 |                                                                              **名称和类型** - 查看所选对象的图标、名称和类型。                                                                              |
|                                 ![](../designers/media/b1-2.png "B1_2")                                 |                                                                          **排列方式** - 按名称、源或类别的字母顺序排列属性。                                                                          |
|                                 ![](../designers/media/b1-3.png "B1_3")                                 |                                                        **画笔属性** - 设置填充画笔、笔划画笔和前景画笔等画笔的可视属性。                                                        |
|                                 ![](../designers/media/b1-4.png "B1_4")                                 |                                                                                    **颜色编辑器** - 用于纯色画笔和渐变画笔。                                                                                    |
|                                 ![](../designers/media/b1-5.png "B1_5")                                 |                                                                                                 **颜色选取器** - 选择颜色。                                                                                                 |
|                                 ![](../designers/media/b1-6.png "B1_6")                                 |                                                                              **色卡** - 查看初始颜色、当前颜色和上一种颜色                                                                               |
|                                 ![](../designers/media/b1-7.png "B1_7")                                 | **取色器** - 使用屏幕上任意元素的颜色。 选择“纯色画笔”时，“颜色取色器”可用。 选择“渐变画笔”时，“渐变取色器”可用。 |
|                                 ![](../designers/media/b1-8.png "B1_8")                                 |                                                                        **属性和事件** - 为所选元素设置属性或选择事件。                                                                         |
|                                 ![](../designers/media/b1-9.png "B1_9")                                 |                                                         **搜索框** - 搜索属性。 在“搜索”框中键入值来筛选显示的属性。                                                          |
| ![](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png "97fa60b9-0caf-4387-9225-b57510d32209") |                                **画笔编辑器选项卡** - 用于选择画笔编辑器。 可选择“无画笔”、“纯色画笔”、“渐变画笔”、“平铺画笔”或“画笔资源”。                                |
|                                ![](../designers/media/b1-11.png "B1_11")                                |                                    **颜色资源** - 将完全相同的颜色应用于不同属性。 “颜色资源”选项卡包括“本地资源”和“系统资源”。                                    |
|                                ![](../designers/media/b1-12.png "B1_12")                                |                                                 **RGB 颜色空间**- 通过调整“R”、“G”或“B”（分别表示红、绿、蓝）数字编辑器中的值修改颜色。                                                  |
|                                ![](../designers/media/b1-13.png "B1_13")                                |                                                                        **Alpha 通道** - 使用 **A** 旁边的数字编辑器修改 Alpha 值。                                                                        |
| ![](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png "d839d12c-07a1-4127-a830-4a8e7069f4fe") |                                       **将颜色转换为资源** - 将所选颜色转换为颜色资源。 在单击“颜色资源”选项卡时，可以获得颜色资源。                                        |
|                                ![](../designers/media/b1-15.png "B1_15")                                |                                                                                 **十六进制值** - 查看所显示颜色的十六进制值。                                                                                 |
|                     ![标注 16](../designers/media/b5-label-16.png "b5_label_16")                     |                                                                                **渐变滑块** - 仅当选择渐变画笔时才显示。                                                                                 |
| ![](../designers/media/d50027a1-6824-4ad8-8b4e-558b0756dcf8.png "d50027a1-6824-4ad8-8b4e-558b0756dcf8") |                                                                     **显示高级属性** - 查看不常用属性的类别。                                                                      |

 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [属性面板](https://www.youtube.com/watch?v=HCqQfiobdag&list=PLBDF977B2F1DAB358&index=7)。

## <a name="see-also"></a>请参阅
 [插入控件并修改其行为](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md)[对象进行动画处理](../designers/animate-objects-in-xaml-designer.md)[绘制形状和路径](../designers/draw-shapes-and-paths.md) [Visual Studio 和 Blend for Visual Studio 中设计 XAML](../designers/designing-xaml-in-visual-studio.md)
