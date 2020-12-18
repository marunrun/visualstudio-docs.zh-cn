---
title: Visual Studio 的图像和图标 | Microsoft Docs
description: 了解用于创建 Visual Studio 图像和图标的设计概念。
ms.date: 04/26/2017
ms.topic: overview
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f29fd0a69ceafa33c00593b67f6775a723780c26
ms.sourcegitcommit: 8a0d0f4c4910e2feb3bc7bd19e8f49629df78df5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2020
ms.locfileid: "97668646"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio 的图像和图标
## <a name="image-use-in-visual-studio"></a><a name="BKMK_ImageUseInVisualStudio"></a> Visual Studio 中的图像使用
 在创建图稿之前，请考虑使用 [Visual Studio 图像库](https://www.microsoft.com/download/details.aspx?id=35825)中的 1,000 多个图像。

### <a name="types-of-images"></a>图像类型

- **图标**。 出现在命令、层次结构、模板等中的小图像。 在 Visual Studio 中使用的默认图标大小为 16x16 PNG。 图像服务生成的图标会自动生成支持 HDPI 的 XAML 格式。

    > [!NOTE]
    > 在菜单系统中使用图像时，不应为每个命令创建图标。 请参阅 [Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)，以确定命令是否应有图标。

- **缩略图。** 在对话框预览区域中使用的图像，例如“新建项目”对话框。

- **对话框图像。** 显示在对话框或向导中的图像，可以是描述性图形或消息指示符。 不经常使用，仅在必要时使用，作用是说明复杂概念或引起用户注意（警报、警告）。

- **动画图像。** 用于进度指示器、状态栏和操作对话框。

- **游标。** 用于指示是否允许使用鼠标进行操作，可以在何处放置对象等。

## <a name="icon-design"></a><a name="BKMK_IconDesign"></a> 图标设计

### <a name="overview"></a>概述
 Visual Studio 使用了新式风格的图标，这些图标采用简洁几何图形和 50/50 的正值/负值（浅色/深色）平衡效果，并使用直接、可理解的喻示方式。 图标设计主要以明确性、简化度和上下文为着眼点。

- **明确性：** 使用传达图标核心意义和个性的喻示。

- **简化度：** 图标直接传达核心含义 - 只通过必要元素传达主题，不含虚饰。

- **上下文：** 在概念开发过程中考虑图标角色的各个方面，这在决定哪些元素构成图标的核心喻意时至关重要。

  设计图标时，有一些需要避免的设计：

- 除非适用，否则不要使用表示 UI 元素的图标。 如果 UI 元素不常见、不明显或不独特，请选择更抽象或更符号化的方法。

- 不要过度使用文档、文件夹、箭头和放大镜等常用元素。 仅当对图标的含义至关重要时才使用此类元素。 例如，面向右方的放大镜应只用于指示“搜索”、“浏览”和“查找”功能。

- 尽管某些旧图标元素保留了透视，但创建新图标时不要使用透视，除非该元素在没有透视的情况下会显得不明确。

- 不要在图标中加入太多信息。 一个可作为可识别的符号轻松识别或了解的图像，比一个过于复杂的图像有用得多。 图标无法传达全部信息。

### <a name="icon-creation"></a>图标创建

#### <a name="concept-development"></a>概念开发
 Visual Studio 提供丰富多样的 UI 图标类型。 在开发过程中仔细考虑图标类型。 不要为图标元素使用不明确或不常见的 UI 对象。 在这些情况下选择使用符号，例如“智能标记”图标。 请注意，左侧抽象标记的含义比右侧基于 UI、意味不明的标记更明确：

|**符号图像的正确使用**|**符号图像的错误使用**|
|-|-|
|![正确的“智能标记”图标](../../extensibility/ux-guidelines/media/0404-01_smarttagcorrect.png "0404-01_SmartTagCorrect")|![不正确的“智能标记”图标](../../extensibility/ux-guidelines/media/0404-02_smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 在某些情况下，为图标使用标准的、易于识别的 UI 元素可以有很好的效果。 “添加窗口”就是一个示例：

|**图标中的正确 UI 元素**|**图标中的错误 UI 元素**|
|-|-|
|![正确的“添加窗口”图标](../../extensibility/ux-guidelines/media/0404-03_addwindowcorrect.png "0404-03_AddWindowCorrect")|![不正确的“添加窗口”图标](../../extensibility/ux-guidelines/media/0404-04_addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 不要将文档用作基本元素，除非它对图标的含义至关重要。 如果“添加文档”（如下）上不含文档元素，则无法传达含义，而使用“刷新”时，则无需使用文档元素来传达含义。

|**文档图标的正确使用**|**文档图标的错误使用**|
|-|-|
|![正确的“文档”图标](../../extensibility/ux-guidelines/media/0404-05_documenticoncorrect.png "0404-05_DocumentIconCorrect")|![不正确的“文档”图标](../../extensibility/ux-guidelines/media/0404-06_documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 对于“显示”这一概念，所使用的图标应能够最有效地说明所显示的内容，一个例子是“显示所有文件”。 如有必要，可以使用透镜隐喻来表示“视图”的概念，一个例子是“资源视图”。

|**“显示”**|**查看”**|
|-|-|
|![“显示”图标](../../extensibility/ux-guidelines/media/0404-07_show.png "0404-07_Show")|![“查看”图标](../../extensibility/ux-guidelines/media/0404-08_view.png "0404-08_View")|

 面朝右方的放大镜图标应只用于表示“搜索”、“查找”和“浏览”。 带加号或减号的左向版本应只用于表示放大/缩小。

|**“搜索”**|**“缩放”**|
|-|-|
|![搜索图标](../../extensibility/ux-guidelines/media/0404-09_search.png "0404-09_Search")|![缩放图标](../../extensibility/ux-guidelines/media/0404-10_zoom.png "0404-10_Zoom")|

 在树状视图中，不要同时使用文件夹图标和修饰符。 如果可用，请仅使用修饰符。

|**正确的树状视图图标**|**错误的树状视图图标**|
|-|-|
|![正确的树状视图图标 &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11_treeviewcorrect1.png "0404-11_TreeViewCorrect1") ![正确的树状视图图标 &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12_treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![错误的树状视图图标 &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13_treeviewincorrect1.png "0404-13_TreeViewIncorrect1") ![错误的树状视图图标 &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14_treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>样式详细信息

#### <a name="layout"></a>布局
 堆栈元素，如标准 16x16 图标所示：

 ![16x16 图标的布局堆栈](../../extensibility/ux-guidelines/media/0404-15_layoutstack.png "0404-15_LayoutStack")<br />16x16 图标的布局堆栈

 状态通知元素最好作为独立图标使用。 但在某些上下文中，需要在基本元素上叠放一个通知，例如“任务完成”图标：

 ![Visual Studio 中的独立通知](../../extensibility/ux-guidelines/media/0404-16_standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")<br />独立通知图标

 ![“任务完成”图标](../../extensibility/ux-guidelines/media/0404-17_taskcomplete.png "0404-17_TaskComplete")<br />“任务完成”图标

 项目图标通常是包含多种大小的 .ico 文件。 大多数 16x16 图标包含相同的元素。 32x32 版本提供更多详细信息，适用时还包括项目类型。

 ![Visual Studio 中的“项目”图标](../../extensibility/ux-guidelines/media/0404-18_iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")<br />VB Windows 控件库项目图标，16x16 和 32x32

 使图标在其像素帧内居中。 如果无法做到这一点，让图标与帧顶部和/或右侧对齐。

 ![图标在像素框架中居中](../../extensibility/ux-guidelines/media/0404-19_iconcentered.png "0404-19_IconCentered")<br />图标在像素框架中居中

 ![图标与像素框架的右上方对齐](../../extensibility/ux-guidelines/media/0404-20_icontopright.png "0404-20_IconTopRight")<br />图标与帧右上方对齐

 ![图标居中并与像素框架的顶部对齐](../../extensibility/ux-guidelines/media/0404-21_icontopalign.png "0404-21_IconTopAlign")<br />图标居中并与帧顶部对齐

 若要实现理想的对齐和平衡，请避免因使用操作字形而阻挡图标的基本元素。 将字形置于基本元素左上角附近。 添加其他元素时，请考虑图标的对齐和平衡。

|**正确的对齐和平衡方式**|**不正确的对齐和平衡方式**|
|-|-|
|![正确的图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-22_alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![不正确的图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-23_alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 确保共有某些元素且成套使用的图标在大小上是匹配的。 注意，如果大小不合适，例如圆圈和箭头的尺寸过大，会导致不匹配。

|**正确的匹配大小**|**不正确的匹配大小**|
|-|-|
|![正确的图标的大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-24_sizeparitycorrect.png "0404-24_SizeParityCorrect")|![不正确的图标的大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-25_sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 使用一致的线条和视觉权重。 使用并排比较的方式来评估要生成的图标与其他图标的比较结果。 切勿使用整个 16x16 帧，请使用 15x15 或更小的帧。 负值对正值（深色对浅色）的比率应该是 50/50。

|**正确的负值对正值比率**|**不正确的负值到正值比率**|
|-|-|
|![正确的图标视觉对象粗细 &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-26_visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![正确的图标视觉对象粗细 &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27_visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![正确的图标视觉对象粗细 &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-28_visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![不正确的图标视觉重量](../../extensibility/ux-guidelines/media/0404-29_visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 在不牺牲元素完整性的前提下，使用简单、类似的形状并从互补的角度来生成元素。 角度尽可能使用 45° 或 90°。

 ![正确的图标角度](../../extensibility/ux-guidelines/media/0404-30_iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>透视
 保持图标清晰易懂。 仅在必要时才使用透视和光源。 虽然应避免在图标元素上使用透视，但有些元素如果没有透视，就无法识别。 在这种情况下，可使用有样式的透视来确保元素明确。

 ![3 点透视图](../../extensibility/ux-guidelines/media/0404-31_3pointperspective.png "0404-31_3PointPerspective")<br />3 点透视图

 ![1 点透视图](../../extensibility/ux-guidelines/media/0404-32_1pointperspective.png "0404-32_1PointPerspective")<br />1 点透视图

 大多数元素应面向右或侧向右倾斜：

 ![向右倾斜的图标](../../extensibility/ux-guidelines/media/0404-33_angledright.png "0404-33_AngledRight")

 只有在给物体增加必要的明确度时才使用光源。

|**正确的光源**|**不正确的光源**|
|-|-|
|![正确的图标光源](../../extensibility/ux-guidelines/media/0404-34_lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![不正确的图标光源](../../extensibility/ux-guidelines/media/0404-35_lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 轮廓只用于提高可读性或更好地传达喻意。 负值-正值（深色-浅色）平衡应为 50/50。

|**轮廓的正确使用**|**轮廓的不正确使用**|
|-|-|
|![正确的轮廓](../../extensibility/ux-guidelines/media/0404-36_outlinescorrect.png "0404-36_OutlinesCorrect")|![不正确的轮廓](../../extensibility/ux-guidelines/media/0404-37_outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>图标类型
 “Shell 和命令栏图标”最多由以下元素中的三种组成：一个基本元素、一个修饰符、一个操作或一个状态。

 ![shell 和命令栏图标的示例](../../extensibility/ux-guidelines/media/0404-38_shellicons.png "0404-38_ShellIcons")<br />shell 和命令栏图标的示例

 “工具窗口和命令栏”图标最多由以下元素中的三种组成：一个基本元素、一个修饰符、一个操作或一个状态。

 ![工具窗口命令栏图标的示例](../../extensibility/ux-guidelines/media/0404-39_toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")<br />工具窗口命令栏图标的示例

 “树状视图消歧器”图标最多由以下元素中的三种组成：一个基本元素、一个修饰符、一个操作或一个状态。

 ![树状视图消歧器图标示例](../../extensibility/ux-guidelines/media/0404-40_treeviewicons.png "0404-40_TreeViewIcons")<br />树状视图消歧器图标示例

 “基于状态的值分类”图标有以下几种状态：活动、活动已禁用和非活动已禁用。

 ![基于状态的值分类图标示例](../../extensibility/ux-guidelines/media/0404-41_statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")<br />基于状态的值分类图标示例

 “IntelliSense”图标最多由以下元素中的三种组成：一个基本元素、一个修饰符和一个状态。

 ![IntelliSense 图标示例](../../extensibility/ux-guidelines/media/0404-42_intellisenseicons.png "0404-42_IntelliSenseIcons")<br />IntelliSense 图标示例

 “小型 (16x16) 项目”图标应不超过两个元素：一个基本元素和一个修饰符。

 ![小型 (16x16) 项目图标示例](../../extensibility/ux-guidelines/media/0404-43_16x16project1.png "0404-43_16x16Project1") ![16x16 项目图标 &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44_16x16project2.png "0404-44_16x16Project2") ![16x16 项目图标 &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45_16x16project3.png "0404-45_16x16Project3")<br />小型 (16x16) 项目示例

 “大型 (32x32) 项目”图标由不超过以下元素中的四个组成：一个基本元素、一到两个修饰符和一个语言覆盖。

 ![大型 (32x32) 项目图标示例](../../extensibility/ux-guidelines/media/0404-46_32x32project.png "0404-46_32x32Project")<br />大型 (32x32) 项目图标示例

### <a name="production-details"></a>生产详细信息
 所有新的 UI 元素都应使用 Windows Presentation Foundation (WPF) 创建，WPF 的所有新图标都应采用 32 位 PNG 格式。 24 位 PNG 是一种不支持透明度的旧格式，因此不建议用于图标。

 将分辨率保存为 96 DPI。

#### <a name="file-types"></a>文件类型

- **32 位 PNG：** 图标的首选格式。 可以存储单个光栅（像素）图像的无损数据压缩文件格式。 32 位 PNG 文件支持 alpha 通道透明度、gamma 校正和隔行扫描。

- **32 位 BMP：** 用于非 WPF 控件。 32 位 BMP（也称为 XP 或增强色）是一种 RGB/A 图像格式，是具有 alpha 通道透明度的全彩图像。 alpha 通道是 Adobe Photoshop 中指定的透明层，之后保存为位图中附加的（第四）颜色通道。 在图稿制作过程中，所有 32 位 BMP 文件都添加了黑色背景，以提供关于颜色深度的快速视觉提示。 此黑色背景表示 UI 中要遮罩的区域。

- **32 位 ICO：** 用于“项目”图标和“添加项”。 所有 ICO 文件均为 32 位全彩，具有 alpha 通道透明度 (RGB/A)。 由于 ICO 文件可以存储多种大小和颜色深度，Vista 图标通常采用 ICO 格式，其中包含 16x16、32x32、48x48 和 256x256 图像大小。 为了在 Windows 资源管理器中正确显示，ICO 文件必须针对每个图像大小保存为 24 位和 8 位颜色深度。

- **XAML：** 用于设计表面和窗口装饰器。 XAML 图标是基于矢量的图像文件，支持缩放、旋转、归档和透明度。 它们在现在的 Visual Studio 中并不常见，但由于其灵活性而变得越来越流行。

- **SVG**

- **24 位 BMP：** 用于 Visual Studio 命令栏。 全彩 RGB 图像格式、24 位 BMP 是一种图标约定，它通过使用洋红色（R=255、G=0、B=255）作为“敲除”透明层的颜色键来创建透明层。 在 24 位 BMP 中，所有洋红色表面都使用背景色显示。

- **24 位 GIF：** 用于 Visual Studio 命令栏。 支持透明度的全彩 RGB 图像格式。 GIF 文件通常用于向导图稿和 GIF 动画。

### <a name="icon-construction"></a>图标构造
 Visual Studio 中最小的图标大小为 16x16。 最常用的是 32x32。 请记住，在设计图标时，不要将 16x16、24x24 或 32x32 的帧整个填满。 清晰、统一的图标结构对于用户识别至关重要。 生成图标时请遵循以下几点。

- 图标应清晰、易懂且一致。

- 最好将状态通知元素作为单个图标使用，而不是将它们叠放在图标基本元素的顶部。 在某些上下文中，UI 可能需要让状态元素与基本元素成对出现。

- 项目图标通常是包含多种大小的 .ico 文件。 仅更新 16x16、24x24 和 32x32 图标。 大多数 16x16 和 24x24 图标包含相同的元素。 32x32 图标包含更多详细信息，适用时包括项目语言类型。

- 对于 32x32 图标，基本元素通常具有 2 像素的线条粗细。 详细信息元素可以使用 1 或 2 像素的线条粗细。 使用最佳判断来确定哪个更适合。

- 对于 16x16 和 24x24 图标，元素之间的间距至少为 1 像素。 对于 32x32 图标，在元素之间以及修饰符和基本元素之间使用 2 像素间距。

  ![大小为 16x16、24x24 和 32x32 的图标的元素间距](../../extensibility/ux-guidelines/media/0404-47_elementspacing.png "0404-47_ElementSpacing")<br />大小为 16x16、24x24 和 32x32 的图标的元素间距

#### <a name="color-and-accessibility"></a>颜色和辅助功能
 Visual Studio 符合性指南要求产品中的所有图标都满足颜色和对比度的辅助功能要求。 这是通过反转图标来实现的，当你在设计的时候，你应该意识到它们会在产品中以编程方式进行反转。

 有关在 Visual Studio 图标中使用颜色的详细信息，请参阅[在图像中使用颜色](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)。

## <a name="using-color-in-images"></a><a name="BKMK_UsingColorInImages"></a>在图像中使用颜色

### <a name="overview"></a>概述
 Visual Studio 中的图标主要采用单色。 颜色的作用是传达特定信息，而不是作为装饰。 使用颜色：

- 来指示操作

- 提示用户查看状态通知

- 指定语言关联

- 区分 IntelliSense 内的项

### <a name="accessibility"></a>可访问性
 Visual Studio 符合性指南要求已签入到产品中的所有图标都满足颜色和对比度的辅助功能要求。 视觉语言调色板中的颜色已经过测试并满足这些要求。

#### <a name="color-inversion-for-dark-themes"></a>深色主题的颜色反转
 为了使图标在 Visual Studio 深色主题中以正确的对比度显示，将以编程方式应用反转。 本指南中的颜色已部分选定，以便正确地进行反转。 将颜色的使用限于此调色板，否则在应用反转时将出现不可预测的结果。

 ![颜色反转的图标示例](../../extensibility/ux-guidelines/media/0405-01_darkthemeinversion.png "0405-01_DarkThemeInversion")<br />颜色反转的图标示例

### <a name="base-palette"></a>基本调色板
 所有标准图标都包含三种基本颜色。 图标不包含渐变或阴影，但 3D 工具图标有一个或两个例外。

|使用情况|名称|值（浅色主题）|样本|示例|
|-----------|----------|---------------------------|------------|-------------|
|背景/深色|VS BG|424242 / 66,66,66|![样本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|![基调色板示例](../../extensibility/ux-guidelines/media/0405-02_basepaletteexample.png "0405-02_BasePaletteExample")|
|前景/浅色|VS FG|F0EFF1 / 240,239,241|![样本 F0EFF1](../../extensibility/ux-guidelines/media/0405_f0eff1.png "0405_F0EFF1")||
|轮廓|VS Out|F6F6F6 / 246,246,246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")||

 除了基本颜色外，每个图标可能包含扩展调色板中的一种附加颜色。

### <a name="extended-palette"></a>扩展调色板

#### <a name="action-modifiers"></a>操作修饰符
 以下四种颜色表示操作修饰符所需的操作类型：

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|正|VS 绿色操作|388A34 / 56,138,52|![样本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|负数|VS 红色操作|A1260D / 161,38,13|![样本 A1260D](../../extensibility/ux-guidelines/media/0405_a1260d.png "0405_A1260D")|
|中立|VS 蓝色操作|00539C / 0,83,156|![样本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|创建/新建|VS 橙色操作|C27D1A / 194,156,26|![样本 C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>示例
 绿色用于正操作修饰符，如“添加”、“运行”、“播放”和“验证”。

|运行|执行查询|播放所有步骤|添加控件|
|-|-|-|-|
|![“运行”图标](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")|![“执行查询”图标](../../extensibility/ux-guidelines/media/0405-04_executequery.png "0405-04_ExecuteQuery")|![“播放所有步骤”图标](../../extensibility/ux-guidelines/media/0405-05_playallsteps.png "0405-05_PlayAllSteps")|![“添加控件”图标](../../extensibility/ux-guidelines/media/0405-06_addcontrol.png "0405-06_AddControl")|

 红色用于负操作修饰符，如“删除”、“停止”、“取消”和“关闭”。

|删除关系|删除列|停止查询|连接离线|
|-|-|-|-|
|![“删除关系”图标](../../extensibility/ux-guidelines/media/0405-07_deleterelationship.png "0405-07_DeleteRelationship")|![“删除列”图标](../../extensibility/ux-guidelines/media/0405-08_deletecolumn.png "0405-08_DeleteColumn")|![“停止查询”图标](../../extensibility/ux-guidelines/media/0405-09_stopquery.png "0405-09_StopQuery")|![“连接离线”图标](../../extensibility/ux-guidelines/media/0405-10_connectionoffline.png "0405-10_ConnectionOffline")|

 蓝色用于中性操作修饰符，最常用箭头表示，如“打开”、“下一个”、“上一个”、“导入”和“导出”。

|转到字段|批量签入|地址编辑器|关联编辑器|
|-|-|-|-|
|![“转到字段”图标](../../extensibility/ux-guidelines/media/0405-11_gotofield.png "0405-11_GoToField")|![“批量签入”图标](../../extensibility/ux-guidelines/media/0405-12_batchedcheckin.png "0405-12_BatchedCheckIn")|![“地址编辑器”图标](../../extensibility/ux-guidelines/media/0405-13_addresseditor.png "0405-13_AddressEditor")|![“关联编辑器”图标](../../extensibility/ux-guidelines/media/0405-14_associationeditor.png "0405-14_AssociationEditor")|

 暗金色主要用于“新建”修饰符。

|新建项目|创建新关系图|新建单元测试|新建列表项|
|-|-|-|-|
|![“新建项目”图标](../../extensibility/ux-guidelines/media/0405-15_newproject.png "0405-15_NewProject")|![“创建新关系图”图标](../../extensibility/ux-guidelines/media/0405-16_createnewgraph.png "0405-16_CreateNewGraph")|![“新建单元测试”图标](../../extensibility/ux-guidelines/media/0405-17_newunittest.png "0405-17_NewUnitTest")|![“新建列表项”图标](../../extensibility/ux-guidelines/media/0405-18_newlistitem.png "0405-18_NewListItem")|

#### <a name="special-cases"></a>特殊情况
 在特殊情况下，彩色操作修饰符可以作为独立图标单独使用。 图标使用的颜色反映了与图标关联的操作。 这种使用仅限于图标的一小部分，包括：

|运行|停止|删除|保存|向后导航|
|-|-|-|-|-|
|![“运行”图标](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")|![停止图标 - 实心红色正方形。](../../extensibility/ux-guidelines/media/0405-19_stop.png "0405-19_Stop")|![删除图标](../../extensibility/ux-guidelines/media/0405-20_delete.png "0405-20_Delete")|![“保存”图标](../../extensibility/ux-guidelines/media/0405-21_save.png "0405-21_Save")|![“向后导航”图标](../../extensibility/ux-guidelines/media/0405-22_navigateback.png "0405-22_NavigateBack")|

### <a name="code-hierarchy-palette"></a>代码层次结构调色板

#### <a name="folder"></a>Folder

|使用情况|名称|值（所有主题）|样本|示例|
|-----------|----------|--------------------------|------------|-------------|
|文件夹|Folder|DCB67A / 220,182,122|![样本 DCB67A](../../extensibility/ux-guidelines/media/0405_dcb67a.png "0405_DCB67A")|![“文件夹颜色”图标](../../extensibility/ux-guidelines/media/0405-23_foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio 语言
 Visual Studio 中提供的每个常见语言或平台都有关联的颜色。 这些颜色用于基础图标，或用于复合图标右上角的语言修饰符上。

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|ASP、HTML、WPF|ASP HTML WPF 蓝色|0095D7 / 0,149,215|![样本 0095D7](../../extensibility/ux-guidelines/media/0405_0096d7.png "0405_0096D7")|
|C++|CPP 紫色|9B4F96 / 155,79,150|![样本 9B4F96](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|C#|CS 绿色（VS 绿色操作）|388A34 / 56,138,52|![样本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|CSS|CSS 红色|BD1E2D / 189,30,45|![样本 BD1E2D](../../extensibility/ux-guidelines/media/0405_bd1e2d.png "0405_BD1E2D")|
|F#|FS 紫色|672878 / 103,40,120|![样本 672878](../../extensibility/ux-guidelines/media/0405_672878.png "0405_672878")|
|Javascript|JS 橙色|F16421 / 241,100,33|![样本 F16421](../../extensibility/ux-guidelines/media/0405_f16421.png "0405_F16421")|
|VB|VB 蓝色（VS 蓝色操作）|00539C / 0,83,156|![样本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|TypeScript|TS 橙色|E04C06 / 224,76,6|![样本 E04C06](../../extensibility/ux-guidelines/media/0405_e04c06.png "0405_E04C06")|
|Python|PY 绿色|879636 / 135,150,54|![样本 879636](../../extensibility/ux-guidelines/media/0405_879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>带有语言修饰符的图标示例

|VB|C#|F#|JavaScript|Python|
|-|-|-|-|-|-|
|!["Visual Basic" 图标](../../extensibility/ux-guidelines/media/0405-25_vb.png "0405-25_VB")|![C&#35; 图标](../../extensibility/ux-guidelines/media/0405-26_csharp.png "0405-26_CSharp")|![C&#43;&#43; 图标](../../extensibility/ux-guidelines/media/0405-27_cplusplus.png "0405-27_CPlusPlus")|![F&#35; 图标](../../extensibility/ux-guidelines/media/0405-28_fsharp.png "0405-28_FSharp")|!["JavaScript" 图标](../../extensibility/ux-guidelines/media/0405-29_javascript.png "0405-29_JavaScript")|!["Python" 图标](../../extensibility/ux-guidelines/media/0405-30_python.png "0405-30_Python")|

|HTML|WPF|ASP|CSS|TypeScript|
|-|-|-|-|-|-|
|!["HTML" 图标](../../extensibility/ux-guidelines/media/0405-31_html.png "0405-31_HTML")<br />HTML|!["WPF" 图标](../../extensibility/ux-guidelines/media/0405-32_wpf.png "0405-32_WPF")<br />WPF|!["ASP" 图标](../../extensibility/ux-guidelines/media/0405-33_asp.png "0405-33_ASP")<br />ASP|!["CSS" 图标](../../extensibility/ux-guidelines/media/0405-34_css.png "0405-34_CSS")<br />CSS|!["TypeScript" 图标](../../extensibility/ux-guidelines/media/0405-35_typescript.png "0405-35_TypeScript")<br />TypeScript||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense 图标使用专用调色板。 这些颜色用于帮助用户快速区分 IntelliSense 弹出列表中的不同项。

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|类、事件|VS 橙色操作|C27D1A / 194,125,26|![样本 C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|
|扩展方法、方法、模块、委托|VS 紫色操作|652D90 / 101,45,144|![样本 652D90](../../extensibility/ux-guidelines/media/0405_652d90.png "0405_652D90")|
|字段、枚举项、宏、结构、联合值类型、运算符、接口|VS 蓝色操作|00539C / 0,83,156|![样本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|对象|VS 绿色操作|388A34 / 56,138,52|![样本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|常数、异常、枚举项、映射、映射项、命名空间、模板、类型定义|背景 (VS BG)|424242 / 66,66,66|![样本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense 图标示例

|类|私有事件|委托|方法好友|字段|
|-|-|-|-|-|
|![“IntelliSense 类”图标](../../extensibility/ux-guidelines/media/0405-36_intellisenseclass.png "0405-36_IntelliSenseClass")|![“IntelliSense 私有事件”图标](../../extensibility/ux-guidelines/media/0405-37_intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")|![“IntelliSense 委托”图标](../../extensibility/ux-guidelines/media/0405-38_intellisensedelegate.png "0405-38_IntelliSenseDelegate")|![“IntelliSense 方法好友”图标](../../extensibility/ux-guidelines/media/0405-39_intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")|![字段图标](../../extensibility/ux-guidelines/media/0405-40_field.png "0405-40_Field")|

|受保护的枚举项|对象|模板|异常快捷方式|
|-|-|-|-|
|![“IntelliSense 受保护的枚举项”图标](../../extensibility/ux-guidelines/media/0405-41_intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")|![“IntelliSense 对象”图标](../../extensibility/ux-guidelines/media/0405-42_intellisenseobject.png "0405-42_IntelliSenseObject")|![“IntelliSense 模板”图标](../../extensibility/ux-guidelines/media/0405-43_intellisensetemplate.png "0405-43_IntelliSenseTemplate")|![“IntelliSense 异常快捷方式”图标](../../extensibility/ux-guidelines/media/0405-44_intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")|

### <a name="notifications"></a>通知
 Visual Studio 中的通知用于指示状态。 “通知”调色板使用以下四种颜色以及黑色或白色前景填充选项来定义具有以下状态级别的通知。

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|状态：中性|蓝色通知（VS 蓝色）|1BA1E2 / 27,161,226|![样本 1BA1E2](../../extensibility/ux-guidelines/media/0405_1ba1e2.png "0405_1BA1E2")|
|状态：正|绿色通知（VS 绿色）|339933 / 51,153,51|![样本 339933](../../extensibility/ux-guidelines/media/0405_339933.png "0405_339933")|
|状态：负|红色通知（VS 红色）|E51400 / 229,20,0|![样本 E51400](../../extensibility/ux-guidelines/media/0405_e51400.png "0405_E51400")|
|状态：警告|黄色通知（VS 橙色）|FFCC00 / 255,204,0|![样本 FFCC00](../../extensibility/ux-guidelines/media/0405_ffcc00.png "0405_FFCC00")|
|前景填充|黑色通知（黑色）|000000 / 0,0,0|![样本 &#35;000000](../../extensibility/ux-guidelines/media/0405_000000.png "0405_000000")|
|前景填充|白色通知（白色）|FFFFFF / 255,255,255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知图标示例

|警报|警告|完成|停止|
|-|-|-|-|
|![警报图标](../../extensibility/ux-guidelines/media/0405-45_alert.png "0405-45_Alert")|![警告图标](../../extensibility/ux-guidelines/media/0405-48_warning.png "0405-48_Warning")|![“完成”图标](../../extensibility/ux-guidelines/media/0405-46_complete.png "0405-46_Complete")|![停止图标 - 实心红色的圆中有一个白色正方形。](../../extensibility/ux-guidelines/media/0405-47_stop.png "0405-47_Stop")|