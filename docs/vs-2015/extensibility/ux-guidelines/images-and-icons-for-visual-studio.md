---
title: 图像和图标
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 933726f1b1b67e1e919e3bc96f166ea516764557
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "58930627"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio 的图像和图标
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

##  <a name="BKMK_ImageUseInVisualStudio"></a> 在 Visual Studio 中的映像使用
 在之前创建图片，请考虑进行中的 1,000 多个映像的用法[Visual Studio 图像库](http://www.microsoft.com/en-my/download/details.aspx?id=35825)。

### <a name="types-of-images"></a>类型的映像

-   **图标**。 显示在命令、 层次结构、 模板和等等的小图像。 在 Visual Studio 中使用的默认图标大小为 16 x 16 PNG。 图标会自动生成的映像服务生成的 XAML 格式的 HDPI 支持。

     **注意：** 菜单系统中都使用映像，而不应创建的每个命令的图标。 请查阅[Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)若要查看您的命令是否应获得一个图标。

-   **缩略图。** 在对话框中，例如新项目对话框的预览区域中使用的图像。

-   **对话框的图像。** 在对话框或向导，作为描述性图形或消息指示器中显示的图像。 使用不常且仅在需要说明一个困难或获得用户的注意力 （警报，警告） 时。

-   **带动画的图像。** 在进度指示器、 状态栏和操作的对话框中使用。

-   **游标。** 用于指示是否在允许操作，使用的鼠标，其中对象可能会断开，依次类推。

##  <a name="BKMK_IconDesign"></a> 图标设计

### <a name="overview"></a>概述
 Visual Studio 使用现代样式图标，具有全新的 geometry 和对半余额为正/负 （浅/深），并使用直接且易于理解的隐喻。 重要图标设计点中心的清晰度、 简化和上下文。

- **清晰性：** 专注于提供一个图标，其含义和个性自我了核心工具。

- **简化：** 图标来缩短其核心意义 – 可以主题通过只是必需的元素和无修饰。

- **上下文：** 概念在开发期间，这至关重要，确定哪些元素构成的图标的核心比喻时，请考虑一个图标的角色的所有方面。

  使用图标，有大量设计点，以避免：

- 不要使用图标表示除 UI 元素，在适当的时候。 UI 元素是既不常见，很明显，也不唯一时，请选择更抽象的或符号的方法。

- 过度使用常见的元素不喜欢的文档、 文件夹、 箭头和放大镜。 使用此类元素，仅当至关重要的图标的含义。 例如，面向右侧的放大镜应指示仅搜索中，浏览和查找。

- 尽管某些旧图标元素维护的角度来看使用，但不创建新图标的角度来看除非元素缺少清楚起见，没有它。

- 不要将过多信息到一个图标。 了更多有用的过于复杂的映像相比，简单的映像，可以轻松地识别或被视为一个可识别的符号。 图标无法判断整篇文章。

### <a name="icon-creation"></a>图标创建

#### <a name="concept-development"></a>概念开发
 Visual Studio 在其用户界面内有各种图标类型。 在开发过程，请仔细考虑的图标类型。 不要将用于所选图标的元素不明白或不常见 UI 对象。 选择符号在这些情况下，例如使用智能标记图标。 请注意，在左侧的抽象标记的含义是较为明显比右侧的含糊不清的、 基于 UI 的版本：

|||
|-|-|
|**符号图像的正确使用**|**符号图像的不正确使用**|
|![正确的智能标记图标](../../extensibility/ux-guidelines/media/0404-01-smarttagcorrect.png "0404年 01_SmartTagCorrect")|![Incorrect Smart Tag icon](../../extensibility/ux-guidelines/media/0404-02-smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 有在其中标准的、 易于识别 UI 元素适用于图标的实例。 添加窗口是这样一个示例：

|||
|-|-|
|**在图标中正确的 UI 元素**|**错误图标中的 UI 元素**|
|![正确添加窗口图标](../../extensibility/ux-guidelines/media/0404-03-addwindowcorrect.png "0404年 03_AddWindowCorrect")|![不正确的添加窗口图标](../../extensibility/ux-guidelines/media/0404-04-addwindowincorrect.png "0404年 04_AddWindowIncorrect")|

 不使用文档作为基元素，除非它是至关重要的图标的含义。 不使用文档上添加文档元素 （见下文） 含义是丢失，而使用刷新文档元素为不必要通信含义。

|||
|-|-|
|**正确使用方法的文档图标**|**使用不正确的文档图标**|
|![正确的文档图标](../../extensibility/ux-guidelines/media/0404-05-documenticoncorrect.png "0404年 05_DocumentIconCorrect")|![不正确的文档图标](../../extensibility/ux-guidelines/media/0404-06-documenticonincorrect.png "0404年 06_DocumentIconIncorrect")|

 应由所显示的内容，例如与显示所有文件的示例一样可最好地阐释的图标表示"显示"的概念。 一种工具以可重用功能区可能用于指示如有必要，例如资源视图示例中的"视图"的概念。

|||
|-|-|
|**"显示"**|**"视图"**|
|![显示图标](../../extensibility/ux-guidelines/media/0404-07-show.png "0404年 07_Show")|![视图图标](../../extensibility/ux-guidelines/media/0404-08-view.png "0404年 08_View")|

 朝右放大玻璃图标应表示仅搜索、 查找和浏览。 朝左变体的加号或减号应表示唯一放大/缩小。

|||
|-|-|
|**"搜索"**|**"缩放"**|
|![搜索图标](../../extensibility/ux-guidelines/media/0404-09-search.png "0404年 09_Search")|![缩放图标](../../extensibility/ux-guidelines/media/0404-10-zoom.png "0404年 10_Zoom")|

 在树视图中，不要使用的文件夹图标和修饰符。 如果可用，请使用仅修饰符。

|||
|-|-|
|**正确的树视图图标**|**不正确的树视图图标**|
|![正确的树视图图标&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11-treeviewcorrect1.png "0404年 11_TreeViewCorrect1") ![正确的树视图图标&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12-treeviewcorrect2.png "0404年 12_TreeViewCorrect2")|![不正确的树视图图标&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13-treeviewincorrect1.png "0404年 13_TreeViewIncorrect1") ![不正确的树视图图标&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14-treeviewincorrect2.png "0404年 14_TreeViewIncorrect2")|

### <a name="style-details"></a>样式的详细信息

#### <a name="layout"></a>布局
 堆栈元素的标准 16x16 图标所示：

 ![16x16 图标的布局堆栈](../../extensibility/ux-guidelines/media/0404-15-layoutstack.png "0404年 15_LayoutStack")

 **16x16 图标的布局堆栈**

 状态通知元素是更好地用作独立的图标。 有的上下文，但是，在其中通知应堆叠在基元素，如使用任务完成图标：

 ![在 Visual Studio 中的独立通知](../../extensibility/ux-guidelines/media/0404-16-standalonenotificationicons.png "0404年 16_StandaloneNotificationIcons")

 **独立通知图标**

 ![任务完成图标](../../extensibility/ux-guidelines/media/0404-17-taskcomplete.png "0404年 17_TaskComplete")

 **任务完成图标**

 项目图标通常是包含多个大小的.ico 文件。 大多数 16x16 图标包含相同的元素。 32 x 32 版本具有更多详细信息，包括时适用的项目类型。

 ![项目在 Visual Studio 中的图标](../../extensibility/ux-guidelines/media/0404-18-iconprojectthreesizes.png "0404年 18_IconProjectThreeSizes")

 **VB Windows 控件库项目图标，16 x 16 和 32 x 32**

 中心在其像素框架中的图标。 如果这不可能，将调整到顶部和/或右侧的帧的图标。

 ![图标在像素框架内居中](../../extensibility/ux-guidelines/media/0404-19-iconcentered.png "0404年 19_IconCentered")

 **图标在像素框架内居中**

 ![图标对齐到像素框架的右上方](../../extensibility/ux-guidelines/media/0404-20-icontopright.png "0404年 20_IconTopRight")

 **图标与顶端对齐的帧**

 ![图标居中并与像素框架的顶部对齐](../../extensibility/ux-guidelines/media/0404-21-icontopalign.png "0404年 21_IconTopAlign")

 **图标居中并与框架的顶部对齐**

 若要实现理想的对齐方式和平衡，避免不阻止操作的标志符号的图标的基本元素。 角的基元素的顶部附近的标志符号的位置。 添加了另一个元素时, 请考虑的对齐方式和图标的平衡。

|||
|-|-|
|**正确对齐和平衡**|**未正确对齐和余额**|
|![更正的图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-22-alignbalancecorrect.png "0404年 22_AlignBalanceCorrect")|![不正确的图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-23-alignbalanceincorrect.png "0404年 23_AlignBalanceIncorrect")|

 请确保共享元素，集中使用的图标大小奇偶校验。 请注意，在不正确配对的圆形和箭头过和不匹配。

|||
|-|-|
|**正确的大小奇偶校验**|**大小不正确的奇偶校验**|
|![更正图标的大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-24-sizeparitycorrect.png "0404年 24_SizeParityCorrect")|![不正确的图标大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-25-sizeparityincorrect.png "0404年 25_SizeParityIncorrect")|

 使用一致的行和 visual 权重。 要生成的图标如何与通过使用-并排比较的其他图标的计算结果。 永远不会使用整个 16 x 16 帧，使用 15 x 15 或更小。 负正 （深浅） 比率应为 50/50。

|||
|-|-|
|**正确的负正比**|**不正确的负正率**|
|![更正的图标视觉重量&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-26-visualweightcorrect1.png "0404年 26_VisualWeightCorrect1")<br /><br /> ![更正的图标视觉重量&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27-visualweightcorrect2.png "0404年 27_VisualWeightCorrect2")<br /><br /> ![更正的图标视觉重量&#40;3&#41;](../../extensibility/ux-guidelines/media/0404-28-visualweightcorrect3.png "0404年 28_VisualWeightCorrect3")|![不正确的图标视觉重量](../../extensibility/ux-guidelines/media/0404-29-visualweightincorrect.png "0404年 29_VisualWeightIncorrect")|

 使用简单、 可比较形状和相互补充的角度来生成所选的元素，而无需牺牲元素完整性。 在可能的情况，请使用 45 度或 90 度角。

 ![更正的图标角度](../../extensibility/ux-guidelines/media/0404-30-iconanglescorrect.png "0404年 30_IconAnglesCorrect")

#### <a name="perspective"></a>透视
 保持清晰易懂的图标。 使用透视和光源仅在必要时。 虽然应避免使用图标元素上的角度来看，但某些元素是没有它无法识别。 在这种情况下，风格的角度来看通信，该元素的清楚起见。

 ![3&#45;点透视](../../extensibility/ux-guidelines/media/0404-31-3pointperspective.png "0404年 31_3PointPerspective")

 **3 点透视图**

 ![1&#45;点透视](../../extensibility/ux-guidelines/media/0404-32-1pointperspective.png "0404年 32_1PointPerspective")

 **1 点透视图**

 大多数元素应面向或向右倾斜。

 ![图标向右倾斜](../../extensibility/ux-guidelines/media/0404-33-angledright.png "0404年 33_AngledRight")

 仅将必要的清楚起见添加到对象时，请使用光源。

|||
|-|-|
|**正确光源**|**不正确的光源**|
|![更正的图标光源](../../extensibility/ux-guidelines/media/0404-34-lightsourcescorrect.png "0404年 34_LightSourcesCorrect")|![不正确的图标光源](../../extensibility/ux-guidelines/media/0404-35-lightsourcesincorrect.png "0404年 35_LightSourcesIncorrect")|

 使用概述了只是为了增强可读性，或若要更好地传达了工具。 负正 （深浅） 平衡应为 50/50。

|||
|-|-|
|**轮廓的正确使用**|**概述了的不正确使用**|
|![更正轮廓](../../extensibility/ux-guidelines/media/0404-36-outlinescorrect.png "0404年 36_OutlinesCorrect")|![不正确的轮廓](../../extensibility/ux-guidelines/media/0404-37-outlinesincorrect.png "0404年 37_OutlinesIncorrect")|

#### <a name="icon-types"></a>图标类型
 **外壳和命令栏**图标不超过三个以下元素组成： 一个基准、 修饰符、 一个操作或一个状态。

 ![外壳和命令栏图标](../../extensibility/ux-guidelines/media/0404-38-shellicons.png "0404年 38_ShellIcons")

 **外壳和命令栏图标的示例**

 **工具窗口命令栏**图标不超过三个以下元素组成： 一个基准、 修饰符、 一个操作或一个状态。

 ![工具窗口命令栏图标](../../extensibility/ux-guidelines/media/0404-39-toolwindowcommandbaricons.png "0404年 39_ToolWindowCommandBarIcons")

 **工具窗口命令栏图标的示例**

 **树视图消除歧义工具**图标不超过三个以下元素组成： 一个基准、 修饰符、 一个操作或一个状态。

 ![树视图消歧器图标](../../extensibility/ux-guidelines/media/0404-40-treeviewicons.png "0404年 40_TreeViewIcons")

 **视图消歧器图标树的示例**

 **基于状态的值的分类**图标存在处于以下状态： 活动、 禁用，活动和非活动状态已禁用。

 ![状态&#45;基于分类值图标](../../extensibility/ux-guidelines/media/0404-41-statebasedtaxonomy.png "0404年 41_StateBasedTaxonomy")

 **基于状态的值的分类图标的示例**

 **IntelliSense**图标不超过三个以下元素组成： 一个基准、 一个修饰符和一个状态。

 ![IntelliSense 图标](../../extensibility/ux-guidelines/media/0404-42-intellisenseicons.png "0404年 42_IntelliSenseIcons")

 **IntelliSense 图标的示例**

 **小型 (16 x 16) 项目**图标应具有不超过两个元素： 一个基类和一个修饰符。

 ![16x16 项目图标&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-43-16x16project1.png "0404年 43_16x16Project1") ![16x16 项目图标&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44-16x16project2.png "0404年 44_16x16Project2")![16x16 项目图标&#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45-16x16project3.png "0404年 45_16x16Project3")

 **小型 (16 x 16) 项目图标的示例**

 **大 (32 x 32) 项目**图标不超过四个以下元素组成： 一个基准、 一到两个修饰符和覆盖层的一种语言。

 ![32 x 32 项目图标](../../extensibility/ux-guidelines/media/0404-46-32x32project.png "0404年 46_32x32Project")

 **大 (32 x 32) 项目图标的示例**

### <a name="production-details"></a>生产环境的详细信息
 应使用 Windows Presentation Foundation (WPF) 创建所有新的 UI 元素和 wpf 的所有新图标应为 32 位 PNG 格式。 24 位 PNG 是旧格式，不支持透明度，因此不建议用于图标。

 保存 96 dpi 分辨率。

#### <a name="file-types"></a>文件类型

-   **32 位 PNG:** 图标的首选的格式。 可以将单个光栅 （像素） 图像存储无损数据压缩文件格式。 32 位 PNG 文件支持 alpha 通道透明度、 灰度校正和隔行扫描。

-   **32 位 BMP:** 非 WPF 控件。 也称为 XP 或增强色，32 位 BMP 是一种 RGB/A 图像格式，具有 alpha 通道透明度的真彩色图像。 Alpha 通道是一层的透明度，然后保存该位图作为其他 （第四个） 中的 Adobe Photoshop 中指定颜色通道。 提供一个快速的视觉提示有关颜色深度的所有 32 位 BMP 文件图稿生产期间添加黑色背景。 此黑色背景表示查看在 UI 中将要屏蔽的区域。

-   **32 位 ICO:** 项目图标和添加项。 ICO 的所有文件都都具有透明度 alpha 通道的 32 位真彩色 (RGB/A)。 因为 ICO 文件可以存储多个大小和颜色深度，Vista 图标是通常包含 16 x 16、 32 x 32、 48 x 48 和 256x256 图像大小以 ICO 格式。 为了在 Windows 资源管理器中正确显示，ICO 文件必须是保存列表进行每个图像大小为 24 位和 8 位颜色深度。

-   **XAML:** 设计图面和 Windows 装饰器。 XAML 图标是支持缩放、 旋转、 归档和透明度的基于矢量的图像文件。 它们现在不是在 Visual Studio 中常见，但由于其灵活性而变得更受欢迎。

-   **SVG**

-   **24 位 BMP:** Visual Studio 命令栏。 为 true 颜色 RGB 图像格式，24 位 BMP 是透明度的图标约定使用洋红色 （R = 255，G = 0，B = 255） 创建一层，为 knock 扩展透明层的颜色键。 在 24 位 bmp 格式，使用的背景色显示所有洋红色图面。

-   **24 位 GIF:** Visual Studio 命令栏。 支持透明度的 true 颜色 RGB 图像格式。 GIF 文件常用于向导图稿和 GIF 动画。

### <a name="icon-construction"></a>图标构造
 在 Visual Studio 中的最小图标大小为 16 x 16。 最大共同使用为 32 × 32。 请记住不以填满整个 16 x 16、 24 x 24 或 32 x 32 帧时设计一个图标。 清晰、 统一图标构造是必要的用户识别。 生成的图标时遵循以下几点。

- 图标应为清除、 易于理解，且一致。

- 最好使用状态通知元素作为单个图标而不层叠在图标基元素。 在某些上下文中，UI 可能需要的状态元素成对使用的基本元素。

- 项目图标通常是包含多个大小的.ico 文件。 正在更新仅 16 x 16、 24 x 24 和 32x32 图标。 大多数 16 x 16 和 24x24 图标将包含相同的元素。 32x32 图标包含更多详细信息，包括项目语言类型时适用。

- 32x32 图标，基元素通常具有 2 个像素线条粗细。 1 或 2 像素线条粗细可用的详细信息元素中。 使用您的最佳判断力来确定这是更适合。

- 其元素为 16 x 16 和 24x24 图标之间至少有 1 个像素宽间距。 对于 32 × 32 图标，使用 2 像素之间的修饰符和基元素以及元素之间的间距。

  ![元素间距 16 x 16、 24 x 24 和 32 x 32 图标](../../extensibility/ux-guidelines/media/0404-47-elementspacing.png "0404年 47_ElementSpacing")

  **元素间距图标大小的 16 x 16、 24 x 24 和 32 x 32**

#### <a name="color-and-accessibility"></a>颜色和辅助功能
 Visual Studio 的符合性指南要求产品中的所有图标都传递颜色和对比度的可访问性要求。 这通过图标反转的方法，并在设计时，您应注意到它们以编程方式将反转产品中。

 在 Visual Studio 图标中使用颜色的详细信息，请参阅[图像中使用颜色](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)。

##  <a name="BKMK_UsingColorInImages"></a> 在映像中使用颜色

### <a name="overview"></a>概述
 在 Visual Studio 中的图标是主要单色。 保留颜色来传达特定信息并永远不会用于修饰。 使用颜色：

-   若要指示某个操作

-   状态通知向用户发出警报

-   若要指定语言隶属关系

-   若要区分 IntelliSense 中的项

### <a name="accessibility"></a>可访问性
 Visual Studio 的符合性指南要求，所有图标签都入到的产品传递颜色和对比度的可访问性要求。 中的 visual 语言调色板的颜色已经过测试并满足这些要求。

#### <a name="color-inversion-for-dark-themes"></a>深色主题的颜色反转
 为了使 Visual Studio 深色主题中的正确对比度比所显示的图标，以编程方式应用反转。 本指南中的颜色选择部分，以便他们正确地反转。 限制对此调色板的颜色的使用或反转应用时，您将看到不可预知的结果。

 ![其颜色颠倒的图标的示例](../../extensibility/ux-guidelines/media/0405-01-darkthemeinversion.png "0405年 01_DarkThemeInversion")

 **必须反转其颜色的图标的示例**

### <a name="base-palette"></a>基调色板
 所有标准图标包含三种基本颜色。 图标包含没有渐变或投影 3D 工具图标的一个或两个例外情况。

|用法|名称|值 （浅色主题）|样本|示例|
|-----------|----------|---------------------------|------------|-------------|
|深色背景 /|VS BG|424242 / 66,66,66|![样本 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|![基调色板示例](../../extensibility/ux-guidelines/media/0405-02-basepaletteexample.png "0405年 02_BasePaletteExample")|
|前景/轻型|VS FG|F0EFF1 / 240,239,241|![样本 F0EFF1](../../extensibility/ux-guidelines/media/0405-f0eff1.png "0405_F0EFF1")||
|轮廓|VS 扩展|F6F6F6 / 246,246,246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")||

 除了基本的颜色，每个图标可能包含其他颜色从扩展的调色板。

### <a name="extended-palette"></a>扩展的调色板

#### <a name="action-modifiers"></a>操作修改程序
 以下四种颜色指示操作修改程序所需的操作类型：

|用法|名称|值 （所有主题）|样本|
|-----------|----------|--------------------------|------------|
|正|VS 操作绿色|388A34 / 56,138,52|![样本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|负数|VS 操作红色|A1260D / 161,38,13|![样本 A1260D](../../extensibility/ux-guidelines/media/0405-a1260d.png "0405_A1260D")|
|非特定语言|VS 操作蓝色|00539C / 0,83,156|![样本 00539c](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|创建/新|VS 操作橙色|C27D1A / 194,156,26|![Swatch C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>示例
 绿色用于"添加"，如正操作修改程序"运行，""Play"和"验证"。

|||||
|-|-|-|-|
|![运行图标](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405年 03_ActionModifierRun") **运行**|![执行查询图标](../../extensibility/ux-guidelines/media/0405-04-executequery.png "0405年 04_ExecuteQuery") **执行查询**|![播放所有步骤图标](../../extensibility/ux-guidelines/media/0405-05-playallsteps.png "0405年 05_PlayAllSteps") **都播放所有步骤**|![添加控件图标](../../extensibility/ux-guidelines/media/0405-06-addcontrol.png "0405年 06_AddControl") **添加控件**|

 红色用于负操作修改程序如"删除，""停止，""取消，"和"关闭"。

|||||
|-|-|-|-|
|![删除关系图标](../../extensibility/ux-guidelines/media/0405-07-deleterelationship.png "0405年 07_DeleteRelationship") **删除关系**|![删除列图标](../../extensibility/ux-guidelines/media/0405-08-deletecolumn.png "0405年 08_DeleteColumn") **删除列**|![停止查询图标](../../extensibility/ux-guidelines/media/0405-09-stopquery.png "0405年 09_StopQuery") **停止查询**|![连接的脱机状态图标](../../extensibility/ux-guidelines/media/0405-10-connectionoffline.png "0405年 10_ConnectionOffline") **脱机连接**|

 蓝色应用于非特定操作修饰符通常表示为箭头，如"，打开"状态"下一步，""Previous，""导入"和"导出"。

|||||
|-|-|-|-|
|![转到字段图标](../../extensibility/ux-guidelines/media/0405-11-gotofield.png "0405年 11_GoToField") **转到字段**|![批处理检查&#45;中图标](../../extensibility/ux-guidelines/media/0405-12-batchedcheckin.png "0405年 12_BatchedCheckIn") **批处理签入**|![地址编辑器图标](../../extensibility/ux-guidelines/media/0405-13-addresseditor.png "0405年 13_AddressEditor") **地址编辑器**|![关联编辑器图标](../../extensibility/ux-guidelines/media/0405-14-associationeditor.png "0405年 14_AssociationEditor") **关联编辑器**|

 深金级主要用于"New"修饰符。

|||||
|-|-|-|-|
|![新项目图标](../../extensibility/ux-guidelines/media/0405-15-newproject.png "0405年 15_NewProject") **新项目**|![创建新关系图图标](../../extensibility/ux-guidelines/media/0405-16-createnewgraph.png "0405年 16_CreateNewGraph") **创建新的关系图**|![新建单元测试图标](../../extensibility/ux-guidelines/media/0405-17-newunittest.png "0405年 17_NewUnitTest") **新单元测试**|![新列表项图标](../../extensibility/ux-guidelines/media/0405-18-newlistitem.png "0405年 18_NewListItem") **新列表项**|

#### <a name="special-cases"></a>特殊情况
 在特殊情况下，可能会单独为一个图标，独立地使用彩色的操作修饰符。 所使用的图标颜色反映与关联的图标的操作。 这种用法仅限于一小部分的图标，包括：

||||||
|-|-|-|-|-|
|![运行图标](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405年 03_ActionModifierRun") **运行**|![停止图标](../../extensibility/ux-guidelines/media/0405-19-stop.png "0405年 19_Stop") **停止**|![删除图标](../../extensibility/ux-guidelines/media/0405-20-delete.png "0405年 20_Delete") **删除**|![保存图标](../../extensibility/ux-guidelines/media/0405-21-save.png "0405年 21_Save") **保存**|![导航后退图标](../../extensibility/ux-guidelines/media/0405-22-navigateback.png "0405年 22_NavigateBack") **回导航**|

### <a name="code-hierarchy-palette"></a>Code 层次结构面板

#### <a name="folder"></a>文件夹

|用法|名称|值 （所有主题）|样本|示例|
|-----------|----------|--------------------------|------------|-------------|
|文件夹|文件夹|DCB67A / 220,182,122|![Swatch DCB67A](../../extensibility/ux-guidelines/media/0405-dcb67a.png "0405_DCB67A")|![文件夹颜色图标](../../extensibility/ux-guidelines/media/0405-23-foldercolor.png "0405年 23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio 语言
 每个常见的语言或平台 Visual Studio 中提供有关联的颜色。 这些颜色的使用基本图标，或出现在复合图标的右上角的语言修饰符。

|用法|名称|值 （所有主题）|样本|
|-----------|----------|--------------------------|------------|
|ASP，HTML，WPF|ASP HTML WPF 蓝色|0095D7 / 0,149,215|![Swatch 0095D7](../../extensibility/ux-guidelines/media/0405-0096d7.png "0405_0096D7")|
|C++|CPP 紫色|9B4F96 / 155,79,150|![样本 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|C#|CS 绿色 （VS 操作绿色）|388A34 / 56,138,52|![样本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|CSS|CSS 红色|BD1E2D / 189,30,45|![样本 BD1E2D](../../extensibility/ux-guidelines/media/0405-bd1e2d.png "0405_BD1E2D")|
|F#|FS 紫色|672878 / 103,40,120|![样本 672878](../../extensibility/ux-guidelines/media/0405-672878.png "0405_672878")|
|JavaScript|JS 橙色|F16421 / 241,100,33|![样本 F16421](../../extensibility/ux-guidelines/media/0405-f16421.png "0405_F16421")|
|VB|VB 蓝色 （VS 操作蓝色表示）|00539C / 0,83,156|![样本 00539c](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|TypeScript|TS 橙色|E04C06 / 224,76,6|![样本 E04C06](../../extensibility/ux-guidelines/media/0405-e04c06.png "0405_E04C06")|
|Python|上一年度绿色|879636 / 135,150,54|![样本 879636](../../extensibility/ux-guidelines/media/0405-879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>图标与语言修饰符的示例

|||||||
|-|-|-|-|-|-|
|![Visual Basic 图标](../../extensibility/ux-guidelines/media/0405-25-vb.png "0405年 25_VB") **VB**|![C&#35;图标](../../extensibility/ux-guidelines/media/0405-26-csharp.png "0405年 26_CSharp")**C#**|![C&#43; &#43;图标](../../extensibility/ux-guidelines/media/0405-27-cplusplus.png "0405年 27_CPlusPlus") **c + +**|![F&#35; icon](../../extensibility/ux-guidelines/media/0405-28-fsharp.png "0405-28_FSharp") **F#**|![JavaScript 图标](../../extensibility/ux-guidelines/media/0405-29-javascript.png "0405年 29_JavaScript") **JavaScript**|![Python 图标](../../extensibility/ux-guidelines/media/0405-30-python.png "0405年 30_Python") **Python**|
|![HTML 图标](../../extensibility/ux-guidelines/media/0405-31-html.png "0405年 31_HTML") **HTML**|![WPF 图标](../../extensibility/ux-guidelines/media/0405-32-wpf.png "0405年 32_WPF") **WPF**|![ASP 图标](../../extensibility/ux-guidelines/media/0405-33-asp.png "0405年 33_ASP") **ASP**|![CSS 图标](../../extensibility/ux-guidelines/media/0405-34-css.png "0405年 34_CSS") **CSS**|![TypeScript icon](../../extensibility/ux-guidelines/media/0405-35-typescript.png "0405-35_TypeScript") **TypeScript**||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense 图标使用排他的调色板。 这些颜色用于帮助用户快速将 IntelliSense 弹出列表中的不同项之间区分开来。

|用法|名称|值 （所有主题）|样本|
|-----------|----------|--------------------------|------------|
|类事件|VS 操作橙色|C27D1A / 194,125,26|![Swatch C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|
|扩展方法，方法中，模块中委托|VS 操作紫色|652D90 / 101,45,144|![样本 652d90](../../extensibility/ux-guidelines/media/0405-652d90.png "0405_652D90")|
|字段中，枚举项、 宏、 结构、 联合值类型，运算符，接口|VS 操作蓝色|00539C / 0,83,156|![样本 00539c](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|对象|VS 操作绿色|388A34 / 56,138,52|![样本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|常量、 异常、 枚举项、 地图、 地图项、 Namespace，模板中，类型定义|背景 (VS BG)|424242 / 66,66,66|![样本 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense 图标的示例

||||||
|-|-|-|-|-|
|![IntelliSense 类图标](../../extensibility/ux-guidelines/media/0405-36-intellisenseclass.png "0405年 36_IntelliSenseClass") **类**|![IntelliSense 私有事件图标](../../extensibility/ux-guidelines/media/0405-37-intellisenseprivateevent.png "0405年 37_IntelliSensePrivateEvent") **私有事件**|![IntelliSense 委托图标](../../extensibility/ux-guidelines/media/0405-38-intellisensedelegate.png "0405年 38_IntelliSenseDelegate") **委托**|![IntelliSense 方法好友图标](../../extensibility/ux-guidelines/media/0405-39-intellisensemethodfriend.png "0405年 39_IntelliSenseMethodFriend") **方法友元**|![字段图标](../../extensibility/ux-guidelines/media/0405-40-field.png "0405年 40_Field") **字段**|
|![IntelliSense 受保护的枚举项图标](../../extensibility/ux-guidelines/media/0405-41-intellisenseprotectedenumitem.png "0405年 41_IntelliSenseProtectedEnumItem") **受保护的枚举项**|![IntelliSense 对象图标](../../extensibility/ux-guidelines/media/0405-42-intellisenseobject.png "0405年 42_IntelliSenseObject") **对象**|![IntelliSense 模板图标](../../extensibility/ux-guidelines/media/0405-43-intellisensetemplate.png "0405年 43_IntelliSenseTemplate") **模板**|![IntelliSense 异常快捷方式图标](../../extensibility/ux-guidelines/media/0405-44-intellisenseexceptionshortcut.png "0405年 44_IntelliSenseExceptionShortcut") **异常快捷方式**||

### <a name="notifications"></a>通知
 在 Visual Studio 中的通知用于指示状态。 通知调色板使用以下四种颜色，以及黑色或白色前台填充选项，来定义具有以下状态级别的通知。

|用法|名称|值 （所有主题）|样本|
|-----------|----------|--------------------------|------------|
|状态： 非特定语言|通知蓝色 （VS 蓝色表示）|1BA1E2 / 27,161,226|![样本 1BA1E2](../../extensibility/ux-guidelines/media/0405-1ba1e2.png "0405_1BA1E2")|
|状态： 正|通知绿色 （VS 绿色）|339933 / 51,153,51|![样本 339933](../../extensibility/ux-guidelines/media/0405-339933.png "0405_339933")|
|状态： 负|通知 Red （VS 红色）|E51400 / 229,20,0|![样本 E51400](../../extensibility/ux-guidelines/media/0405-e51400.png "0405_E51400")|
|状态： 警告|通知黄色 （VS 橙色）|FFCC00 / 255,204,0|![Swatch FFCC00](../../extensibility/ux-guidelines/media/0405-ffcc00.png "0405_FFCC00")|
|前景色填充|通知黑色 (Black)|000000 / 0,0,0|![样本&#35;000000](../../extensibility/ux-guidelines/media/0405-000000.png "0405_000000")|
|前景色填充|通知白色 (White)|FFFFFF / 255,255,255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知图标的示例

|||||
|-|-|-|-|
|![警报图标](../../extensibility/ux-guidelines/media/0405-45-alert.png "0405年 45_Alert") **警报**|![警告图标](../../extensibility/ux-guidelines/media/0405-48-warning.png "0405年 48_Warning") **警告**|![完成图标](../../extensibility/ux-guidelines/media/0405-46-complete.png "0405年 46_Complete") **完成**|![停止图标](../../extensibility/ux-guidelines/media/0405-47-stop.png "0405年 47_Stop") **停止**|

### <a name="visual-studio-online"></a>Visual Studio Online
 一般情况下，Visual Studio Online 包括功能的浏览器中托管。 在不同的环境颜色各不相同，但该样式将保持不变。

|Group|用法|名称|值 （所有主题）|样本|
|-----------|-----------|----------|--------------------------|------------|
|TFS|背景|TFSO BG|656565/ 101, 101, 101|![样本 656565](../../extensibility/ux-guidelines/media/0405-656565.png "0405_656565")|
|TFS|轮廓|OUT TFSO|FFFFFF / 255，255，255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|Napa|背景|白色|FFFFFF / 255，255，255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|摩纳哥|背景|白色|FFFFFF / 255，255，255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|背景|白色|FFFFFF / 255，255，255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|普通|F12 Grey_Primary|555555 / 85, 85, 85|![样本 555555](../../extensibility/ux-guidelines/media/0405-555555.png "0405_555555")|
|F12|悬停|F12 Blue_Hover|2279BF / 34,121,191|![样本 2279BF](../../extensibility/ux-guidelines/media/0405-2279bf.png "0405_2279BF")|
|F12|已禁用|F12 LtGrey_Disabled|ABABAC / 171,171,172|![Swatch ABABAC](../../extensibility/ux-guidelines/media/0405-ababac.png "0405_ABABAC")|
|F12|将鼠标悬停在背景|将鼠标悬停在 bg|D9EBF7 / 217,235,247|![Swatch D9EBF7](../../extensibility/ux-guidelines/media/0405-d9ebf7.png "0405_D9EBF7")|
|F12|按下的背景|按下的 bg|B2D7F0 / 178,215,240|![Swatch B2D7F0](../../extensibility/ux-guidelines/media/0405-b2d7f0.png "0405_B2D7F0")|
|F12|轮廓|VS 扩展|F6F6F6 / 246,246,246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")|
|F12|信息|信息|00BCF2 / 0,188,242|![样本 00BCF2](../../extensibility/ux-guidelines/media/0405-00bcf2.png "0405_00BCF2")|
|F12|警告|警告|F28300 / 242,131,0|![样本 F28300](../../extensibility/ux-guidelines/media/0405-f28300.png "0405_F28300")|
|F12|错误 / 负|Error_Negative|E81123 / 232,17,35|![样本 E81123](../../extensibility/ux-guidelines/media/0405-e81123.png "0405_E81123")|
|F12|启动 / 正|Start_Positive|009E49 / 0,158,73|![样本 009E49](../../extensibility/ux-guidelines/media/0405-009e49.png "0405_009E49")|
|F12|中断类型|中断类型|9B4F96 / 155,79,150|![样本 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|F12|事件标记|事件标记|A51F00 / 165,31,0|![Swatch A51F00](../../extensibility/ux-guidelines/media/0405-a51f00.png "0405_A51F00")|
|F12|用户标记|用户标记|F16220 / 241,98,32|![样本 F16220](../../extensibility/ux-guidelines/media/0405-f16220.png "0405_F16220")|

#### <a name="examples-of-visual-studio-online-icons"></a>Visual Studio Online 的图标的示例

|TFS Online||||
|----------------|-|-|-|
|![TFS Online 团队图标](../../extensibility/ux-guidelines/media/0405-49-tfsonlineteam.png "0405年 49_TFSOnlineTeam") **Online 团队**|![TFS 信息图标](../../extensibility/ux-guidelines/media/0405-50-tfsinformation.png "0405年 50_TFSInformation") **信息**|![TFS 历史记录图标](../../extensibility/ux-guidelines/media/0405-51-tfshistory.png "0405年 51_TFSHistory") **历史记录**|![TFS 分支图标](../../extensibility/ux-guidelines/media/0405-52-tfsbranch.png "0405年 52_TFSBranch") **分支**|

|Napa||||
|----------|-|-|-|
|![Napa 内容图标](../../extensibility/ux-guidelines/media/0405-53-napacontent.png "0405年 53_NapaContent") **内容**|![Napa 办公邮件图标](../../extensibility/ux-guidelines/media/0405-54-napaofficemail.png "0405年 54_NapaOfficeMail") **Office 邮件**|![Napa SharePoint 图标](../../extensibility/ux-guidelines/media/0405-55-napasharepoint.png "0405年 55_NapaSharePoint") **SharePoint**|![Napa 任务窗格图标](../../extensibility/ux-guidelines/media/0405-56-napataskpane.png "0405年 56_NapaTaskPane") **任务窗格**|

|摩纳哥||||
|------------|-|-|-|
|![Monaco 文件图标](../../extensibility/ux-guidelines/media/0405-57-monacofiles.png "0405年 57_MonacoFiles") **文件**|![Monaco Git 图标](../../extensibility/ux-guidelines/media/0405-58-monacogit.png "0405年 58_MonacoGit") **Git**|![Monaco 搜索图标](../../extensibility/ux-guidelines/media/0405-59-monacosearch.png "0405年 59_MonacoSearch") **搜索**|![Monaco 文本图标](../../extensibility/ux-guidelines/media/0405-60-monacotext.png "0405年 60_MonacoText") **文本**|

|F12||||
|---------|-|-|-|
|![F12 整齐代码图标](../../extensibility/ux-guidelines/media/0405-61-f12prettycode.png "0405年 61_F12PrettyCode") **相当代码**|![F12 警告图标](../../extensibility/ux-guidelines/media/0405-62-f12warning.png "0405年 62_F12Warning") **警告**|![F12 模拟图标](../../extensibility/ux-guidelines/media/0405-63-f12emulate.png "0405年 63_F12Emulate") **Emulate**|
