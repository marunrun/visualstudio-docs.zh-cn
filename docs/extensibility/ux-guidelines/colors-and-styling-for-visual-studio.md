---
title: 视觉工作室的颜色和造型 |微软文档
ms.date: 07/31/2017
ms.topic: conceptual
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2c7d8a02de9331f268cd06ad35e19faab6494fe0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699855"
---
# <a name="colors-and-styling-for-visual-studio"></a>Visual Studio 的颜色和样式

## <a name="use-color-in-visual-studio"></a>在视觉工作室中使用颜色

在视觉工作室中，颜色主要用作通信工具，而不仅仅是装饰。 最小使用颜色，并保留它的情况，你想：

- 传达含义或隶属关系（例如，平台或语言修改器）

- 吸引注意力（例如，指示状态更改）

- 提高可读性并提供用于导航 UI 的地标

- 提高可取性

在 Visual Studio 中，存在将颜色分配给 UI 元素的几个选项。 有时，很难确定您应该使用哪个选项，或者如何正确使用它。 本主题将帮助您：

- 了解用于在 Visual Studio 中定义颜色的不同服务和系统。

- 为给定元素选择正确的选项。

- 正确使用您选择的选项。

> [!NOTE]
> 切勿对 UI 元素硬编码十六进制、RGB 或系统颜色。 使用服务可以灵活地调整色调。 此外，如果没有该服务，您将无法利用[VSColor 服务](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)的主题切换功能。

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>为可视化工作室界面元素分配颜色的方法

选择最适合 UI 元素的方法。

| 您的 UI | 方法 | 它们是什么？ |
| --- | --- | --- |
| 您有嵌入的或独立的对话框。 | **系统颜色** | 允许操作系统定义 UI 元素的颜色和外观的系统名称，如通用对话框控件。 |
| 您有要与整个 VS 环境一致的自定义 UI，并且具有与共享令牌的类别和语义含义相匹配的 UI 元素。 | **常见共享颜色** | 特定 UI 元素的现有预定义颜色令牌名称 |
| 您具有单个要素或一组要素，并且没有类似元素的共享颜色。 | **自定义颜色** | 特定于区域且不打算与其他 UI 共享的颜色令牌名称 |
| 您希望允许最终用户自定义 UI 或内容（例如，对于文本编辑器或专用设计器窗口）。 | **最终用户自定义**<br /><br />**（工具&gt;选项对话框）** | **在"工具&gt;选项**"对话框的"字体和颜色"页或特定于一个 UI 功能的专用页面中定义的设置。 |

### <a name="visual-studio-themes"></a>视觉工作室主题

Visual Studio 具有三种不同的颜色主题：浅色、深色和蓝色。 它还检测高对比度模式，这是专为辅助功能而设计的全系统颜色主题。

在首次使用 Visual Studio 时，系统会提示用户选择主题，并稍后通过转到 **"工具选项&gt;环境&gt;常规&gt;"** 并从"颜色主题"下拉菜单中选择新主题来切换主题。

用户还可以使用控制面板将其整个系统切换到几个高对比度主题之一。 如果用户选择高对比度主题，则 Visual Studio 颜色主题选择器不再影响 Visual Studio 中的颜色，尽管当用户退出高对比度模式时，将保存任何主题更改。 有关高对比度模式的详细信息，请参阅[选择高对比度颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors)。

### <a name="the-vscolor-service"></a>VSColor 服务

Visual Studio 提供一种称为 VSColor 服务的环境颜色服务，该服务允许您将 UI 元素的颜色值绑定到包含每个 Visual Studio 主题颜色值的命名条目。 这可确保颜色将自动更改以反映当前用户选择的主题或系统高对比度模式。 使用该服务意味着所有主题相关颜色更改的实现都在一个位置处理，如果您使用服务中的常见共享颜色，则 UI 将自动反映 Visual Studio 的未来版本中的新主题。

### <a name="implementation"></a>实现

Visual Studio 源代码包括多个包定义文件，其中包含令牌名称列表和每个主题的相应颜色值。 颜色服务读取这些包定义文件中定义的 VSColors。 这些颜色在 XAML 标记或代码中引用，然后通过`IVsUIShell5.GetThemedColor`方法或动态资源映射加载。

### <a name="system-colors"></a>系统颜色

默认情况下，公共控件引用系统颜色。 如果希望 UI 使用系统颜色（如创建嵌入或独立对话框时），则无需执行任何操作。

