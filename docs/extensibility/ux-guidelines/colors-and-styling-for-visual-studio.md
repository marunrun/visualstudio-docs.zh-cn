---
title: Visual Studio 的颜色和样式 |Microsoft Docs
ms.date: 07/31/2017
ms.topic: conceptual
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: faded3e4a541ad899306e40bf9d46bf96a6b8ace
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338350"
---
# <a name="colors-and-styling-for-visual-studio"></a>Visual Studio 的颜色和样式

## <a name="use-color-in-visual-studio"></a>使用 Visual Studio 中的颜色

在 Visual Studio 中，颜色是主要用作通信工具，而不仅仅是作为修饰。 按最小方式使用颜色和保留的情况下，您希望对：

- 通信含义或隶属关系 （例如，平台或语言修饰符）

- 吸引注意力 （例如，指示状态更改）

- 提高可读性并提供用于导航 UI 的特征点

- 提高性能

将颜色分配到 Visual Studio 中的 UI 元素的存在多个选项。 有时可能很难进行图的选项，您就应该使用，或如何正确使用它。 本主题将帮助你：

- 了解不同的服务和系统用于在 Visual Studio 中定义的颜色。

- 选择给定元素的正确选项。

- 正确地使用你选择的选项。

> [!NOTE]
> 永远不会进行硬编码十六进制、 RGB 或到 UI 元素的系统颜色。 使用这些服务可以灵活地优化 hue。 此外，而无需服务，你将不能充分利用的主题切换功能[VSColor service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>将颜色分配到 Visual Studio 界面元素的方法

选择最适合你的 UI 元素的方法。

| 你的 UI | 方法 | 它们是什么？ |
| --- | --- | --- |
| 有嵌入或独立的对话框。 | **系统颜色** | 允许定义的颜色和外观的 UI 元素中，操作系统的系统名称，如通用对话框控件。 |
| 具有你想要与整体的 VS 环境保持一致的自定义 UI 和具有匹配的类别和语义含义的共享标记的 UI 元素。 | **公共共享的颜色** | 现有的预定义的颜色标记名称的特定 UI 元素 |
| 你有单个功能组并且没有类似的元素没有共享的颜色。 | **自定义颜色** | 特定于区域且不应与其他 UI，共享的颜色标记名称 |
| 你想要允许最终用户将自定义 UI 或内容 （例如，文本编辑器或专门的设计器窗口）。 | **最终用户自定义**<br /><br />**(工具&gt;选项对话框)** | 定义的"字体和颜色"页中设置**工具&gt;选项**对话框或特定于一个用户界面功能的专用的页面。 |

### <a name="visual-studio-themes"></a>Visual Studio 主题

Visual Studio 提供三种不同的颜色主题： 浅色、 深色，和蓝色。 它还检测高对比度模式，这是系统范围内颜色主题用于可访问性。

用户会提示您选择在其首次使用 Visual Studio 的过程主题，可以通过转到更高版本切换主题**工具&gt;选项&gt;环境&gt;常规**并选择从新的主题"颜色主题"下拉列表菜单。

用户还可以使用控制面板以其整个系统切换到多个高对比度主题之一。 如果用户选择高对比度主题，然后 Visual Studio 颜色主题选择器不会再影响颜色在 Visual Studio 中，虽然任何主题更改为在用户退出高对比度模式下时保存。 有关高对比度模式的详细信息，请参阅[选择高对比度颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors)。

### <a name="the-vscolor-service"></a>VSColor service

Visual Studio 提供了称为 VSColor 服务，可用于将 UI 元素的颜色值绑定到命名条目，其中包含每个 Visual Studio 主题的颜色值的环境颜色服务。 这可确保您的颜色将自动更改，以反映当前用户选择了主题或系统高对比度模式。 对服务的使用意味着在一个位置，处理所有与主题相关的颜色更改的实现，如果使用的从服务的公共共享的颜色，UI 将自动反映在 Visual Studio 的未来版本中的新主题。

### <a name="implementation"></a>实现

Visual Studio 源代码包括多个包定义文件，包含的标记名称和每个主题的各自的颜色值的列表。 颜色服务读取 VSColors 这些包定义文件中定义。 这些颜色将 XAML 标记中或在代码中引用并通过然后加载`IVsUIShell5.GetThemedColor`方法或 DynamicResource 映射。

### <a name="system-colors"></a>系统颜色

默认情况下，公共控件引用系统颜色。 如果您需要在用户界面使用系统颜色，如当您创建一个嵌入的或独立的对话框，您不必执行任何操作。

### <a name="common-shared-colors-in-the-vscolor-service"></a>VSColor 服务中的公共共享的颜色

界面元素应反映整体的 Visual Studio 环境。 通过重复使用公共共享的颜色适用于您正在设计的 UI 组件，可确保你的接口与其他 Visual Studio 接口，一致，并且，当您的颜色主题是添加或更新时，将自动更新。

使用之前公共共享的颜色，请确保你了解如何正确使用它们。 公共共享颜色的使用不正确可能会导致不一致，令人沮丧，或令人困惑的体验，为你的用户。

### <a name="user-customizable-colors"></a>用户可自定义颜色

请参阅：[为最终用户公开的颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

有时，您将想要允许最终用户将在代码编辑器或设计图面创建像一样自定义 UI。 可自定义 UI 组件都位于**字体和颜色**一部分**工具&gt;选项**对话框中，用户可以选择要更改的前景色、 背景色，或两者。

![工具&gt;选项对话框](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301 a_ToolsOptionsDialog")<br />工具&gt;选项对话框

## <a name="BKMK_TheVSColorService"></a> VSColor Service

Visual Studio 提供的环境颜色服务，也称为 VSColor service 或外壳颜色服务。 此服务，可将 UI 元素的颜色值绑定到集，其中包含每个主题颜色的名称-值颜色。 VSColor 服务必须用于所有 UI 元素，以便颜色自动更改以反映当前用户选择了主题，并以使 UI 绑定到的环境颜色服务将集成新的主题在将来版本的 Visual Studio。

### <a name="how-the-service-works"></a>服务工作原理

环境颜色服务读取 VSColors UI 组件.pkgdef 中定义。 这些 VSColors 然后在 XAML 标记或代码中引用并将其通过加载`IVsUIShell5.GetThemedColor`或`DynamicResource`映射。

![环境颜色服务体系结构](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302 a_EnvironmentColorServiceArchitecture")<br />环境颜色服务体系结构

### <a name="accessing-the-service"></a>访问服务

有几种不同方法访问使用 VSColor service，具体取决于哪种颜色标记您和您拥有哪种代码。

#### <a name="predefined-environment-colors"></a>预定义的环境颜色

##### <a name="from-native-code"></a>从本机代码

在 shell 提供了一种服务，提供对`COLORREF`的颜色。 服务/接口是：

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

文件 VSShell80.idl，枚举中`__VSSYSCOLOREX`具有 shell 颜色常量。 若要使用它，传入的索引值形式中的值之一`enum __VSSYSCOLOREX`记录在 MSDN 或常规索引号 Windows 系统 API， `GetSysColor`，接受。 执行此操作获取返回应在第二个参数中使用的颜色的 RGB 值。

如果存储笔或使用一种新颜色的画笔，则必须`AdviseBroadcastMessages`（从 Visual Studio shell 中) 和侦听`WM_SYSCOLORCHANGE`和`WM_THEMECHANGED`消息。

若要访问本机代码中的颜色服务，你将类似于下面这样的调用：

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> `COLORREF`返回的值`GetVSSysColorEx()`包含只是 R、 G、 B 组件的主题颜色。 如果主题项使用透明度，返回前丢弃的 alpha 通道值。 因此，如果感兴趣的环境颜色需要在透明度通道是重要的地方使用，则应使用`IVsUIShell5.GetThemedColor`而不是`IVsUIShell2::GetVSSysColorEx`，如本主题后面所述。

##### <a name="from-managed-code"></a>从托管代码

通过本机代码访问 VSColor service 其实非常简单。 如果你正在通过托管代码，但是，确定如何使用该服务可能比较棘手。 这一点后，下面是 C# 代码片段演示此过程：

```csharp
private void VSColorPaint(object sender, System.Windows.Forms.PaintEventArgs e)
{
    //getIVSUIShell2
    IVsUIShell2 uiShell2 = Package.GetService(typeof(SVsUIShell)) as IVsUIShell2;
    Debug.Assert (uiShell2 != null, "failed to get IVsUIShell2");

    if (uiShell2 != null)
    {
        //get the COLORREF structure
        uint win32Color;
        uiShell2.GetVSSysColorEx((int)__VSSYSCOLOREX.VSCOLOR_SMARTTAG_HOVER_FILL, out win32Color);

        //translate it to a managed Color structure
        Color myColor = ColorTranslator.FromWin32((int)win32Color);
        //use it
        e.Graphics.FillRectangle(new SolidBrush(myColor), 0, 0, 100, 100);
    }
}
```

如果您正在 Visual Basic 中，使用：

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>从 WPF UI

可以绑定到通过值导出到应用程序的 Visual Studio 颜色`ResourceDictionary`。 下面是使用颜色表中的资源，以及绑定到 XAML 中的环境字体数据的示例。

```xml
<Style TargetType="{x:Type Button}">
    <Setter Property="TextBlock.FontFamily"
            Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
    <Setter Property="TextBlock.FontSize"
            Value="{DynamicResource VsFont.EnvironmentFontSize}" />
    <Setter Property="Background"
            Value="{DynamicResource VsBrush.EnvironmentBackgroundGradient}" />
</Style>
```

#### <a name="helper-classes-and-methods-for-managed-code"></a>帮助器类和托管代码的方法

对于托管代码，shell 的托管包框架库 (`Microsoft.VisualStudio.Shell.12.0.dll`) 包含几个帮助程序类促进使用主题颜色。

中的帮助器方法`Microsoft.VisualStudio.Shell.VsColors`MPF 中的类包括`GetThemedGDIColor()`和`GetThemedWPFColor()`。 这些帮助器方法返回的主题项作为颜色值`System.Drawing.Color`或`System.Windows.Media.Color`、 WinForms 或 WPF UI 中使用。

```csharp
IVsUIShell5 shell5;
Button button = new Button();
button.BackColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemBrushKey);
button.ForeColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemTextBrushKey);

/// <summary>
/// Gets a System.Drawing.Color value from the current theme for the given color key.
/// </summary>
/// <param name="vsUIShell">The IVsUIShell5 service, used to get the color's value.</param>
/// <param name="themeResourceKey">The key to find the color for.</param>
/// <returns>The current theme's value of the named color.</returns>
public static System.Drawing.Color GetThemedGDIColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Validate.IsNotNull(vsUIShell, "vsUIShell");
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");

   byte[] colorComponents = GetThemedColorRgba(vsUIShell, themeResourceKey);

   // Note: The Win32 color we get back from IVsUIShell5.GetThemedColor is ABGR
   return System.Drawing.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);
}

private static byte[] GetThemedColorRgba(IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Guid category = themeResourceKey.Category;
   __THEMEDCOLORTYPE colorType = __THEMEDCOLORTYPE.TCT_Foreground
   if (themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundColor || themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundBrush)
   {
      colorType = __THEMEDCOLORTYPE.TCT_Background;
   }

   // This call will throw an exception if the color is not found
   uint rgbaColor = vsUIShell.GetThemedColor(ref category, themeResourceKey.Name, (uint)colorType);
   return BitConverter.GetBytes(rgbaColor);
}
public static System.Windows.Media.Color GetThemedWPFColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Validate.IsNotNull(vsUIShell, "vsUIShell");
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");

   byte[] colorComponents = GetThemedColorComponents(vsUIShell, themeResourceKey);

    return System.Windows.Media.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);
}
```

类还可用于获取给定 WPF 颜色资源键，VSCOLOR 标识符，反之亦然。

```csharp
public static string GetColorBaseKey(int vsSysColor);
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);
```

方法`VsColors`类查询 VSColor 服务以返回每次调用它们的颜色值。 若要获取颜色值是`System.Drawing.Color`，从而提高了性能的替代方法是改为使用的方法`Microsoft.VisualStudio.PlatformUI.VSThemeColor`类，该类将缓存从 VSColor 服务获取的颜色值。 类在内部订阅 shell 广播的消息事件和主题更改事件发生时将放弃缓存的值。 此外，此类提供。要订阅主题更改的 NET 友好事件。 使用`ThemeChanged`事件来添加新的处理程序，并使用`GetThemedColor()`方法来获取颜色值`ThemeResourceKeys`感兴趣。 示例代码可能如下所示：

```csharp
public MyWindowPanel()
{
    InitializeComponent();

    // Subscribe to theme changes events so we can refresh the colors
    VSColorTheme.ThemeChanged += VSColorTheme_ThemeChanged;

    RefreshColors();
}

private void VSColorTheme_ThemeChanged(ThemeChangedEventArgs e)
{
    RefreshColors();

    // Also post a message to all the children so they can apply the current theme appropriately
    foreach (System.Windows.Forms.Control child in this.Controls)
    {
        NativeMethods.SendMessage(child.Handle, e.Message, IntPtr.Zero, IntPtr.Zero);
    }
}

private void RefreshColors()
{
    this.BackColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowBackgroundColorKey);
    this.ForeColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowTextColorKey);
}

protected override void Dispose(bool disposing)
{
    if (disposing)
    {
        VSColorTheme.ThemeChanged -= this.VSColorTheme_ThemeChanged;
        base.Dispose(disposing);}
}
```

## <a name="BKMK_ChoosingHighContrastColors"></a> 选择高对比度颜色

### <a name="overview"></a>概述

Windows 使用增加的文本、 背景和图像的色彩对比度的多个高对比度系统级主题使元素显示在屏幕上更为明显。 可访问性原因，务必在用户切换到高对比度主题时，Visual Studio 界面元素做出正确响应。

只有几种系统颜色可用于高对比度主题。 在选择您的系统颜色名称时，请记住以下提示：

- **选择具有相同的语义含义的系统颜色**着色的元素。 例如，如果您所选择的时间段内的文本的高对比度颜色，使用 WindowText 和不 ControlText。

- **选择前景/背景对**一起或不会相信您的颜色选择，将所有高对比度主题中正常工作。

- **确定你的 UI 中的哪些部分是最重要，并确保将脱颖而出的内容区域。** 因此强边框颜色的使用通常定义的内容区域，因为有不同的内容区域没有颜色变体，您将丢失详细信息，通常会区分颜色色调细微的差异，很的多。

### <a name="system-color-set"></a>系统颜色集

在表[WPF 团队博客：SystemColors 引用](https://blogs.msdn.microsoft.com/wpf/2010/11/30/systemcolors-reference/)指示一整套的系统颜色的名称，并显示在每个主题对应色调。

如果应用此限制的一组到你的 UI，颜色*预期，将会丢失细节"正常"主题中存在的*。 下面是用户界面的示例，用于区分工具窗口中的区域的细微灰颜色。 如果使用在高对比度模式下显示的同一窗口搭配使用，可以看到，所有背景相同的色调，由边框单独指示这些区域的边框：

![在高对比度如何细微的详细信息的示例会丢失](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303 a_PropertiesWindow")<br />在高对比度会丢失如何细微的详细信息的示例

#### <a name="choosing-text-colors-in-an-editor"></a>在编辑器中选择文本颜色

在编辑器中或设计图面上使用以的文本，以指示含义，例如允许的简单标识的相似项的组。 在高对比度主题，但是，您没有的功能来区分多个三种文本颜色。 WindowText、 GrayText 和 HotTrackText WindowBackground 图面上提供的唯一颜色。 由于不能使用三个以上的颜色，请仔细选择你想要在高对比度模式中显示的最重要差异。

在每个高对比度主题中的显示上一个编辑器图面中，允许的标记名称的每个色调：

![高对比度编辑器比较](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303 b_HCEditorComparison")<br />高对比度编辑器比较

编辑器表面蓝色主题中的示例：

![蓝色主题中的编辑器](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303 c_EditorBlue")<br />蓝色主题中的编辑器

![高对比度 #1 主题中的编辑器](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303 d_EditorHC1")<br />高对比度 #1 主题中的编辑器

### <a name="usage-patterns"></a>使用模式

许多常用的 UI 元素已定义的高对比度颜色。 以便你的 UI 元素与类似组件保持一致，可以选择自己的系统颜色名称时引用这些使用情况模式。

| 系统颜色 | 用法 |
| --- | --- |
| ActiveCaption | -Active IDE 和 rafted 的窗口按钮上悬停并按标志符号<br />-为 IDE 和 rafted 的 windows 标题栏背景<br />默认状态栏背景 |
| ActiveCaptionText | -Active IDE 和 rafted 的窗口标题栏前景 （文本和字形）<br />的背景和边框上悬停并按活动窗口按钮 |
| 控件 | -组合框、 下拉列表和搜索控制默认和已禁用背景信息，包括下拉按钮<br />-停靠目标按钮背景<br />命令栏背景<br />-工具窗口背景 |
| ControlDark | -IDE 背景<br />菜单和命令栏分隔符<br />命令栏边框<br />隐藏菜单<br />-工具窗口选项卡上的默认值并将鼠标悬停边框和分隔符<br />-还文档溢出按钮背景<br />-停靠目标标志符号边框 |
| ControlDarkDark |-失去焦点的选定文档选项卡窗口 |
| ControlLight |-自动隐藏选项卡边框<br />列表式组合框和下拉列表边框<br />-停靠目标背景和边框 |
| ControlLightLight | -已选定、 已设定焦点的临时窗口边框 |
| ControlText | 列表式组合框和下拉列表标志符号<br />-工具窗口中取消选择选项卡文本 |
| GrayText |的禁用边框、 下拉标志符号、 文本和菜单项文本组合框和下拉列表<br />-已禁用的菜单文本<br />搜索控件搜索选项标头文本<br />搜索控制部分分隔符 |
| 突出显示 | -所有悬停和按下的背景和边框，除组合框下拉按钮背景和文档以及溢出按钮边框<br />-选定项背景 |
| HighlightText | -所有悬停和按下的前景色 （文本和字形）<br />-已设定焦点的工具窗口和文档选项卡窗口控件的前景<br />-已设定焦点的工具窗口标题栏边框<br />的前景色集中的所选的临时选项卡<br />-还文档溢出按钮边框上悬停并按<br />-所选图标边框|
| HotTrack | -滚动条滚动块背景和按下时的边框<br />-滚动条在按下的箭头标志符号 |
| InactiveCaption | 非活动状态的 IDE 和 rafted 的窗口按钮上悬停标志符号<br />-为 IDE 和 rafted 的 windows 标题栏背景<br />-已禁用的搜索控件背景 |
| InactiveCaptionText | 非活动状态的 IDE 和 rafted 的 windows 标题栏前景 （文本和字形）<br />非活动窗口按钮背景和悬停时的边框<br />-失去焦点的工具窗口按钮背景和边框<br />-已禁用的搜索控件的前景 |
| 菜单 | -下拉列表菜单背景<br />-选中和禁用的复选标记背景 |
| MenuText | -下拉列表菜单边框<br />-选中标记<br />菜单标志符号<br />-下拉列表菜单文本<br />-所选图标边框 |
| Scrollbar | -滚动栏和滚动条箭头的背景信息，所有状态 |
| 窗口 | -自动隐藏选项卡背景<br />菜单栏和命令架背景<br />-失去焦点或未选定的文档窗口选项卡背景和文档边框，用于打开和临时选项卡<br />-失去焦点的工具窗口标题栏背景<br />-工具窗口选项卡背景，同时选中和取消选择 |
| WindowFrame | -IDE 边框 |
| WindowText | -自动隐藏选项卡上的前景色<br />-所选工具窗口选项卡前景色<br />-失去焦点或未选定的临时选项卡前景色和失去焦点的文档窗口选项卡<br />-未选定标志符号通过树视图默认前景色和悬停<br />的所选工具窗口选项卡边框<br />-滚动条滚动块背景、 边框和标志符号 |

## <a name="BKMK_ExposingColorsForEndUsers"></a> 为最终用户公开的颜色

### <a name="overview"></a>概述

有时你会想要允许最终用户将在代码编辑器或设计图面创建时像一样自定义 UI。 若要执行此操作的最常见方法是通过使用**工具&gt;选项**对话框。 除非您拥有高度专业化需要特殊的控件的 UI，以提供自定义项的最简单方法是通过**字体和颜色**页内**环境**对话框部分。 对于公开自定义每个元素，用户可以选择更改的前景色、 背景色，或两者。

### <a name="building-a-vspackage-for-your-customizable-colors"></a>构建您的可自定义颜色的 VSPackage

VSPackage 可以控制字体和通过自定义类别的颜色和字体和颜色属性页上显示项。 在使用此机制，Vspackage 必须实现[IVsFontAndColorDefaultsProvider](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider)接口和其关联的接口。

从原理上讲，此机制可用于修改显示的所有现有项目和包含它们的类别。 但是，它不应修改文本编辑器类别或其显示项。 文本编辑器类别的详细信息，请参阅[字体和颜色概述](../font-and-color-overview.md)。

若要实现自定义类别或显示的项，VSPackage 必须：

- **创建或标识注册表中的类别。** IDE 的实现**字体和颜色**属性页使用此信息来正确地查询支持给定的类别的服务。

- **创建或标识 （可选） 在注册表中的组。** 它可能是很适合用于定义一个表示集合的两个或多个类别的组。 如果定义一个组，则 IDE 将自动合并子类别，并将分发在组中的显示项。

- **实现 IDE 的支持。**

- **处理更改字体和颜色。**

#### <a name="to-create-or-identify-categories"></a>若要创建或标识类别

构造一个特殊类型的类别下的注册表项`[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]`其中`<Category>`类别的非本地化名称。

填充注册表具有两个值：

| 名称 | 类型 | 数据 | 描述 |
| --- | --- | --- | --- |
| 类别 | REG_SZ | GUID | 创建标识类别的 GUID |
| package | REG_SZ | GUID | 支持类别的 VSPackage 服务的 GUID |

 在注册表中指定的服务必须提供的实现[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)相应类别。

#### <a name="to-create-or-identify-groups"></a>若要创建或标识组

构造一个特殊类型的类别下的注册表项`[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]`其中`<group>`是组的非本地化名称。

填充注册表具有两个值：

| 名称 | 类型 | 数据 | 描述 |
|--- | --- | --- | --- |
| 类别 | REG_SZ | GUID | 创建标识类别的 GUID |
| package | REG_SZ | GUID | 支持类别的 VSPackage 服务的 GUID |

在注册表中指定的服务必须提供的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>为相应的组。

![实现 IVsFontAndColorGroup](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304 a_FontAndColorGroup")<br />实现 `IVsFontAndColorGroup`

### <a name="to-implement-ide-support"></a>若要实现 IDE 支持

实现[GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject)，这会返回任一[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)接口或<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>接口到每个类别 IDE 或组提供的 GUID。

它支持每个类别，VSPackage 实现的一个单独实例[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)接口。

通过包实现的方法[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)必须提供与 IDE:

- 类别中显示项的列表

- 显示项的可本地化名称

- 显示类别的每个成员的信息

> [!NOTE]
> 每个类别必须包含至少一个显示项。

IDE 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>接口可定义多个类别的联合。

其实现提供了与 IDE:

- 构成了一组给定的类别的列表

- 对实例的访问[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)支持组内的每个类别

- 可本地化的组名称

#### <a name="updating-the-ide"></a>正在更新 IDE

IDE 将缓存有关字体和颜色设置的信息。 因此，任何修改后的 IDE 字体和颜色配置，确保缓存最新的是一种最佳做法。

更新缓存是通过[IvsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager)接口，并可执行全局或仅在所选的项。

### <a name="handling-font-and-color-changes"></a>处理字体和颜色更改

若要正确支持 VSPackage 显示的文本的颜色，支持 VSPackage 的着色服务必须响应通过的字体和颜色属性页所做的用户启动的更改。

若要执行此操作，VSPackage 必须：

- **处理 IDE 生成的事件**通过实现[IVsFontAndColorEvents](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents)接口。 IDE 调用后面的字体和颜色页的用户修改的相应方法。 例如，它调用[OnFontChanged](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged)如果选择新字体的方法。

  **或**

- **轮询更改 IDE**。 这可以通过系统实现[IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)接口。 主要用于支持暂留，尽管[GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem)方法可以获取显示项的字体和颜色信息。 字体和颜色设置的详细信息，请参阅 MSDN 文章[访问存储的字体和颜色设置](../accessing-stored-font-and-color-settings.md)。

> [!NOTE]
> 若要确保轮询结果是否正确，请使用[IVsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager)接口，以确定是否刷新的缓存和 update 之前调用的检索方法所需[IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)接口。

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>注册自定义字体和颜色类别，无需实现接口

下面的代码示例演示如何注册自定义字体和颜色而无需实现接口的类别：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"

    "NameID"=dword:00000064
```

此代码示例：

- `"NameID"` = 在包中的本地化的类别名称的资源 ID
- `"ToolWindowPackage"` = 包 GUID
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"` 只是一个示例和实际值可以是由实现者提供一个新的 GUID。

### <a name="set-the-font-and-color-property-category-guid"></a>设置字体和颜色的属性类别的 GUID

下面的代码示例演示如何设置类别的 Guid。

```csharp
// m_pView is your IVsTextView
IVsTextEditorPropertyCategoryContainer spPropCatContainer =
(IVsTextEditorPropertyCategoryContainer)m_pView;
if (spPropCatContainer != null)
{
IVsTextEditorPropertyContainer spPropContainer;
Guid GUID_EditPropCategory_View_MasterSettings =
new Guid("{D1756E7C-B7FD-49a8-B48E-87B14A55655A}");
hr = spPropCatContainer.GetPropertyCategory(
ref GUID_EditPropCategory_View_MasterSettings,
out spPropContainer);
if(hr == 0)
{
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_FontCategory,
catGUID);
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_ColorCategory,
catGUID);
}
}
```
