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
ms.openlocfilehash: 843829c56fcbd2f5c558d7c4a8b14a660a431eac
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558219"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio 的图像和图标
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="BKMK_ImageUseInVisualStudio"></a>Visual Studio 中的图像使用
 创建图稿之前，请考虑在[Visual Studio 图像库](https://www.microsoft.com/download/details.aspx?id=35825)中使用1000多个图像。

### <a name="types-of-images"></a>映像类型

- **图标**。 出现在命令、层次结构、模板等中的小图像。 在 Visual Studio 中使用的默认图标大小为 16x16 PNG。 映像服务生成的图标会自动生成 HDPI 支持的 XAML 格式。

     **注意：** 如果在菜单系统中使用图像，则不应为每个命令创建一个图标。 请参阅[Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)，查看命令是否应该获得图标。

- **缩览.** 在对话框的预览区域中使用的图像，如 "新建项目" 对话框。

- **对话框图像。** 对话框或向导中显示的图像，可以作为描述性图形或消息指示器。 仅在必要时使用，以便阐释难以理解的概念或引起用户注意（警报、警告）。

- **动画图像。** 在进度指示器、状态栏和操作对话框中使用。

- **指针.** 用于指示是允许使用鼠标还是允许在其中放置对象等操作。

## <a name="BKMK_IconDesign"></a>图标设计

### <a name="overview"></a>概述
 Visual Studio 使用新式的图标，其中包含干净的几何和正/负（浅/暗）的50/50 平衡，并使用直接、可理解的形式。 关键图标设计要点围绕清晰、简化和上下文。

- **清晰度：** 专注于核心比喻，提供图标的含义和 individuality。

- **简化：** 将图标缩减为其核心含义–只需元素，即可获取主题，无需基本。

- **上下文：** 在概念开发期间考虑图标角色的所有方面，这在确定哪些元素构成图标的核心比喻时至关重要。

  使用图标时，有许多设计点需要避免：

- 不要使用表示 UI 元素的图标（如果适用）。 如果 UI 元素既不常见、明显又不唯一，请选择更抽象或更具符号的方法。

- 不要滥用常见元素，例如文档、文件夹、箭头和放大镜。 仅当对图标的含义至关重要时才使用此类元素。 例如，右侧的放大镜应仅指示 "搜索"、"浏览" 和 "查找"。

- 尽管某些旧图标元素保留了透视的使用，但不要使用透视创建新图标，除非该元素缺少清晰的元素。

- 不要将过多的信息 cram 图标。 可以轻松识别或了解为可识别符号的简单映像比过于复杂的映像更有用。 图标无法讲述全部内容。

### <a name="icon-creation"></a>图标创建

#### <a name="concept-development"></a>概念开发
 Visual Studio 在其用户界面中提供各种图标类型。 在开发过程中仔细考虑图标类型。 不要对图标元素使用不清楚或不常见的 UI 对象。 在这些情况下选择符号，例如，通过智能标记图标。 请注意，左侧抽象标记的含义比右侧基于 UI 的模糊版本更为明显：

|||
|-|-|
|**正确使用符号图像**|**不正确使用符号图像**|
|![更正智能标记图标](../../extensibility/ux-guidelines/media/0404-01-smarttagcorrect.png "0404-01_SmartTagCorrect")|![智能标记图标不正确](../../extensibility/ux-guidelines/media/0404-02-smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 在某些情况下，标准的、易于识别的 UI 元素可以很好地用于图标。 添加窗口是一个示例：

|||
|-|-|
|**更正图标中的 UI 元素**|**图标中的 UI 元素不正确**|
|![正确的 "添加窗口" 图标](../../extensibility/ux-guidelines/media/0404-03-addwindowcorrect.png "0404-03_AddWindowCorrect")|![不正确的 "添加窗口" 图标](../../extensibility/ux-guidelines/media/0404-04-addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 不要将文档用作基元素，除非该元素对图标的含义是必需的。 如果 "添加文档" （以下）上没有 "文档元素"，则表示含义会丢失，而 "刷新文档" 元素不必传达含义。

|||
|-|-|
|**正确使用文档图标**|**不正确使用文档图标**|
|![更正文档图标](../../extensibility/ux-guidelines/media/0404-05-documenticoncorrect.png "0404-05_DocumentIconCorrect")|![错误的文档图标](../../extensibility/ux-guidelines/media/0404-06-documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 "Show" 的概念应该用图标表示，该图标最能说明要显示的内容，如 "显示所有文件" 示例。 如果需要，可以使用镜头比喻来指示 "查看" 的概念，如使用资源视图示例。

|||
|-|-|
|**向**|**显示**|
|![显示图标](../../extensibility/ux-guidelines/media/0404-07-show.png "0404-07_Show")|![视图图标](../../extensibility/ux-guidelines/media/0404-08-view.png "0404-08_View")|

 面向右的放大镜图标只应表示 "搜索"、"查找" 和 "浏览"。 带有加号或减号的左变量只应表示放大/缩小。

|||
|-|-|
|**寻找**|**贴近**|
|![搜索图标](../../extensibility/ux-guidelines/media/0404-09-search.png "0404-09_Search")|![缩放图标](../../extensibility/ux-guidelines/media/0404-10-zoom.png "0404-10_Zoom")|

 在树视图中，不要同时使用文件夹图标和修饰符。 如果可用，请仅使用修饰符。

|||
|-|-|
|**正确的树视图图标**|**不正确的树视图图标**|
|![正确的树视图&#40;图标&#41; 1](../../extensibility/ux-guidelines/media/0404-11-treeviewcorrect1.png "0404-11_TreeViewCorrect1") ![正确的树&#40;视图&#41;图标 2](../../extensibility/ux-guidelines/media/0404-12-treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![不正确的树&#40;视图&#41;图标 1](../../extensibility/ux-guidelines/media/0404-13-treeviewincorrect1.png "0404-13_TreeViewIncorrect1") ![不正确&#40;的&#41;树视图图标 2](../../extensibility/ux-guidelines/media/0404-14-treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>样式详细信息

#### <a name="layout"></a>布局
 如标准16x16 图标所示的堆栈元素：

 ![16x16 图标的布局堆栈](../../extensibility/ux-guidelines/media/0404-15-layoutstack.png "0404-15_LayoutStack")

 **16x16 图标的布局堆栈**

 状态通知元素更好用作独立图标。 但存在上下文，其中通知应在基元素上堆积，如使用 "任务完成" 图标：

 ![Visual Studio 中的独立通知](../../extensibility/ux-guidelines/media/0404-16-standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")

 **独立通知图标**

 !["任务完成" 图标](../../extensibility/ux-guidelines/media/0404-17-taskcomplete.png "0404-17_TaskComplete")

 **"任务完成" 图标**

 项目图标通常是包含多个大小的 .ico 文件。 大多数16x16 图标包含相同的元素。 32x32 版本包含更多详细信息，包括项目类型（如果适用）。

 ![Visual Studio 中的项目图标](../../extensibility/ux-guidelines/media/0404-18-iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")

 **VB Windows 控件库项目图标、16x16 和32x32**

 使图标在其像素框架中居中。 如果无法做到这一点，请将图标与框架的顶部和/或右侧对齐。

 ![位于像素框架内的图标](../../extensibility/ux-guidelines/media/0404-19-iconcentered.png "0404-19_IconCentered")

 **位于像素框架内的图标**

 ![图标与像素框架的右上方对齐](../../extensibility/ux-guidelines/media/0404-20-icontopright.png "0404-20_IconTopRight")

 **图标与框架右上方对齐**

 ![图标居中并与像素框架的顶部对齐](../../extensibility/ux-guidelines/media/0404-21-icontopalign.png "0404-21_IconTopAlign")

 **图标居中并与框架的顶部对齐**

 若要实现理想的对齐和平衡，请避免用操作标志符号阻止该图标的基本元素。 将标志符号置于基元素左上角附近。 添加其他元素时，请考虑该图标的对齐方式和余额。

|||
|-|-|
|**正确对齐和平衡**|**对齐和余额错误**|
|![更正图标平衡和对齐方式](../../extensibility/ux-guidelines/media/0404-22-alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![图标平衡和对齐不正确](../../extensibility/ux-guidelines/media/0404-23-alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 确保用于共享元素并在集中使用的图标的大小奇偶校验。 请注意，在错误配对中，圆圈和箭头非常大，并且不匹配。

|||
|-|-|
|**正确的大小奇偶校验**|**大小不正确**|
|![更正图标大小和奇偶校验](../../extensibility/ux-guidelines/media/0404-24-sizeparitycorrect.png "0404-24_SizeParityCorrect")|![图标大小和奇偶校验不正确](../../extensibility/ux-guidelines/media/0404-25-sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 使用一致的线条和视觉权重。 使用并排比较来评估所生成图标与其他图标的比较方式。 切勿使用整个16x16 帧，请使用15x15 或更小的帧。 负数到正（从深色到浅）的比率应为50/50。

|||
|-|-|
|**更正负到正比率**|**负与正的比率不正确**|
|![图标&#40;1 的正确视觉权重&#41;](../../extensibility/ux-guidelines/media/0404-26-visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![图标&#40;2 的正确视觉权重&#41;](../../extensibility/ux-guidelines/media/0404-27-visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![图标&#40;3 的正确视觉权重&#41;](../../extensibility/ux-guidelines/media/0404-28-visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![图标的视觉权重不正确](../../extensibility/ux-guidelines/media/0404-29-visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 使用简单、可比较的形状和互补角度来构建元素，而不会牺牲元素完整性。 尽可能使用45°或90度角。

 ![更正图标角度](../../extensibility/ux-guidelines/media/0404-30-iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>透视
 使图标清晰明了。 仅在必要时才使用透视和光源。 虽然应避免使用 "透视" 图标元素，但没有该元素时，某些元素是无法识别的。 在这种情况下，风格化透视会传达元素的清晰度。

 ![3&#45;点透视](../../extensibility/ux-guidelines/media/0404-31-3pointperspective.png "0404-31_3PointPerspective")

 **3点透视**

 ![1&#45;点透视](../../extensibility/ux-guidelines/media/0404-32-1pointperspective.png "0404-32_1PointPerspective")

 **1点透视**

 大多数元素应该面向或向右倾斜。

 ![图标向右倾斜](../../extensibility/ux-guidelines/media/0404-33-angledright.png "0404-33_AngledRight")

 仅在将必要的清晰度添加到对象时使用光源。

|||
|-|-|
|**正确的光源**|**不正确的光源**|
|![正确的图标灯光源](../../extensibility/ux-guidelines/media/0404-34-lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![图标的灯光源不正确](../../extensibility/ux-guidelines/media/0404-35-lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 仅使用大纲提高清晰度，或更好地传达比喻。 负（深色）平衡应为50/50。

|||
|-|-|
|**正确使用轮廓**|**不正确地使用轮廓**|
|![正确的轮廓](../../extensibility/ux-guidelines/media/0404-36-outlinescorrect.png "0404-36_OutlinesCorrect")|![不正确的轮廓](../../extensibility/ux-guidelines/media/0404-37-outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>图标类型
 **Shell 和命令栏**图标包含的元素不超过三个：一个基元素、一个修饰符、一个操作或一个状态。

 ![Shell 和命令栏图标](../../extensibility/ux-guidelines/media/0404-38-shellicons.png "0404-38_ShellIcons")

 **Shell 和命令栏图标示例**

 **工具窗口命令栏**图标包含的元素不超过三个：一个基元素、一个修饰符、一个操作或一个状态。

 ![工具窗口命令栏图标](../../extensibility/ux-guidelines/media/0404-39-toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")

 **工具窗口命令栏图标示例**

 **树视图消除歧义**图标包含的以下元素不超过三个：一个基本元素、一个修饰符、一个操作或一个状态。

 ![树视图消除歧义图标](../../extensibility/ux-guidelines/media/0404-40-treeviewicons.png "0404-40_TreeViewIcons")

 **树视图消除歧义图标示例**

 **基于状态的值分类**图标处于以下状态：活动、已禁用和非活动已禁用。

 ![基于&#45;状态的分类值图标](../../extensibility/ux-guidelines/media/0404-41-statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")

 **基于状态的值分类图标示例**

 **IntelliSense**图标包含的元素不超过三个：一个基元素、一个修饰符和一个状态。

 ![IntelliSense 图标](../../extensibility/ux-guidelines/media/0404-42-intellisenseicons.png "0404-42_IntelliSenseIcons")

 **IntelliSense 图标示例**

 **小（16x16）项目**图标不应具有两个以上的元素：一个基元素和一个修饰符。

 ![16x16 项目图标&#40;1&#41; ](../../extensibility/ux-guidelines/media/0404-43-16x16project1.png "0404-43_16x16Project1") ![16x16 项目图标&#40;2&#41; ](../../extensibility/ux-guidelines/media/0404-44-16x16project2.png "0404-44_16x16Project2") ![16x16 项目图标&#40;3&#41; ](../../extensibility/ux-guidelines/media/0404-45-16x16project3.png "0404-45_16x16Project3")

 **小（16x16）项目图标示例**

 **大（32x32）项目**图标不包含以下四个元素中的四个：一个基本元素、两个修饰符和一个语言覆盖区。

 ![32x32 项目图标](../../extensibility/ux-guidelines/media/0404-46-32x32project.png "0404-46_32x32Project")

 **大（32x32）项目图标示例**

### <a name="production-details"></a>生产详细信息
 所有新的 UI 元素都应该使用 Windows Presentation Foundation （WPF）创建，WPF 的所有新图标应采用32位 PNG 格式。 24位 PNG 是一种不支持透明度的旧格式，因此不建议用于图标。

 将分辨率保存为 96 DPI。

#### <a name="file-types"></a>文件类型

- **32 位 PNG：** 图标的首选格式。 一种无损数据压缩文件格式，可存储单个光栅（像素）图像。 32位 PNG 文件支持 alpha 通道透明度、伽玛更正和隔行扫描。

- **32 位 BMP：** 对于非 WPF 控件。 也称为 XP 或高颜色，32位 BMP 是一种 RGB/image 格式，这是一个带有 alpha 通道透明度的真彩色图像。 Alpha 通道是在 Adobe Photoshop 中指定的一层透明度，然后将其作为附加（第四）颜色通道保存到位图中。 在图稿生产过程中，将在所有32位 BMP 文件中添加黑色背景，以提供有关颜色深度的快速可视提示。 此黑色背景表示要在 UI 中屏蔽的区域。

- **32 位 .ico：** 对于项目图标和添加项。 所有的 .ICO 文件都是32位真彩色，具有 alpha 通道透明度（RGB/A）。 因为 .ICO 文件可以存储多个大小和颜色深度，所以，Vista 图标通常采用包含16x16、32x32、48x48 和256x256 图像大小的 .ICO 格式。 若要在 Windows 资源管理器中正确显示，则必须将 .ICO 文件保存到每个图像大小的24位和8位颜色深度。

- **XAML：** 用于设计图面和 Windows 装饰器。 XAML 图标是基于矢量的图像文件，支持缩放、旋转、归档和透明度。 它们目前在 Visual Studio 中并不常见，但由于其灵活性，它们变得越来越流行。

- **SVG**

- 适用于 Visual Studio 命令栏的**24 位 BMP：** 。 "真彩色 RGB 图像格式"，24位 BMP 是一个图标约定，它通过使用品红（R = 255，G = 0，B = 255）作为 "挖空透明度" 层的颜色键来创建透明度层。 在24位 BMP 中，使用背景色显示所有洋红色图面。

- **24 位 GIF：** 适用于 Visual Studio 命令栏。 支持透明度的真彩色 RGB 图像格式。 GIF 文件通常用于向导插图和 GIF 动画。

### <a name="icon-construction"></a>图标构造
 Visual Studio 中的最小图标大小为16x16。 最常见的用法是32x32。 请注意，在设计图标时不会填充整个16x16、24x24 或32x32 帧。 清晰的图标构造对于用户识别至关重要。 在生成图标时遵循以下几点。

- 图标应清晰、可理解和一致。

- 最好使用状态通知元素作为单个图标，而不是将其堆栈到图标基元素之上。 在某些上下文中，UI 可能要求状态元素与基元素配对。

- 项目图标通常是包含若干大小的 .ico 文件。 仅更新16x16、24x24 和32x32 图标。 大多数16x16 和24x24 图标将包含相同的元素。 32x32 图标包含更多详细信息，包括项目语言类型（如果适用）。

- 对于32x32 图标，基本元素通常具有2像素的线条粗细。 可对详细信息元素使用1到2像素的线条宽度。 使用最佳判断来确定哪个更适合。

- 16x16 和24x24 图标的元素之间至少有1个像素的间距。 对于32x32 图标，请在元素之间以及修饰符和 base 元素之间使用2像素的间距。

  ![16x16、24x24 和32x32 图标的元素间距](../../extensibility/ux-guidelines/media/0404-47-elementspacing.png "0404-47_ElementSpacing")

  **大小为16x16、24x24 和32x32 的图标的元素间距**

#### <a name="color-and-accessibility"></a>颜色和辅助功能
 Visual Studio 符合性准则要求产品中的所有图标均满足颜色和对比度的辅助功能要求。 这是通过图标反转来实现的，在设计时，您应该注意到它们将以编程方式在产品中进行反转。

 有关在 Visual Studio 图标中使用颜色的详细信息，请参阅[使用图像中的颜色](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)。

## <a name="BKMK_UsingColorInImages"></a>使用图像中的颜色

### <a name="overview"></a>概述
 Visual Studio 中的图标主要单色。 颜色是为传达特定信息而不是装饰而保留的。 使用颜色：

- 指示操作

- 向用户发出警报状态通知

- 指定语言关联

- 区分 IntelliSense 内的项

### <a name="accessibility"></a>可访问性
 Visual Studio 符合性准则要求所有已签入产品的图标都通过颜色和对比度的辅助功能要求。 已对 visual language 调色板中的颜色进行了测试并满足这些要求。

#### <a name="color-inversion-for-dark-themes"></a>深色主题的颜色反转
 为了使图标在 Visual Studio 深色主题中显示为正确的对比度，将以编程方式应用反转。 本指南中的颜色已在部分中选择，以使它们正确地反转。 限制对此调色板使用颜色，或在应用反转后出现不可预知的结果。

 ![颜色已反转的图标示例](../../extensibility/ux-guidelines/media/0405-01-darkthemeinversion.png "0405-01_DarkThemeInversion")

 **颜色反转的图标示例**

### <a name="base-palette"></a>基本调色板
 所有标准图标都包含三种基本颜色。 图标不包含渐变或阴影，三维工具图标有一个或两个例外。

|使用情况|名称|值（浅色主题）|样板|示例|
|-----------|----------|---------------------------|------------|-------------|
|背景/深色|VS BG|424242 / 66,66,66|![样本424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|![基本调色板示例](../../extensibility/ux-guidelines/media/0405-02-basepaletteexample.png "0405-02_BasePaletteExample")|
|前景/浅色|VS FG|F0EFF1 / 240,239,241|![样本 F0EFF1](../../extensibility/ux-guidelines/media/0405-f0eff1.png "0405_F0EFF1")||
|轮廓|与外|F6F6F6 / 246,246,246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")||

 除了基本颜色之外，每个图标还可以包含扩展调色板中的一种附加颜色。

### <a name="extended-palette"></a>扩展调色板

#### <a name="action-modifiers"></a>操作修饰符
 以下四种颜色指示操作修饰符所需的操作类型：

|使用情况|名称|值（所有主题）|样板|
|-----------|----------|--------------------------|------------|
|正|VS 操作绿色|388A34/56138、52|![样本388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|负|VS 操作红色|A1260D/161，38，13|![样本 A1260D](../../extensibility/ux-guidelines/media/0405-a1260d.png "0405_A1260D")|
|中立|VS 操作蓝|00539C / 0,83,156|![样本00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|创建/新建|VS 操作橙色|C27D1A / 194,156,26|![样本 C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>示例
 绿色用于正操作修饰符，如 "添加"、"运行"、"播放" 和 "验证"。

|||||
|-|-|-|-|
|![运行图标](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405-03_ActionModifierRun")**运行**|![执行查询图标](../../extensibility/ux-guidelines/media/0405-04-executequery.png "0405-04_ExecuteQuery")**执行查询**|"![播放所有步骤" 图标](../../extensibility/ux-guidelines/media/0405-05-playallsteps.png "0405-05_PlayAllSteps")**播放所有步骤**|![添加控件图标](../../extensibility/ux-guidelines/media/0405-06-addcontrol.png "0405-06_AddControl")**添加控件**|

 Red 用于否定操作修饰符，如 "删除"、"停止"、"取消" 和 "关闭"。

|||||
|-|-|-|-|
|![删除关系图标](../../extensibility/ux-guidelines/media/0405-07-deleterelationship.png "0405-07_DeleteRelationship")**删除关系**|![删除列图标](../../extensibility/ux-guidelines/media/0405-08-deletecolumn.png "0405-08_DeleteColumn")**删除列**|![停止查询图标](../../extensibility/ux-guidelines/media/0405-09-stopquery.png "0405-09_StopQuery")**停止查询**|脱机![连接脱机图标](../../extensibility/ux-guidelines/media/0405-10-connectionoffline.png "0405-10_ConnectionOffline")**连接**|

 Blue 适用于最常表示为箭头的非特定操作修饰符，如 "打开"、"下一步"、"上一步"、"导入" 和 "导出"。

|||||
|-|-|-|-|
|"![中转到" 字段图标](../../extensibility/ux-guidelines/media/0405-11-gotofield.png "0405-11_GoToField")**中转到字段**|![批处理签&#45;入图标](../../extensibility/ux-guidelines/media/0405-12-batchedcheckin.png "0405-12_BatchedCheckIn")**批量签入**|![地址编辑器图标](../../extensibility/ux-guidelines/media/0405-13-addresseditor.png "0405-13_AddressEditor")**地址编辑器**|![关联编辑器图标](../../extensibility/ux-guidelines/media/0405-14-associationeditor.png "0405-14_AssociationEditor")**关联编辑器**|

 深金色主要用于 "New" 修饰符。

|||||
|-|-|-|-|
|![新建项目图标](../../extensibility/ux-guidelines/media/0405-15-newproject.png "0405-15_NewProject")**新建项目**|"![新建关系图" 图标](../../extensibility/ux-guidelines/media/0405-16-createnewgraph.png "0405-16_CreateNewGraph")**创建新关系图**|![新单元测试图标](../../extensibility/ux-guidelines/media/0405-17-newunittest.png "0405-17_NewUnitTest")**新建单元测试**|![新建列表项图标](../../extensibility/ux-guidelines/media/0405-18-newlistitem.png "0405-18_NewListItem")**新建列表项**|

#### <a name="special-cases"></a>特殊情况
 在特殊情况下，可以将彩色操作修饰符单独用作独立图标。 图标使用的颜色反映了图标所关联的操作。 此使用限制为一小部分图标，其中包括：

||||||
|-|-|-|-|-|
|![运行图标](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405-03_ActionModifierRun")**运行**|![停止图标](../../extensibility/ux-guidelines/media/0405-19-stop.png "0405-19_Stop")**停止**|![删除图标](../../extensibility/ux-guidelines/media/0405-20-delete.png "0405-20_Delete")**删除**|![保存图标](../../extensibility/ux-guidelines/media/0405-21-save.png "0405-21_Save")**保存**|![向后导航图标](../../extensibility/ux-guidelines/media/0405-22-navigateback.png "0405-22_NavigateBack")**向后导航**|

### <a name="code-hierarchy-palette"></a>代码层次结构调色板

#### <a name="folder"></a>Folder

|使用情况|名称|值（所有主题）|样板|示例|
|-----------|----------|--------------------------|------------|-------------|
|Folders|Folder|DCB67A / 220,182,122|![样本 DCB67A](../../extensibility/ux-guidelines/media/0405-dcb67a.png "0405_DCB67A")|![文件夹颜色图标](../../extensibility/ux-guidelines/media/0405-23-foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio 语言
 Visual Studio 中提供的每个常见语言或平台都有关联的颜色。 这些颜色用在基本图标上，或在复合图标右上角出现的语言修饰符上使用。

|使用情况|名称|值（所有主题）|样板|
|-----------|----------|--------------------------|------------|
|ASP、HTML、WPF|ASP HTML WPF 蓝色|0095D7 / 0,149,215|![样本0095D7](../../extensibility/ux-guidelines/media/0405-0096d7.png "0405_0096D7")|
|C++|CPP 紫色|9B4F96/155，79150|![样本9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|C#|CS 绿色（VS 操作绿色）|388A34/56138、52|![样本388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|CSS|CSS Red|BD1E2D/189，30，45|![样本 BD1E2D](../../extensibility/ux-guidelines/media/0405-bd1e2d.png "0405_BD1E2D")|
|F#|FS 紫色|672878 / 103,40,120|![样本672878](../../extensibility/ux-guidelines/media/0405-672878.png "0405_672878")|
|JavaScript|JS 橙色|F16421 / 241,100,33|![样本 F16421](../../extensibility/ux-guidelines/media/0405-f16421.png "0405_F16421")|
|VB|VB 蓝（VS 操作蓝色）|00539C / 0,83,156|![样本00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|TypeScript|TS 橙色|E04C06 / 224,76,6|![样本 E04C06](../../extensibility/ux-guidelines/media/0405-e04c06.png "0405_E04C06")|
|Python|PY 绿色|879636 / 135,150,54|![样本879636](../../extensibility/ux-guidelines/media/0405-879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>带有语言修饰符的图标的示例

|||||||
|-|-|-|-|-|-|
|![Visual Basic 图标](../../extensibility/ux-guidelines/media/0405-25-vb.png "0405-25_VB") **VB**|![C&#35;图标](../../extensibility/ux-guidelines/media/0405-26-csharp.png "0405-26_CSharp")**C#**|![C&#43;图标&#43; ](../../extensibility/ux-guidelines/media/0405-27-cplusplus.png "0405-27_CPlusPlus")**C++**|![F&#35;图标](../../extensibility/ux-guidelines/media/0405-28-fsharp.png "0405-28_FSharp")**F#**|![Javascript 图标](../../extensibility/ux-guidelines/media/0405-29-javascript.png "0405-29_JavaScript") **javascript**|![Python 图标](../../extensibility/ux-guidelines/media/0405-30-python.png "0405-30_Python") **python**|
|![Html 图标](../../extensibility/ux-guidelines/media/0405-31-html.png "0405-31_HTML") **html**|![Wpf 图标](../../extensibility/ux-guidelines/media/0405-32-wpf.png "0405-32_WPF") **wpf**|![Asp 图标](../../extensibility/ux-guidelines/media/0405-33-asp.png "0405-33_ASP") **asp**|![Css 图标](../../extensibility/ux-guidelines/media/0405-34-css.png "0405-34_CSS") **css**|![Typescript 图标](../../extensibility/ux-guidelines/media/0405-35-typescript.png "0405-35_TypeScript") **typescript**||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense 图标使用独有调色板。 这些颜色用于帮助用户在 IntelliSense 弹出列表中快速区分不同的项。

|使用情况|名称|值（所有主题）|样板|
|-----------|----------|--------------------------|------------|
|类，事件|VS 操作橙色|C27D1A / 194,125,26|![样本 C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|
|扩展方法、方法、模块、委托|VS 操作紫色|652D90/101、45144|![样本652D90](../../extensibility/ux-guidelines/media/0405-652d90.png "0405_652D90")|
|字段、枚举项、宏、结构、联合值类型、运算符、接口|VS 操作蓝|00539C / 0,83,156|![样本00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|Object|VS 操作绿色|388A34/56138、52|![样本388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|常量、异常、枚举项、映射、映射项、命名空间、模板、类型定义|背景（VS BG）|424242 / 66,66,66|![样本424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense 图标示例

||||||
|-|-|-|-|-|
|![IntelliSense 类 icon](../../extensibility/ux-guidelines/media/0405-36-intellisenseclass.png "0405-36_IntelliSenseClass") **类**|![IntelliSense 专用事件图标](../../extensibility/ux-guidelines/media/0405-37-intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")**私有事件**|![IntelliSense 委托图标](../../extensibility/ux-guidelines/media/0405-38-intellisensedelegate.png "0405-38_IntelliSenseDelegate")**委托**|![IntelliSense 方法 friend 图标](../../extensibility/ux-guidelines/media/0405-39-intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")**方法 friend**|![字段图标](../../extensibility/ux-guidelines/media/0405-40-field.png "0405-40_Field")**字段**|
|![IntelliSense 保护的枚举项图标](../../extensibility/ux-guidelines/media/0405-41-intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")**受保护的枚举项**|![IntelliSense 对象图标](../../extensibility/ux-guidelines/media/0405-42-intellisenseobject.png "0405-42_IntelliSenseObject")**对象**|![IntelliSense 模板图标](../../extensibility/ux-guidelines/media/0405-43-intellisensetemplate.png "0405-43_IntelliSenseTemplate")**模板**|![IntelliSense 异常快捷方式图标](../../extensibility/ux-guidelines/media/0405-44-intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")**异常快捷方式**||

### <a name="notifications"></a>通知
 Visual Studio 中的通知用于指示状态。 "通知" 面板使用以下四种颜色以及黑色或白色的前景填充选项来定义具有以下状态级别的通知。

|使用情况|名称|值（所有主题）|样板|
|-----------|----------|--------------------------|------------|
|状态：中性|通知蓝（与蓝色）|1BA1E2/27161226|![样本1BA1E2](../../extensibility/ux-guidelines/media/0405-1ba1e2.png "0405_1BA1E2")|
|状态：正值|通知绿色（与绿色）|339933 / 51,153,51|![样本339933](../../extensibility/ux-guidelines/media/0405-339933.png "0405_339933")|
|状态：负值|通知红色（与红色）|E51400/229，20，0|![样本 E51400](../../extensibility/ux-guidelines/media/0405-e51400.png "0405_E51400")|
|状态：警告|通知黄色（VS 橙色）|FFCC00/255204，0|![样本 FFCC00](../../extensibility/ux-guidelines/media/0405-ffcc00.png "0405_FFCC00")|
|前景填充|通知黑色（黑色）|000000 / 0,0,0|![样本&#35;000000](../../extensibility/ux-guidelines/media/0405-000000.png "0405_000000")|
|前景填充|通知（白色）|FFFFFF/255255255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知图标示例

|||||
|-|-|-|-|
|![警报图标](../../extensibility/ux-guidelines/media/0405-45-alert.png "0405-45_Alert")**警报**|![警告图标](../../extensibility/ux-guidelines/media/0405-48-warning.png "0405-48_Warning")**警告**|![完成图标](../../extensibility/ux-guidelines/media/0405-46-complete.png "0405-46_Complete")**完成**|![停止图标](../../extensibility/ux-guidelines/media/0405-47-stop.png "0405-47_Stop")**停止**|

### <a name="visual-studio-online"></a>Visual Studio Online
 通常，Visual Studio Online 包含浏览器中托管的功能。 在不同的环境中，颜色会有所不同，但样式会保持不变。

|组|使用情况|名称|值（所有主题）|样板|
|-----------|-----------|----------|--------------------------|------------|
|TFS|背景|TFSO BG|656565/ 101, 101, 101|![样本656565](../../extensibility/ux-guidelines/media/0405-656565.png "0405_656565")|
|TFS|轮廓|TFSO|FFFFFF/255、255、255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|Napa|背景|白色|FFFFFF/255、255、255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|摩纳哥|背景|白色|FFFFFF/255、255、255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|背景|白色|FFFFFF/255、255、255|![样本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|一般|F12 Grey_Primary|555555 / 85, 85, 85|![样本555555](../../extensibility/ux-guidelines/media/0405-555555.png "0405_555555")|
|F12|悬停|F12 Blue_Hover|2279BF / 34,121,191|![样本2279BF](../../extensibility/ux-guidelines/media/0405-2279bf.png "0405_2279BF")|
|F12|已禁用|F12 LtGrey_Disabled|ABABAC / 171,171,172|![样本 ABABAC](../../extensibility/ux-guidelines/media/0405-ababac.png "0405_ABABAC")|
|F12|悬停背景|悬停 bg|D9EBF7 / 217,235,247|![样本 D9EBF7](../../extensibility/ux-guidelines/media/0405-d9ebf7.png "0405_D9EBF7")|
|F12|按下背景|按下 bg|B2D7F0 / 178,215,240|![样本 B2D7F0](../../extensibility/ux-guidelines/media/0405-b2d7f0.png "0405_B2D7F0")|
|F12|轮廓|与外|F6F6F6 / 246,246,246|![样本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")|
|F12|信息|信息|00BCF2/0188242|![样本00BCF2](../../extensibility/ux-guidelines/media/0405-00bcf2.png "0405_00BCF2")|
|F12|警告|警告|F28300 / 242,131,0|![样本 F28300](../../extensibility/ux-guidelines/media/0405-f28300.png "0405_F28300")|
|F12|错误/负数|Error_Negative|E81123/232，17，35|![样本 E81123](../../extensibility/ux-guidelines/media/0405-e81123.png "0405_E81123")|
|F12|开始/正面|Start_Positive|009E49/0158，73|![样本009E49](../../extensibility/ux-guidelines/media/0405-009e49.png "0405_009E49")|
|F12|中断类型|中断类型|9B4F96/155，79150|![样本9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|F12|事件标记|事件标记|A51F00/165，31，0|![样本 A51F00](../../extensibility/ux-guidelines/media/0405-a51f00.png "0405_A51F00")|
|F12|用户标记|用户标记|F16220/241，98，32|![样本 F16220](../../extensibility/ux-guidelines/media/0405-f16220.png "0405_F16220")|

#### <a name="examples-of-visual-studio-online-icons"></a>Visual Studio Online 图标示例

|TFS Online||||
|----------------|-|-|-|
|![TFS online 团队图标](../../extensibility/ux-guidelines/media/0405-49-tfsonlineteam.png "0405-49_TFSOnlineTeam")**在线团队**|![TFS 信息图标](../../extensibility/ux-guidelines/media/0405-50-tfsinformation.png "0405-50_TFSInformation")**信息**|![TFS 历史记录图标](../../extensibility/ux-guidelines/media/0405-51-tfshistory.png "0405-51_TFSHistory")**历史记录**|![TFS 分支图标](../../extensibility/ux-guidelines/media/0405-52-tfsbranch.png "0405-52_TFSBranch")**分支**|

|Napa||||
|----------|-|-|-|
|![Napa 内容图标](../../extensibility/ux-guidelines/media/0405-53-napacontent.png "0405-53_NapaContent")**内容**|![Napa office mail 图标](../../extensibility/ux-guidelines/media/0405-54-napaofficemail.png "0405-54_NapaOfficeMail") **office mail**|![Napa sharepoint 图标](../../extensibility/ux-guidelines/media/0405-55-napasharepoint.png "0405-55_NapaSharePoint") **sharepoint**|![Napa 任务窗格图标](../../extensibility/ux-guidelines/media/0405-56-napataskpane.png "0405-56_NapaTaskPane")**任务窗格**|

|摩纳哥||||
|------------|-|-|-|
|![摩纳哥文件图标](../../extensibility/ux-guidelines/media/0405-57-monacofiles.png "0405-57_MonacoFiles")**文件**|![摩纳哥 git 图标](../../extensibility/ux-guidelines/media/0405-58-monacogit.png "0405-58_MonacoGit") **git**|![摩纳哥搜索图标](../../extensibility/ux-guidelines/media/0405-59-monacosearch.png "0405-59_MonacoSearch")**搜索**|![摩纳哥文本图标](../../extensibility/ux-guidelines/media/0405-60-monacotext.png "0405-60_MonacoText")**文本**|

|F12||||
|---------|-|-|-|
|![F12 漂亮代码图标](../../extensibility/ux-guidelines/media/0405-61-f12prettycode.png "0405-61_F12PrettyCode")**代码**太好|![F12 警告图标](../../extensibility/ux-guidelines/media/0405-62-f12warning.png "0405-62_F12Warning")**警告**|![F12 模拟图标](../../extensibility/ux-guidelines/media/0405-63-f12emulate.png "0405-63_F12Emulate")**模拟**|