### <a name="common-shared-colors-in-the-vscolor-service"></a>VSColor 服务中的常见共享颜色

您的界面元素应反映整个可视化工作室环境。 通过重用适用于所设计的 UI 组件的常见共享颜色，可确保界面与其他 Visual Studio 界面一致，并确保在添加或更新主题时颜色将自动更新。

在使用公共共享颜色之前，请确保您了解如何正确使用它们。 对常见共享颜色的不正确使用可能会导致用户体验不一致、令人沮丧或混乱。

### <a name="user-customizable-colors"></a>用户可自定义的颜色

请参阅：[为最终用户公开颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

有时，您需要允许最终用户自定义 UI，例如创建代码编辑器或设计图面时。 可自定义的 UI 组件位于 **"&gt;工具选项"** 对话框的"**字体和颜色**"部分，用户可以选择更改前景颜色、背景颜色或两者。

![工具&gt;选项对话框](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301-a_ToolsOptionsDialog")<br />工具&gt;选项对话框

## <a name="the-vscolor-service"></a><a name="BKMK_TheVSColorService"></a>VSColor 服务

Visual Studio 提供环境颜色服务，也称为 VSColor 服务或外壳颜色服务。 此服务允许您将 UI 元素的颜色值绑定到包含每个主题颜色的名称值颜色集。 VSColor 服务必须用于所有 UI 元素，以便颜色自动更改以反映当前用户选择的主题，以便绑定到环境颜色服务的 UI 将与 Visual Studio 的未来版本中的新主题集成。

### <a name="how-the-service-works"></a>服务的工作原理

环境颜色服务读取在 .pkgdef 中定义的 UI 组件中的 VSColors。 然后，这些 VSColors 在 XAML 标记或代码中引用，并通过`IVsUIShell5.GetThemedColor`或`DynamicResource`映射加载。

![环境颜色服务体系结构](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302-a_EnvironmentColorServiceArchitecture")<br />环境颜色服务体系结构

### <a name="accessing-the-service"></a>访问服务

有几种不同的方法来访问 VSColor 服务，具体取决于您正在使用的颜色令牌类型以及您拥有的代码类型。

#### <a name="predefined-environment-colors"></a>预定义环境颜色

##### <a name="from-native-code"></a>从本机代码

shell 提供一种服务，该服务允许访问`COLORREF`颜色。 服务/接口是：

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

在文件 VSShell80.idl 中，枚举`__VSSYSCOLOREX`具有外壳颜色常量。 要使用它，请传入为索引值，从 MSDN`enum __VSSYSCOLOREX`中记录的值之一或 Windows 系统 API`GetSysColor`接受的常规索引号。 执行此操作将返回应在第二个参数中使用的颜色的 RGB 值。

如果存储具有新颜色的笔或画笔，则必须`AdviseBroadcastMessages`（关闭 Visual Studio 外壳）并侦听`WM_SYSCOLORCHANGE`和`WM_THEMECHANGED`消息。

要访问本机代码中的颜色服务，您将进行类似于以下的调用：

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> 返回`COLORREF``GetVSSysColorEx()`的值仅包含主题颜色的 R、G、B 组件。 如果主题条目使用透明度，则在返回之前将丢弃 alpha 通道值。 因此，如果需要在透明度通道很重要的地方使用感兴趣的环境颜色，则应使用`IVsUIShell5.GetThemedColor`而不是`IVsUIShell2::GetVSSysColorEx`，如本主题后面所述。

##### <a name="from-managed-code"></a>从托管代码

通过本机代码访问 VSColor 服务相当简单。 但是，如果您正在处理托管代码，则确定如何使用服务可能比较棘手。 考虑到这一点，下面是一个 C# 代码段，演示了此过程：

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

如果您在可视化基础中工作，请使用：

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>从 WPF UI

您可以通过导出到应用程序的 的值绑定到 Visual Studio 颜色`ResourceDictionary`。 下面是使用颜色表中的资源以及绑定到 XAML 中的环境字体数据的示例。

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

#### <a name="helper-classes-and-methods-for-managed-code"></a>托管代码的帮助器类和方法

对于托管代码，shell 的托管包框架库 （`Microsoft.VisualStudio.Shell.12.0.dll`） 包含几个帮助器类，便于使用主题颜色。

MPF 类中的`Microsoft.VisualStudio.Shell.VsColors`帮助器方法包括`GetThemedGDIColor()`和`GetThemedWPFColor()`。 这些帮助器方法返回主题条目的颜色值，作为`System.Drawing.Color`或`System.Windows.Media.Color`，用于 WinForms 或 WPF UI。

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

该类还可用于获取给定 WPF 颜色资源键的 VSCOLOR 标识符，反之亦然。

```csharp
public static string GetColorBaseKey(int vsSysColor);
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);
```

`VsColors`类查询 VSColor 服务的方法，以在每次调用颜色值时返回颜色值。 要获取颜色值，`System.Drawing.Color`性能更好的替代方法是使用`Microsoft.VisualStudio.PlatformUI.VSThemeColor`类的方法，该方法缓存从 VSColor 服务获取的颜色值。 类在内部订阅 shell 广播消息事件，并在发生主题更改事件时丢弃缓存的值。 此外，类提供 。NET 友好活动，用于订阅主题更改。 使用`ThemeChanged`事件添加新处理程序，并使用`GetThemedColor()`方法获取感兴趣的颜色值。 `ThemeResourceKeys` 示例代码可能如下所示：

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

## <a name="choosing-high-contrast-colors"></a><a name="BKMK_ChoosingHighContrastColors"></a>选择高对比度颜色

### <a name="overview"></a>概述

Windows 使用多个高对比度的系统级主题，这些主题可增加文本、背景和图像的颜色对比度，从而使元素在屏幕上显得更加清晰。 出于辅助功能的原因，当用户切换到高对比度主题时，Visual Studio 界面元素正确响应非常重要。

只有少量系统颜色可用于高对比度主题。 选择系统颜色名称时，请记住以下提示：

- 选择与着色的元素**具有相同语义含义的系统颜色**。 例如，如果要为窗口中的文本选择高对比度颜色，请使用 WindowText 而不是 ControlText。

- **一起选择前景/背景对**，否则您不会确信您的颜色选择在所有高对比度主题中都起作用。

- **确定 UI 的哪些部分最重要，并确保内容区域脱颖而出。** 您将失去颜色色调的细微差异通常会区分的很多细节，因此使用强边框颜色是定义内容区域的常见内容，因为不同内容区域没有颜色变体。

### <a name="system-color-set"></a>系统颜色集

[WPF 团队博客中的表：系统颜色参考](https://blogs.msdn.microsoft.com/wpf/2010/11/30/systemcolors-reference/)指示完整的系统颜色名称集，以及每个主题中显示的相应色调。

当将这种有限的颜色集应用于 UI 时 *，预计您将丢失"正常"主题中存在的细微细节*。 下面是一个带有微妙灰色 UI 的示例，用于区分工具窗口中的区域。 与在高对比度模式下显示的同一窗口配对时，您可以看到所有背景都具有相同的色调，并且这些区域的边界仅由边框表示：

![高对比度中如何丢失细微细节的示例](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303-a_PropertiesWindow")<br />高对比度中如何丢失细微细节的示例

#### <a name="choosing-text-colors-in-an-editor"></a>在编辑器中选择文本颜色

着色文本用于编辑器或设计表面以指示含义，例如允许轻松识别类似项组。 但是，在高对比度主题中，您无法区分三种以上文本颜色。 窗口文本、灰色文本和热轨道文本是窗口背景曲面上唯一可用的颜色。 由于不能使用三种颜色以上，请仔细选择在高对比度模式下要显示的最重要差异。

编辑器曲面上允许的每个令牌名称的色调，因为它们出现在每个高对比度主题中：

![高对比度编辑器比较](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303-b_HCEditorComparison")<br />高对比度编辑器比较

蓝色主题中编辑器表面的示例：

![蓝色主题中的编辑器](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303-c_EditorBlue")<br />蓝色主题中的编辑器

![高对比度#1主题的编辑](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303-d_EditorHC1")<br />高对比度#1主题的编辑

### <a name="usage-patterns"></a>使用模式

许多常见的 UI 元素已定义了高对比度颜色。 在选择自己的系统颜色名称时，可以引用这些使用模式，以便 UI 元素与类似的组件一致。

| 系统颜色 | 使用情况 |
| --- | --- |
| ActiveCaption | - 活动 IDE 和漂流窗口按钮字形悬停并按下<br />- IDE 和漂流窗口的标题栏背景<br />- 默认状态栏背景 |
| ActiveCaptionText | - 标题栏前景的活动 IDE 和漂流窗口（文本和字形）<br />- 悬停上活动窗口按钮的背景和边框，然后按 |
| 控制 | - 组合框、下拉列表以及搜索控件默认和禁用的背景，包括下拉按钮<br />- 停靠目标按钮背景<br />- 命令栏背景<br />- 工具窗口背景 |
| ControlDark | - IDE 背景<br />- 菜单和命令栏分隔符<br />- 命令栏边框<br />- 菜单阴影<br />- 工具窗口选项卡默认值和悬停边框和分隔符<br />- 记录溢出按钮背景<br />- 停靠目标字形边框 |
| ControlDarkDark |- 未聚焦、选定的文档选项卡窗口 |
| ControlLight |- 自动隐藏选项卡边框<br />- 组合框和下拉列表边框<br />- 停靠目标背景和边框 |
| 控制灯 | - 选定、重点突出的临时边界 |
| 控件文本 | - 组合框和下拉列表字形<br />- 工具窗口未选中选项卡文本 |
| 灰色文本 |- 组合框和下拉列表禁用边框、下拉字、文本和菜单项文本<br />- 禁用菜单文本<br />- 搜索控件"搜索选项"标题文本<br />- 搜索控制截面分隔符 |
| 突出显示 | - 所有悬停和按下的背景和边框，但组合框下拉按钮背景和文档溢出按钮边框<br />- 选定的项目背景 |
| 突出显示文本 | - 所有悬停和按下的前景（文本和字形）<br />- 聚焦工具窗口和文档选项卡窗口控制前景<br />- 聚焦工具窗口标题栏边框<br />- 聚焦、选定的临时选项卡前景<br />- 在悬停上记录溢流按钮边框，然后按<br />- 选定的图标边框|
| 热轨道 | - 按压上滚动条拇指背景和边框<br />- 按压时滚动条箭头字形 |
| 非活动标题 | - 悬停时非活动 IDE 和漂流窗口按钮字形<br />- IDE 和漂流窗口的标题栏背景<br />- 禁用的搜索控制背景 |
| 非活动字幕文本 | - 非活动 IDE 和漂流窗口标题栏前景（文本和字形）<br />- 非活动窗口按钮背景和悬停边框<br />- 无焦点工具窗口按钮背景和边框<br />- 禁用的搜索控制前景 |
| 菜单 | - 下拉菜单背景<br />- 已选中并禁用复选标记背景 |
| 菜单文本 | - 下拉菜单边框<br />- 检查标记<br />- 菜单字形<br />- 下拉菜单文本<br />- 选定的图标边框 |
| Scrollbar | - 滚动条和滚动条箭头背景，所有状态 |
| 窗口 | - 自动隐藏选项卡背景<br />- 菜单栏和命令搁板背景<br />- 未聚焦或未选择的文档窗口选项卡背景和文档边框，适用于打开和临时选项卡<br />- 无焦点工具窗口标题栏背景<br />- 工具窗口选项卡背景，已选择和未选中 |
| 窗口框架 | - IDE 边框 |
| 窗口文本 | - 自动隐藏选项卡前景<br />- 选定的工具窗口选项卡前景<br />- 未聚焦的文档窗口选项卡和未聚焦或未选中的临时选项卡前景<br />- 树视图默认前景，并将鼠标悬停在未选择的字形上<br />- 工具窗口选择选项卡边框<br />- 滚动条拇指背景、边框和字形 |

## <a name="exposing-colors-for-end-users"></a><a name="BKMK_ExposingColorsForEndUsers"></a>为最终用户公开颜色

### <a name="overview"></a>概述

有时，您希望允许最终用户自定义 UI，例如创建代码编辑器或设计图面时。 最常见的方法是使用 **"工具&gt;选项"** 对话框。 除非您具有需要特殊控件的高度专业化 UI，否则显示自定义的最简单方法是通过对话框 **"环境**"部分中的 **"字体和颜色**"页。 对于要自定义公开的每个元素，用户可以选择更改前景颜色、背景颜色或两者。

### <a name="building-a-vspackage-for-your-customizable-colors"></a>为可自定义的颜色构建 VS 包

VSPackage 可以通过自定义类别控制字体和颜色，并在"字体和颜色"属性页上显示项目。 使用此机制时，VSPackages 必须实现[IVsFontAndColorDefaults 提供程序接口](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider)及其关联的接口。

原则上，此机制可用于修改所有现有的显示项及其包含它们的类别。 但是，它不应用于修改文本编辑器类别或其显示项。 有关文本编辑器类别的详细信息，请参阅[字体和颜色概述](/visualstudio/extensibility/font-and-color-overview?view=vs-2015)。

要实现自定义类别或显示项目，VS 包必须：

- **创建或标识注册表中的类别。** IDE 的 **"字体和颜色**"属性页的实现使用此信息正确查询支持给定类别的服务。

- **在注册表中创建或标识组（可选）。** 定义表示两个或多个类别的联合的组可能很有用。 如果定义了组，IDE 将自动合并子类别并在组中分发显示项。

- **实施 IDE 支持。**

- **处理字体和颜色更改。**

#### <a name="to-create-or-identify-categories"></a>创建或标识类别

构造特殊类型的类别注册表项，其`[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]``<Category>`下是类别的非本地化名称。

使用两个值填充注册表：

| 名称 | 类型 | 数据 | 描述 |
| --- | --- | --- | --- |
| 类别 | REG_SZ | GUID | 为识别类别而创建的 GUID |
| 程序包 | REG_SZ | GUID | 支持类别的 VSPackage 服务的 GUID |

 注册表中指定的服务必须为相应的类别提供[IVsFontAndColorDefaults 的](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)实现。

#### <a name="to-create-or-identify-groups"></a>创建或标识组

构造特殊类型的类别注册表项，其`[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]``<group>`下是组的非本地化名称。

使用两个值填充注册表：

| 名称 | 类型 | 数据 | 描述 |
|--- | --- | --- | --- |
| 类别 | REG_SZ | GUID | 为识别类别而创建的 GUID |
| 程序包 | REG_SZ | GUID | 支持类别的 VSPackage 服务的 GUID |

注册表中指定的服务必须为相应的组提供 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>实现。

![实施IVsfontandColor集团](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304-a_FontAndColorGroup")<br />`IVsFontAndColorGroup` 的实现

### <a name="to-implement-ide-support"></a>实现 IDE 支持

实现[GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject)，它返回[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>或每个类别或 GUID 提供的 IDE 接口。

对于它支持的每个类别，VS包实现[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)接口的单独实例。

通过[IVsfontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)实现的方法必须为 IDE 提供：

- 类别中显示项的列表

- 显示项的可本地化名称

- 显示类别每个成员的信息

> [!NOTE]
> 每个类别必须至少包含一个显示项。

IDE 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>接口定义多个类别的联合。

其实现为 IDE 提供了：

- 组成给定组的类别列表

- 访问支持组内每个类别的[IVsFontAndColorDefaults 实例](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)

- 可本地化组名称

#### <a name="updating-the-ide"></a>更新 IDE

IDE 缓存有关字体和颜色设置的信息。 因此，在修改 IDE 字体和颜色配置后，最佳做法是确保缓存是最新的。

更新缓存通过[IvsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager)界面完成，可以全局执行，也可以仅对选定项目执行。

### <a name="handling-font-and-color-changes"></a>处理字体和颜色更改

为了正确支持 VSPackage 显示的文本着色，支持 VSPackage 的着色服务必须响应用户通过"字体和颜色"属性页所做的更改。

为此，VS 包必须：

- 通过实现[IVsfontAndColor 事件](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents)接口**来处理 IDE 生成的事件**。 在用户修改"字体和颜色"页后，IDE 调用适当的方法。 例如，如果选择了新字体，它将调用[OnFont"更改](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged)"方法。

  **或**

- **轮询 IDE 以进行更改**。 这可以通过系统实现的[IVsfontAndColor 存储](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)接口来完成。 尽管主要为了支持持久性，但[GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem)方法可以获取显示项目的字体和颜色信息。 有关字体和颜色设置的详细信息，请参阅 MSDN 文章[访问存储的字体和颜色设置](/visualstudio/extensibility/accessing-stored-font-and-color-settings?view=vs-2015)。

> [!NOTE]
> 为确保轮询结果正确，请使用[IVsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager)界面来确定是否需要缓存刷新和更新，然后调用[IVsFontAndColor 存储](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)接口的检索方法。

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>注册自定义字体和颜色类别，无需实现接口

以下代码示例演示如何在不实现接口的情况下注册自定义字体和颜色类别：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"

    "NameID"=dword:00000064
```

对于此代码示例：

- `"NameID"`• 包中本地化类别名称的资源 ID
- `"ToolWindowPackage"`• 包 GUID
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"`只是一个示例，实际值可以是实现器提供的新 GUID。

### <a name="set-the-font-and-color-property-category-guid"></a>设置字体和颜色属性类别 GUID

下面的代码示例演示了设置类别 GUID。

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
