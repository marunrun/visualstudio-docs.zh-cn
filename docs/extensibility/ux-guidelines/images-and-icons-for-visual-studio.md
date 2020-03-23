---
title: 视觉工作室的图像和图标 |微软文档
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1e449fb30bd95319a46d1db50da63778f6800a70
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301595"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio 的图像和图标
## <a name="image-use-in-visual-studio"></a><a name="BKMK_ImageUseInVisualStudio"></a>视觉工作室中的图像使用
 在创建图稿之前，请考虑使用[Visual Studio 图像库中](https://www.microsoft.com/download/details.aspx?id=35825)的 1，000 多张图片。

### <a name="types-of-images"></a>图像类型

- **图标**. 出现在命令、层次结构、模板等中的小图像。 Visual Studio 中使用的默认图标大小为 16x16 PNG。 影像服务生成的图标会自动生成 XAML 格式，用于 HDPI 支持。

    > [!NOTE]
    > 当图像在菜单系统中使用时，不应为每个命令创建图标。 请参阅[Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)，查看命令是否应获得图标。

- **缩略 图。** 对话框的预览区域（如"新项目"对话框）中使用的图像。

- **对话框图像。** 以描述性图形或消息指示器显示在对话框或向导中的图像。 很少使用，且仅在必要时才用于说明一个困难的概念或引起用户的注意（警报、警告）。

- **动画图像。** 用于进度指示器、状态栏和操作对话框。

- **游标。** 用于指示是否允许使用鼠标操作、可能丢弃对象的位置等。

## <a name="icon-design"></a><a name="BKMK_IconDesign"></a>图标设计

### <a name="overview"></a>概述
 Visual Studio 使用现代风格的图标，这些图标具有干净的几何形状和 50/50 的正/负（浅色/暗数）平衡，并使用直接、可理解的隐喻。 关键图标设计点围绕清晰度、简化和上下文。

- **清晰度：** 关注核心隐喻，赋予图标其意义和个性。

- **简化：** 将图标减小到其核心含义 - 只需必要的元素即可将主题与无褶边。

- **上下文：** 在概念开发过程中考虑图标角色的所有方面，这在决定哪些元素构成图标的核心隐喻时至关重要。

  使用图标，有许多设计点需要避免：

- 除非适用，否则不要使用表示 UI 元素的图标。 当 UI 元素既不常见、明显也不唯一时，请选择更抽象或符号化的方法。

- 不要过度使用文档、文件夹、箭头和放大镜等常见元素。 仅当图标的含义至关重要时，才使用这些元素。 例如，右侧的放大镜应仅指示搜索、浏览和查找。

- 尽管某些旧图标元素保持透视的使用，但除非没有透视，则不要创建具有透视的新图标，除非该元素缺乏清晰度。

- 不要将太多信息塞进图标中。 一个简单的图像，可以很容易地识别或学习为可识别的符号比过于复杂的图像更有用。 图标无法讲述整个故事。

### <a name="icon-creation"></a>图标创建

#### <a name="concept-development"></a>概念开发
 Visual Studio 在其 UI 中具有多种图标类型。 在开发过程中仔细考虑图标类型。 不要对图标元素使用不明确或不常见的 UI 对象。 在这些情况下，例如使用智能标记图标，请选择符号。 请注意，左侧抽象标记的含义比右侧模糊的基于 UI 的版本更明显：

|||
|-|-|
|**正确使用符号图像**|**符号图像使用不正确**|
|![正确的“智能标记”图标](../../extensibility/ux-guidelines/media/0404-01_smarttagcorrect.png "0404-01_SmartTagCorrect")|![不正确的“智能标记”图标](../../extensibility/ux-guidelines/media/0404-02_smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 在某些情况下，标准、易于识别的 UI 元素对图标工作良好。 添加窗口就是一个示例：

|||
|-|-|
|**图标中更正 UI 元素**|**图标中的 UI 元素不正确**|
|![正确的“添加窗口”图标](../../extensibility/ux-guidelines/media/0404-03_addwindowcorrect.png "0404-03_AddWindowCorrect")|![不正确的“添加窗口”图标](../../extensibility/ux-guidelines/media/0404-04_addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 不要将文档用作基本元素，除非文档对图标的含义至关重要。 如果没有 Add Document 上的文档元素（下图），含义将丢失，而使用"刷新"时，文档元素就不必传达含义。

|||
|-|-|
|**正确使用文档图标**|**文档图标使用不正确**|
|![正确的“文档”图标](../../extensibility/ux-guidelines/media/0404-05_documenticoncorrect.png "0404-05_DocumentIconCorrect")|![不正确的“文档”图标](../../extensibility/ux-guidelines/media/0404-06_documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 "show"的概念应该由最能说明显示内容的图标表示，例如使用"显示所有文件"示例。 如有必要，可以使用镜头隐喻来指示"视图"的概念，例如使用资源视图示例。

|||
|-|-|
|**"显示"**|**"查看"**|
|![“显示”图标](../../extensibility/ux-guidelines/media/0404-07_show.png "0404-07_Show")|![“查看”图标](../../extensibility/ux-guidelines/media/0404-08_view.png "0404-08_View")|

 右侧的放大镜图标应仅表示搜索、查找和浏览。 带有加号或减号的左侧变体应仅表示放大/缩小。

|||
|-|-|
|**"搜索"**|**"缩放"**|
|![搜索图标](../../extensibility/ux-guidelines/media/0404-09_search.png "0404-09_Search")|![缩放图标](../../extensibility/ux-guidelines/media/0404-10_zoom.png "0404-10_Zoom")|

 在树视图中，不要同时使用文件夹图标和修改器。 如果可用，则仅使用修改器。

|||
|-|-|
|**正确的树视图图标**|**树视图图标不正确**|
|![正确树视图图标&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11_treeviewcorrect1.png "0404-11_TreeViewCorrect1") ![正确树视图图标&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12_treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![树视图图标&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13_treeviewincorrect1.png "0404-13_TreeViewIncorrect1") ![不正确的树视图图标&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14_treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>样式详细信息

#### <a name="layout"></a>布局
 堆栈元素，如标准 16x16 图标所示：

 ![16x16 图标的布局堆栈](../../extensibility/ux-guidelines/media/0404-15_layoutstack.png "0404-15_LayoutStack")<br />16x16 图标的布局堆栈

 状态通知元素更好地用作独立图标。 但是，在某些情况下，通知应堆叠在基本元素上，例如使用"任务完成"图标：

 ![Visual Studio 中的独立通知](../../extensibility/ux-guidelines/media/0404-16_standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")<br />独立通知图标

 ![“任务完成”图标](../../extensibility/ux-guidelines/media/0404-17_taskcomplete.png "0404-17_TaskComplete")<br />任务完成图标

 项目图标通常是包含多个大小的 .ico 文件。 大多数 16x16 图标包含相同的元素。 32x32 版本具有更多详细信息，包括项目类型（如果适用）。

 ![Visual Studio 中的“项目”图标](../../extensibility/ux-guidelines/media/0404-18_iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")<br />VB Windows 控制库项目图标，16x16 和 32x32

 将图标居其像素帧中居中。 如果无法这样做，则将图标对齐到框架的顶部和/或右侧。

 ![图标在像素框架中居中](../../extensibility/ux-guidelines/media/0404-19_iconcentered.png "0404-19_IconCentered")<br />图标在像素框架中居中

 ![图标与像素框架的右上方对齐](../../extensibility/ux-guidelines/media/0404-20_icontopright.png "0404-20_IconTopRight")<br />与框架右上角对齐的图标

 ![图标居中并与像素框架的顶部对齐](../../extensibility/ux-guidelines/media/0404-21_icontopalign.png "0404-21_IconTopAlign")<br />图标居中并对齐到框架顶部

 要实现理想的对齐和平衡，请避免用动作字形阻挡图标的基本元素。 将字形放在基元素左上角附近。 添加附加元素时，请考虑图标的对齐和平衡。

|||
|-|-|
|**正确的对齐和平衡**|**对齐和平衡不正确**|
|![正确的图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-22_alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![不正确的图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-23_alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 确保共享元素并在集中使用的图标的大小奇偶校验。 请注意，在不正确的配对中，圆圈和箭头大小过大且不匹配。

|||
|-|-|
|**正确的大小奇偶校验**|**大小奇偶校验不正确**|
|![正确的图标的大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-24_sizeparitycorrect.png "0404-24_SizeParityCorrect")|![不正确的图标的大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-25_sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 使用一致的线条和视觉权重。 使用并排比较评估要构建的图标与其他图标的比较情况。 切勿使用整个 16x16 帧，使用 15x15 或更小。 负对正（暗对光）比应为50/50。

|||
|-|-|
|**正确的负正比率**|**不正确的负正比率**|
|![&#40;1&#41;图标的正确视觉权重](../../extensibility/ux-guidelines/media/0404-26_visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![图标&#40;2&#41;的正确视觉权重](../../extensibility/ux-guidelines/media/0404-27_visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![&#40;3&#41;图标的正确视觉权重](../../extensibility/ux-guidelines/media/0404-28_visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![不正确的图标视觉重量](../../extensibility/ux-guidelines/media/0404-29_visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 使用简单、可比较的形状和互补的角度构建元素，而不会牺牲元素的完整性。 尽可能使用 45° 或 90° 角度。

 ![正确的图标角度](../../extensibility/ux-guidelines/media/0404-30_iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>透视
 保持图标清晰且易于理解。 仅在必要时使用透视和光源。 尽管应避免对图标元素使用透视，但某些元素在没有它的情况下是无法识别的。 在这种情况下，样式化的透视图传达元素的清晰度。

 ![3 点透视图](../../extensibility/ux-guidelines/media/0404-31_3pointperspective.png "0404-31_3PointPerspective")<br />3 点透视图

 ![1 点透视图](../../extensibility/ux-guidelines/media/0404-32_1pointperspective.png "0404-32_1PointPerspective")<br />1 点透视图

 大多数元素应朝向或向右倾斜：

 ![向右倾斜的图标](../../extensibility/ux-guidelines/media/0404-33_angledright.png "0404-33_AngledRight")

 仅当向对象添加必要的清晰度时，才使用光源。

|||
|-|-|
|**正确的光源**|**光源不正确**|
|![正确的图标光源](../../extensibility/ux-guidelines/media/0404-34_lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![不正确的图标光源](../../extensibility/ux-guidelines/media/0404-35_lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 使用轮廓只是为了增强可读性或更好地传达隐喻。 负正（暗光）余额应为 50/50。

|||
|-|-|
|**正确使用轮廓**|**不正确使用轮廓**|
|![正确的轮廓](../../extensibility/ux-guidelines/media/0404-36_outlinescorrect.png "0404-36_OutlinesCorrect")|![不正确的轮廓](../../extensibility/ux-guidelines/media/0404-37_outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>图标类型
 **命令程序单图标**由以下三个元素组成：一个基、一个修改器、一个操作或一个状态。

 ![外壳和命令栏图标的示例](../../extensibility/ux-guidelines/media/0404-38_shellicons.png "0404-38_ShellIcons")<br />外壳和命令栏图标的示例

 **工具窗口命令栏**图标由以下元素中的三个组成：一个基、一个修改器、一个操作或一个状态。

 ![工具窗口命令栏图标的示例](../../extensibility/ux-guidelines/media/0404-39_toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")<br />工具窗口命令栏图标的示例

 **树视图消除歧义图标**由以下元素中的三个组成：一个基、一个修改器、一个操作或一个状态。

 ![树视图消除歧义图标的示例](../../extensibility/ux-guidelines/media/0404-40_treeviewicons.png "0404-40_TreeViewIcons")<br />树视图消除歧义图标的示例

 **基于状态的值分类**图标存在以下状态：活动、活动禁用和非活动禁用。

 ![基于状态的值分类图标示例](../../extensibility/ux-guidelines/media/0404-41_statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")<br />基于状态的值分类图标示例

 **IntelliSense**图标包含以下元素中的三个：一个基体、一个修改器和一个状态。

 ![IntelliSense 图标示例](../../extensibility/ux-guidelines/media/0404-42_intellisenseicons.png "0404-42_IntelliSenseIcons")<br />IntelliSense 图标示例

 **小型 （16x16） 项目**图标不应具有两个元素：一个基和一个修饰符。

 ![小型 （16x16） 项目图标](../../extensibility/ux-guidelines/media/0404-43_16x16project1.png "0404-43_16x16Project1") ![16x16 项目图标&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44_16x16project2.png "0404-44_16x16Project2") ![16x16 项目图标&#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45_16x16project3.png "0404-45_16x16Project3")<br />小型 （16x16） 项目图标示例

 **大型 （32x32） 项目**图标由以下元素中的四个组成：一个基体、一个到两个修饰符和一个语言叠加。

 ![大型 （32x32） 项目图标示例](../../extensibility/ux-guidelines/media/0404-46_32x32project.png "0404-46_32x32Project")<br />大型 （32x32） 项目图标示例

### <a name="production-details"></a>生产详细信息
 所有新的 UI 元素都应使用 Windows 演示文稿基础 （WPF） 创建，WPF 的所有新图标应采用 32 位 PNG 格式。 24 位 PNG 是一种不支持透明度的旧版格式，因此不推荐用于图标。

 将分辨率保存在 96 DPI。

#### <a name="file-types"></a>文件类型

- **32 位 PNG：** 图标的首选格式。 可存储单个栅格（像素）图像的无损数据压缩文件格式。 32 位 PNG 文件支持 alpha 通道透明度、伽马校正和隔行扫描。

- **32 位 BMP：** 用于非 WPF 控件。 32 位 BMP 也称为 XP 或高颜色，是 RGB/A 图像格式，是具有 alpha 通道透明度的真实彩色图像。 alpha 通道是在 Adobe Photoshop 中指定的一层透明度，然后作为附加（第四个）颜色通道保存在位图中。 在图稿制作期间，黑色背景将添加到所有 32 位 BMP 文件中，以提供有关颜色深度的快速视觉提示。 此黑色背景表示要在 UI 中屏蔽的区域。

- **32 位 ICO：** 用于项目图标和添加项目。 所有 ICO 文件都是具有 alpha 通道透明度 （RGB/A） 的 32 位真颜色。 由于 ICO 文件可以存储多种尺寸和颜色深度，Vista 图标通常采用 ICO 格式，包含 16x16、32x32、48x48 和 256x256 图像大小。 为了在 Windows 资源管理器中正确显示，ICO 文件必须为每个图像大小保存为 24 位和 8 位颜色深度。

- **XAML：** 用于设计曲面和 Windows 装饰器。 XAML 图标是基于矢量的图像文件，支持缩放、旋转、归档和透明度。 它们在视觉工作室中并不常见，但由于它们的灵活性而越来越受欢迎。

- **SVG**

- **24 位 BMP：** 用于可视化工作室命令栏。 24 位 BMP 是一种真实彩色 RGB 图像格式，它是一种图标约定，它使用洋红色 （R=255、G=0、 B=255） 作为仿冒透明度图层的颜色键来创建透明度层。 在 24 位 BMP 中，所有洋红色曲面都使用背景颜色显示。

- **24 位 GIF：** 用于可视化工作室命令栏。 支持透明度的真彩色 RGB 图像格式。 GIF 文件通常用于向导图稿和 GIF 动画。

### <a name="icon-construction"></a>图标结构
 Visual Studio 中最小的图标大小为 16x16。 最大的常用是32x32。 在设计图标时，请注意不要填满整个 16x16、24x24 或 32x32 帧。 清晰、均匀的图标结构对于用户识别至关重要。 构建图标时，应遵守以下几点。

- 图标应该清晰、易懂且一致。

- 最好将状态通知元素用作单个图标，而不是将它们堆叠在图标基础元素之上。 在某些上下文中，UI 可能需要状态元素与基元素配对。

- 项目图标通常是包含多个大小的 .ico 文件。 仅更新 16x16、24x24 和 32x32 图标。 大多数 16x16 和 24x24 图标将包含相同的元素。 32x32 图标包含更多详细信息，包括项目语言类型（如果适用）。

- 对于 32x32 图标，基本元素通常具有 2 像素的线粗。 1 像素或 2 像素的线粗可用于细节元素。 用你最好的判断来确定哪个更合适。

- 元素之间至少有 1 像素间距，用于 16x16 和 24x24 图标。 对于 32x32 图标，在元素之间以及修改器和基本元素之间使用 2 像素间距。

  ![大小为 16x16、24x24 和 32x32 的图标的元素间距](../../extensibility/ux-guidelines/media/0404-47_elementspacing.png "0404-47_ElementSpacing")<br />大小为 16x16、24x24 和 32x32 的图标的元素间距

#### <a name="color-and-accessibility"></a>颜色和可访问性
 Visual Studio 合规性准则要求产品中的所有图标都通过颜色和对比度的辅助功能要求。 这是通过图标反转实现的，当您正在设计时，您应该意识到它们将在产品中以编程方式反转。

 有关在视觉工作室图标中使用颜色的详细信息，请参阅[在图像中使用颜色](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)。

## <a name="using-color-in-images"></a><a name="BKMK_UsingColorInImages"></a>在图像中使用颜色

### <a name="overview"></a>概述
 视觉工作室中的图标主要是单色的。 颜色是保留以传达特定信息，永远不会用于装饰。 颜色使用：

- 指示操作

- 提醒用户状态通知

- 指定语言隶属关系

- 区分 IntelliSense 中的项目

### <a name="accessibility"></a>可访问性
 Visual Studio 合规性准则要求所有签入产品的图标都通过颜色和对比度的辅助功能要求。 视觉语言调色板中的颜色已经过测试并满足这些要求。

#### <a name="color-inversion-for-dark-themes"></a>深色主题的颜色反转
 为了使图标在 Visual Studio 黑暗主题中以正确的对比度显示，以编程方式应用反转。 本指南中的颜色部分被选中，以便它们正确反转。 将颜色的使用限制为此调色板，否则在应用反转时，您将获得不可预知的结果。

 ![颜色反转的图标示例](../../extensibility/ux-guidelines/media/0405-01_darkthemeinversion.png "0405-01_DarkThemeInversion")<br />颜色反转的图标示例

### <a name="base-palette"></a>基本调色板
 所有标准图标包含三种基本颜色。 图标不包含渐变或阴影，3D 工具图标有一个或两个例外。

|使用情况|名称|值（浅色主题）|样本|示例|
|-----------|----------|---------------------------|------------|-------------|
|背景/黑暗|VS BG|424242 / 66,66,66|![样本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|![基调色板示例](../../extensibility/ux-guidelines/media/0405-02_basepaletteexample.png "0405-02_BasePaletteExample")|
|前景/灯光|VS FG|F0EFF1 / 240，239，241|![样本 F0EFF1](../../extensibility/ux-guidelines/media/0405_f0eff1.png "0405_F0EFF1")||
|轮廓|VS 出|F6F6F6 / 246，246，246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")||

 除了基本颜色之外，每个图标可能包含扩展调色板中的一个附加颜色。

### <a name="extended-palette"></a>扩展调色板

#### <a name="action-modifiers"></a>操作修改器
 以下四种颜色指示操作修改器所需的操作类型：

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|正|VS 动作绿色|388A34 / 56，138，52|![样本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|负|VS 动作红色|A1260D / 161，38，13|![样本 A1260D](../../extensibility/ux-guidelines/media/0405_a1260d.png "0405_A1260D")|
|中立|VS 动作蓝色|00539C / 0，83，156|![样本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|创建/新建|VS 动作橙色|C27D1A / 194，156，26|![样本 C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>示例
 绿色用于积极动作修改符，如"添加"、"运行"、"播放"和"验证"。

|||||
|-|-|-|-|
|![“运行”图标](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")<br />运行|![“执行查询”图标](../../extensibility/ux-guidelines/media/0405-04_executequery.png "0405-04_ExecuteQuery")<br />执行查询|![“播放所有步骤”图标](../../extensibility/ux-guidelines/media/0405-05_playallsteps.png "0405-05_PlayAllSteps")<br />播放所有步骤|![“添加控件”图标](../../extensibility/ux-guidelines/media/0405-06_addcontrol.png "0405-06_AddControl")<br />添加控件|

 红色用于否定动作修改符，如"删除"、"停止"、"取消"和"关闭"。

|||||
|-|-|-|-|
|![“删除关系”图标](../../extensibility/ux-guidelines/media/0405-07_deleterelationship.png "0405-07_DeleteRelationship")<br />删除关系|![“删除列”图标](../../extensibility/ux-guidelines/media/0405-08_deletecolumn.png "0405-08_DeleteColumn")<br />删除列|![“停止查询”图标](../../extensibility/ux-guidelines/media/0405-09_stopquery.png "0405-09_StopQuery")<br />停止查询|![“连接离线”图标](../../extensibility/ux-guidelines/media/0405-10_connectionoffline.png "0405-10_ConnectionOffline")<br />连接脱机|

 蓝色应用于最常表示为箭头的中性动作修改器，如"打开"、"下一步"、"上一个"、"导入"和"导出"。

|||||
|-|-|-|-|
|![“转到字段”图标](../../extensibility/ux-guidelines/media/0405-11_gotofield.png "0405-11_GoToField")<br />转到字段|![&#45;图标中批量检查](../../extensibility/ux-guidelines/media/0405-12_batchedcheckin.png "0405-12_BatchedCheckIn")<br />批处理签入|![“地址编辑器”图标](../../extensibility/ux-guidelines/media/0405-13_addresseditor.png "0405-13_AddressEditor")<br />地址编辑器|![“关联编辑器”图标](../../extensibility/ux-guidelines/media/0405-14_associationeditor.png "0405-14_AssociationEditor")<br />关联编辑器|

 深色主要用于"新建"修改器。

|||||
|-|-|-|-|
|![“新建项目”图标](../../extensibility/ux-guidelines/media/0405-15_newproject.png "0405-15_NewProject")<br />新建项目|![“创建新关系图”图标](../../extensibility/ux-guidelines/media/0405-16_createnewgraph.png "0405-16_CreateNewGraph")<br />创建新图形|![“新建单元测试”图标](../../extensibility/ux-guidelines/media/0405-17_newunittest.png "0405-17_NewUnitTest")<br />新单元测试|![“新建列表项”图标](../../extensibility/ux-guidelines/media/0405-18_newlistitem.png "0405-18_NewListItem")<br />新建列表项|

#### <a name="special-cases"></a>特殊情况
 在特殊情况下，彩色动作修改器可以单独用作独立图标。 用于图标的颜色反映图标关联的操作。 此使用仅限于图标的一小部分，包括：

||||||
|-|-|-|-|-|
|![“运行”图标](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")<br />运行|![“停止”图标](../../extensibility/ux-guidelines/media/0405-19_stop.png "0405-19_Stop")<br />停止|![删除图标](../../extensibility/ux-guidelines/media/0405-20_delete.png "0405-20_Delete")<br />删除|![“保存”图标](../../extensibility/ux-guidelines/media/0405-21_save.png "0405-21_Save")<br />保存|![“向后导航”图标](../../extensibility/ux-guidelines/media/0405-22_navigateback.png "0405-22_NavigateBack")<br />向后导航|

### <a name="code-hierarchy-palette"></a>代码层次结构调色板

#### <a name="folder"></a>Folder

|使用情况|名称|值（所有主题）|样本|示例|
|-----------|----------|--------------------------|------------|-------------|
|Folders|Folder|DCB67A / 220，182，122|![样本 DCB67A](../../extensibility/ux-guidelines/media/0405_dcb67a.png "0405_DCB67A")|![“文件夹颜色”图标](../../extensibility/ux-guidelines/media/0405-23_foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>视觉工作室语言
 Visual Studio 中提供的每个通用语言或平台都有关联的颜色。 这些颜色用于基本图标，或出现在复合图标右上角的语言修饰符上。

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|ASP， HTML， WPF|ASP HTML WPF 蓝色|0095D7 / 0，149，215|![样本 0095D7](../../extensibility/ux-guidelines/media/0405_0096d7.png "0405_0096D7")|
|C++|CPP 紫色|9B4F96 / 155，79，150|![样本 9B4F96](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|C#|CS 绿色 （VS 动作绿色）|388A34 / 56，138，52|![样本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|CSS|CSS 红色|BD1E2D / 189，30，45|![样本 BD1E2D](../../extensibility/ux-guidelines/media/0405_bd1e2d.png "0405_BD1E2D")|
|F#|FS 紫色|672878 / 103,40,120|![样本 672878](../../extensibility/ux-guidelines/media/0405_672878.png "0405_672878")|
|JavaScript|JS 橙色|F16421 / 241，100，33|![样本 F16421](../../extensibility/ux-guidelines/media/0405_f16421.png "0405_F16421")|
|VB|VB 蓝色 （VS 动作蓝）|00539C / 0，83，156|![样本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|TypeScript|TS 橙色|E04C06 / 224，76，6|![样本 E04C06](../../extensibility/ux-guidelines/media/0405_e04c06.png "0405_E04C06")|
|Python|PY 绿色|879636 / 135,150,54|![样本 879636](../../extensibility/ux-guidelines/media/0405_879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>带有语言修饰符的图标示例

|||||||
|-|-|-|-|-|-|
|!["Visual Basic" 图标](../../extensibility/ux-guidelines/media/0405-25_vb.png "0405-25_VB")<br />VB|![C&#35;图标](../../extensibility/ux-guidelines/media/0405-26_csharp.png "0405-26_CSharp")<br />C#|![C&#43;&#43; 图标](../../extensibility/ux-guidelines/media/0405-27_cplusplus.png "0405-27_CPlusPlus")<br />C++|![F&#35;图标](../../extensibility/ux-guidelines/media/0405-28_fsharp.png "0405-28_FSharp")<br />F#|!["JavaScript" 图标](../../extensibility/ux-guidelines/media/0405-29_javascript.png "0405-29_JavaScript")<br />JavaScript|!["Python" 图标](../../extensibility/ux-guidelines/media/0405-30_python.png "0405-30_Python")<br />Python|
|!["HTML" 图标](../../extensibility/ux-guidelines/media/0405-31_html.png "0405-31_HTML")<br />HTML|!["WPF" 图标](../../extensibility/ux-guidelines/media/0405-32_wpf.png "0405-32_WPF")<br />WPF|!["ASP" 图标](../../extensibility/ux-guidelines/media/0405-33_asp.png "0405-33_ASP")<br />ASP|!["CSS" 图标](../../extensibility/ux-guidelines/media/0405-34_css.png "0405-34_CSS")<br />CSS|!["TypeScript" 图标](../../extensibility/ux-guidelines/media/0405-35_typescript.png "0405-35_TypeScript")<br />TypeScript||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense 图标使用独占调色板。 这些颜色用于帮助用户快速区分 IntelliSense 弹出窗口中的不同项。

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|类， 事件|VS 动作橙色|C27D1A / 194，125，26|![样本 C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|
|扩展方法、方法、模块、委托|VS 动作紫色|652D90 / 101，45，144|![样本 652D90](../../extensibility/ux-guidelines/media/0405_652d90.png "0405_652D90")|
|字段， 枚举项， 宏， 结构， 联合值类型， 运算符， 接口|VS 动作蓝色|00539C / 0，83，156|![样本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|Object|VS 动作绿色|388A34 / 56，138，52|![样本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|常量、 异常、 枚举项、 映射、 地图项、 命名空间、 模板、 类型定义|背景 （VS BG）|424242 / 66,66,66|![样本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense 图标示例

||||||
|-|-|-|-|-|
|![“IntelliSense 类”图标](../../extensibility/ux-guidelines/media/0405-36_intellisenseclass.png "0405-36_IntelliSenseClass")<br />类|![“IntelliSense 私有事件”图标](../../extensibility/ux-guidelines/media/0405-37_intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")<br />私人活动|![“IntelliSense 委托”图标](../../extensibility/ux-guidelines/media/0405-38_intellisensedelegate.png "0405-38_IntelliSenseDelegate")<br />委托|![“IntelliSense 方法好友”图标](../../extensibility/ux-guidelines/media/0405-39_intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")<br />方法朋友|![字段图标](../../extensibility/ux-guidelines/media/0405-40_field.png "0405-40_Field")<br />字段|
|![“IntelliSense 受保护的枚举项”图标](../../extensibility/ux-guidelines/media/0405-41_intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")<br />受保护的枚举项|![“IntelliSense 对象”图标](../../extensibility/ux-guidelines/media/0405-42_intellisenseobject.png "0405-42_IntelliSenseObject")<br />Object|![“IntelliSense 模板”图标](../../extensibility/ux-guidelines/media/0405-43_intellisensetemplate.png "0405-43_IntelliSenseTemplate")<br />模板|![“IntelliSense 异常快捷方式”图标](../../extensibility/ux-guidelines/media/0405-44_intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")<br />异常快捷方式||

### <a name="notifications"></a>通知
 可视化工作室中的通知用于指示状态。 通知调色板使用以下四种颜色以及黑色或白色前景填充选项来定义具有以下状态级别的通知。

|使用情况|名称|值（所有主题）|样本|
|-----------|----------|--------------------------|------------|
|状态：中性|通知蓝色 （VS 蓝色）|1BA1E2 / 27，161，226|![样本 1BA1E2](../../extensibility/ux-guidelines/media/0405_1ba1e2.png "0405_1BA1E2")|
|状态： 正|通知绿色（VS 绿色）|339933 / 51,153,51|![样本 339933](../../extensibility/ux-guidelines/media/0405_339933.png "0405_339933")|
|状态： 负|通知红色（VS 红色）|E51400 / 229，20，0|![样本 E51400](../../extensibility/ux-guidelines/media/0405_e51400.png "0405_E51400")|
|状态：警告|通知黄色（VS 橙色）|FFCC00 / 255，204，0|![样本 FFCC00](../../extensibility/ux-guidelines/media/0405_ffcc00.png "0405_FFCC00")|
|前景填充|通知黑色（黑色）|000000 / 0,0,0|![斯沃琪&#35;00000](../../extensibility/ux-guidelines/media/0405_000000.png "0405_000000")|
|前景填充|通知白色（白色）|FFFFFF / 255，255，255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知图标示例

|||||
|-|-|-|-|
|![警报图标](../../extensibility/ux-guidelines/media/0405-45_alert.png "0405-45_Alert")<br />警报|![警告图标](../../extensibility/ux-guidelines/media/0405-48_warning.png "0405-48_Warning")<br />警告|![“完成”图标](../../extensibility/ux-guidelines/media/0405-46_complete.png "0405-46_Complete")<br />完成|![“停止”图标](../../extensibility/ux-guidelines/media/0405-47_stop.png "0405-47_Stop")<br />停止|

### <a name="visual-studio-online"></a>Visual Studio Online
 通常，可视化工作室联机功能由托管在浏览器中的功能组成。 颜色在不同的环境中不同，但样式保持不变。

|组|使用情况|名称|值（所有主题）|样本|
|-----------|-----------|----------|--------------------------|------------|
|TFS|背景|TFSO BG|656565/ 101, 101, 101|![样本 656565](../../extensibility/ux-guidelines/media/0405_656565.png "0405_656565")|
|TFS|轮廓|TFSO 出|FFFFFF / 255， 255， 255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|纳帕|背景|白色|FFFFFF / 255， 255， 255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|摩纳哥|背景|白色|FFFFFF / 255， 255， 255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|F12|背景|白色|FFFFFF / 255， 255， 255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|F12|一般|F12 Grey_Primary|555555 / 85, 85, 85|![样本 555555](../../extensibility/ux-guidelines/media/0405_555555.png "0405_555555")|
|F12|悬停|F12 Blue_Hover|2279BF / 34，121，191|![样本 2279BF](../../extensibility/ux-guidelines/media/0405_2279bf.png "0405_2279BF")|
|F12|已禁用|F12 LtGrey_Disabled|阿巴巴奇 / 171，171，172|![样本 ABABAC](../../extensibility/ux-guidelines/media/0405_ababac.png "0405_ABABAC")|
|F12|悬停背景|悬停 bg|D9EBF7 / 217，235，247|![样本 D9EBF7](../../extensibility/ux-guidelines/media/0405_d9ebf7.png "0405_D9EBF7")|
|F12|按下的背景|按下 bg|B2D7F0 / 178，215，240|![样本 B2D7F0](../../extensibility/ux-guidelines/media/0405_b2d7f0.png "0405_B2D7F0")|
|F12|轮廓|VS 出|F6F6F6 / 246，246，246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")|
|F12|信息|信息|00BCF2 / 0，188，242|![样本 00BCF2](../../extensibility/ux-guidelines/media/0405_00bcf2.png "0405_00BCF2")|
|F12|警告|警告|F28300 / 242，131，0|![样本 F28300](../../extensibility/ux-guidelines/media/0405_f28300.png "0405_F28300")|
|F12|错误/负|Error_Negative|E81123 / 232，17，35|![样本 E81123](../../extensibility/ux-guidelines/media/0405_e81123.png "0405_E81123")|
|F12|开始/正|Start_Positive|009E49 / 0，158，73|![样本 009E49](../../extensibility/ux-guidelines/media/0405_009e49.png "0405_009E49")|
|F12|中断类型|中断类型|9B4F96 / 155，79，150|![样本 9B4F96](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|F12|事件标记|事件标记|A51F00 / 165，31，0|![样本 A51F00](../../extensibility/ux-guidelines/media/0405_a51f00.png "0405_A51F00")|
|F12|用户标记|用户标记|F16220 / 241，98，32|![样本 F16220](../../extensibility/ux-guidelines/media/0405_f16220.png "0405_F16220")|

#### <a name="examples-of-visual-studio-online-icons"></a>视觉工作室在线图标示例

|TFS 在线||||
|----------------|-|-|-|
|![“TFS Online 团队”图标](../../extensibility/ux-guidelines/media/0405-49_tfsonlineteam.png "0405-49_TFSOnlineTeam")<br />在线团队|![“TFS 信息”图标](../../extensibility/ux-guidelines/media/0405-50_tfsinformation.png "0405-50_TFSInformation")<br />信息|![“TFS 历史记录”图标](../../extensibility/ux-guidelines/media/0405-51_tfshistory.png "0405-51_TFSHistory")<br />历史记录|![“TFS 分支”图标](../../extensibility/ux-guidelines/media/0405-52_tfsbranch.png "0405-52_TFSBranch")<br />分支|

|纳帕||||
|----------|-|-|-|
|![“Napa 内容”图标](../../extensibility/ux-guidelines/media/0405-53_napacontent.png "0405-53_NapaContent")<br />内容|![“Napa 办公邮件”图标](../../extensibility/ux-guidelines/media/0405-54_napaofficemail.png "0405-54_NapaOfficeMail")<br />办公室邮件|!["Napa SharePoint" 图标](../../extensibility/ux-guidelines/media/0405-55_napasharepoint.png "0405-55_NapaSharePoint")<br />SharePoint|![“Napa 任务窗格”图标](../../extensibility/ux-guidelines/media/0405-56_napataskpane.png "0405-56_NapaTaskPane")<br />任务窗格|

|摩纳哥||||
|------------|-|-|-|
|![“Monaco 文件”图标](../../extensibility/ux-guidelines/media/0405-57_monacofiles.png "0405-57_MonacoFiles")<br />文件|!["Monaco Git" 图标](../../extensibility/ux-guidelines/media/0405-58_monacogit.png "0405-58_MonacoGit")<br />Git|![“Monaco 搜索”图标](../../extensibility/ux-guidelines/media/0405-59_monacosearch.png "0405-59_MonacoSearch")<br />搜索|![“Monaco 文本”图标](../../extensibility/ux-guidelines/media/0405-60_monacotext.png "0405-60_MonacoText")<br />文本|

|F12|||
|---------|-|-|
|![“F12 整齐代码”图标](../../extensibility/ux-guidelines/media/0405-61_f12prettycode.png "0405-61_F12PrettyCode")<br />漂亮的代码|![“F12 警告”图标](../../extensibility/ux-guidelines/media/0405-62_f12warning.png "0405-62_F12Warning")<br />警告|![“F12 模拟”图标](../../extensibility/ux-guidelines/media/0405-63_f12emulate.png "0405-63_F12Emulate")<br />模仿|