---
title: Visual Studio 的字体和格式 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8634ab15a10b59fc21de390e0633d6d91793616d
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67891040"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Visual Studio 的字体和格式
## <a name="BKMK_TheEnvironmentFont"></a> 环境字体
 Visual Studio 中的所有字体必须针对自定义向用户都公开。 这主要是通过**字体和颜色**页面**工具 > 选项**对话框。 字体设置的三个主要类别是：

- **环境字体**-IDE （集成的开发环境），用于所有界面元素，包括对话框、 菜单、 工具窗口和文档窗口的主要字体。 默认情况下，环境字体将关联到显示为 9 pt Segoe UI 在当前版本的 Windows 系统字体。 所有界面元素都使用一种字体，可帮助确保整个 IDE 具有一致的字体的外观。

- **文本编辑器**-在页的图面上的代码和其他基于文本的编辑器可以自定义文本编辑器中的元素**工具 > 选项**。

- **特定集合**-提供用户自定义其界面元素的可能会公开特定于它们的设计的字体的设计器窗口图面自己设置页中**工具 > 选项**。

### <a name="editor-font-customization-and-resizing"></a>自定义编辑器字体和大小调整
 用户通常将放大或缩放大小和/或根据其喜好，独立于常规用户界面编辑器中文本的颜色。 环境字体中或作为一个编辑器/设计器的一部分可能会出现的元素上使用，所以务必要注意的预期的行为，这些字体分类之一发生更改时。

 创建时出现的 UI 元素在编辑器但不是属于*内容*，务必要使用环境字体并不将文本字体，以便在可预测的方式调整元素的大小。

1. 代码编辑器中的文本，与代码文本字体设置调整大小并响应编辑器文本的缩放级别。

2. 接口的所有其他元素应绑定到环境字体设置，并对在环境中的任何全局更改做出响应。 这包括 （但不限于）：

    - 上下文菜单中的文本

    - 文本在编辑器中使用修饰，如灯泡菜单文本，快速查找编辑器窗格中，并导航到窗格

    - 对话框中的文本标签等**在文件中查找**或**重构**

### <a name="accessing-the-environment-font"></a>访问环境字体
 在本机模式或 WinForms 代码中，可以通过调用方法访问环境字体`IUIHostLocale::GetDialogFont`查询从接口后`SID_SUIHostLocale`服务。

 有关 Windows Presentation Foundation (WPF) 中，从 shell 的派生自己的对话框窗口类`DialogWindow`类而不是 WPF 的`Window`类。

 在 XAML 中，代码如下所示：

```xaml
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>
```

代码隐藏：

```csharp
internal partial class WebConfigModificationWindow : DialogWindow
{
}
```

 (替换`Microsoft.VisualStudio.Shell.11.0`MPF dll 的当前版本。)

 若要显示对话框中，调用"`ShowModal()`"通过在类上`ShowDialog()`。 `ShowModal()` 在外壳程序中设置正确的模式状态，可确保对话框能够位于父窗口中，依次类推。

 代码如下所示:

```csharp
MyWindow window = new MyWindow();
window.ShowModal()
```

 `ShowModal` 返回一个布尔值？ （可以为 null 的布尔值） 与`DialogResult`，如果需要可使用它。 返回值为 true，如果对话框中，已关闭**确定**。

 如果你需要在其自身中显示一些 WPF UI，不是一个对话框，并位于`HwndSource`，如弹出窗口或 Win32/WinForms 父窗口的 WPF 子窗口，您将需要设置`FontFamily`和`FontSize`WPF 元素的根元素上。 (在 shell 上主窗口中，设置的属性，但将无法继承过去`HWND`)。 在 shell 提供了属性可以绑定到，此类资源：

```xaml
<Setter Property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter Property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />
```

### <a name="BKMK_Formatting"></a> 格式设置 （缩放/粗体） 参考
 某些对话框需要特定的文本为粗体或以外的环境字体的大小。 以前，大于环境字体的字体已编码为"`environment font +2`"或类似。 使用提供的代码片段将支持高 DPI 监视器，并确保在正确的大小和权重 （如 Light 或 Semilight） 始终显示的显示文本。

> [!NOTE]
> 应用格式设置之前，请确保您按照中的指南[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。 * *

 若要缩放环境字体，请设置样式的 TextBlock 或 Label 所示。 每个正确使用这些代码段将生成正确的字体，包括适当的尺寸和重量变体。

 其中"`vsui`"是对命名空间的引用`Microsoft.VisualStudio.Shell`:

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

#### <a name="375-environment-font--light"></a>375%环境字体 + Light

**显示为：** 34 pt Segoe UI Light

::: moniker range="vs-2017"

**用于：** （少见） 唯一品牌 UI，如启动页中

::: moniker-end

::: moniker range=">=vs-2019"

**用于：** （少见） 唯一经过品牌打造的用户界面

::: moniker-end

**程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);
```

**XAML:** 设置样式的 TextBlock 或 Label 所示。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>
```

#### <a name="310-environment-font--light"></a>310%环境字体 + Light
 **显示为：** 28 pt Segoe UI Light**用于：** 大型签名对话框标题、 主标题在报表中

 **程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);
```

 **XAML:** 设置样式的 TextBlock 或 Label 所示。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>
```

#### <a name="200-environment-font--semilight"></a>200%环境字体 + Semilight
 **显示为：** 18 磅 Segoe UI Semilight**用于：** 子标题、 小型和中型对话框中的标题

 **程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);
```

 **XAML:** 设置样式的 TextBlock 或 Label 所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>
```

#### <a name="155-environment-font"></a>155%环境字体
 **显示为：** 14 pt Segoe UI**用于：** 文档中的节标题好用户界面或报表

 **程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);
```

 **XAML:** 设置样式的 TextBlock 或 Label 所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>
```

#### <a name="133-environment-font"></a>133%环境字体
 **显示为：** 12 pt Segoe UI**用于：** 签名对话框和文档中的较小副标题好用户界面

 **程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);
```

 **XAML:** 设置样式的 TextBlock 或 Label 所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>
```

#### <a name="122-environment-font"></a>122%环境字体
 **显示为：** 11 pt Segoe UI**用于：** 部分签名对话框中的标题，排名靠前的节点在树视图中，垂直选项卡导航

 **程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);
```

 **XAML:** 设置样式的 TextBlock 或 Label 所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>
```

#### <a name="environment-font--bold"></a>环境字体 + 粗体
 **将显示为：** 粗体 9 pt Segoe UI**用于：** 标签和签名对话框、 报表和文档中的副标题好用户界面

 **程序代码中：** 其中`textBlock`是一个以前定义的文本块和`label`是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);
```

 **XAML:** 设置样式的 TextBlock 或 Label 所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>
```

### <a name="localizable-styles"></a>可本地化的样式
 在某些情况下，本地化人员将需要修改不同的区域设置，如粗体移除的东亚语言文本的字体样式。 若要使本地化的字体样式成为可能，这些样式必须是在.resx 文件中。 完成此操作并仍编辑 Visual Studio 窗体设计器中的字体样式的最好办法是在设计时显式设置字体样式。 尽管这将创建一个完整的字体对象并可能似乎违背了父字体的继承，但仅 FontStyle 属性用于将字体设置。

 解决方法是将挂钩对话框窗体的`FontChanged`事件。 在`FontChanged`事件，遍历所有控件，并检查其字体被设置。 如果设置，请将其更改为基于窗体的字体和控件的上一个字体样式的新字体。 此代码中的一个示例是：

```csharp
private void Form1_FontChanged(object sender, System.EventArgs e)
{
          SetFontStyles();
}

/// <summary>
/// SetFontStyles - This function will iterate all controls on a page
/// and recreate their font with the desired fontstyle.
/// It should be called in the OnFontChanged handler (and also in the constructor
/// in case the IUIService is not available so OnFontChange doesn't fire).
/// This way, when the VS shell font is given to us the controls that have
/// a different style for the font (bolded for example) will recreate their font
/// and use the VS shell font but with a style variation (bolded ...).
/// </summary>
protected void SetFontStyles()
{
     SetFontStyles(this, this, this.Font);
}

protected static void SetFontStyles(Control topControl, Control parent, Font referenceFont)
{
     foreach(Control c in parent.Controls)
     {
          if (c.Controls != null && c.Controls.Count > 0) {
               SetFontStyles(topControl, c, referenceFont);
          }
          if (c.Font != topControl.Font) {
               c.Font = new Font(referenceFont, c.Font.Style);
          }
     }
}
```

 使用此代码可保证，当更新窗体的字体时，控件的字体也将更新。 应调用此方法还会从窗体的构造函数，因为对话框中可能会失败，若要获取的实例`IUIService`和`FontChanged`会永远不会触发事件。 挂接`FontChanged`将允许动态拾取新的字体，即使对话框已打开的对话框。

### <a name="testing-the-environment-font"></a>测试环境字体
 若要确保你的 UI 使用环境字体，且会保留大小设置，打开**工具 > 选项 > 环境 > 字体和颜色**下选择"环境字体"和"显示其设置:"下拉列表菜单。

 ![在工具的字体和颜色设置&gt;选项对话框](../../extensibility/ux-guidelines/media/0201-a_optionsfonts.png "0201 a_OptionsFonts")<br />在工具的字体和颜色设置&gt;选项对话框

 设置为更非常不同于默认字体。 若要使它更加明显的 UI 不会更新，选择一种字体与具有衬线 （如"Times New Roman")，并设置非常大的大小。 然后，测试你的 UI，以确保它符合环境。 下面是使用许可证对话框中的一个示例：

 ![不遵从环境字体的 UI 文本的示例](../../extensibility/ux-guidelines/media/0201-b_wrongfontdialog.png "0201 b_WrongFontDialog")<br />不遵从环境字体的 UI 文本的示例

 "用户信息"和"产品信息"未在这种情况下，遵守字体。 在某些情况下，这可能是一个明确的设计选择，但如果未指定显式字体则红线规范的一部分，它可以是一个 bug。

 若要重置字体，请单击"使用默认值"下**工具 > 选项 > 环境 > 字体和颜色**。

## <a name="BKMK_TextStyle"></a> 文本样式
 文本样式引用字体大小、 宽度和大小写。 实现指南，请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

### <a name="text-casing"></a>文本大小写

#### <a name="all-caps"></a>全部大写
 请不要用于全部大写标题或 Visual Studio 中的标签。

#### <a name="all-lowercase"></a>全部小写
 不要使用全部为小写的标题或 Visual Studio 中的标签。

#### <a name="sentence-and-title-case"></a>句子和标题的用例
 词首字母大写或句子大小写，具体取决于这种情况，应使用 Visual Studio 中的文本。

|使用为词首字母大写：|使用句子大小写的：|
|-------------------------|----------------------------|
|对话框标题|标签|
|分组框|复选框|
|菜单项|单选按钮|
|上下文菜单项|列表框项|
|按钮|状态栏|
|表标签||
|列标题||
|工具提示||

##### <a name="title-case"></a>词首字母大写
 词首字母大写是大多数或所有词在短语内的第一个字母首字母大写的样式。 在 Visual Studio 中，词首字母大写用于多个项，包括：

- **工具提示。** 示例:"预览所选项目"

- **列标题。** 示例:"系统响应"

- **菜单项。** 示例:"全部保存"

  在使用词首字母大写，这些是何时首字母大写的单词以及何时将小写的准则：

|大写|注释和示例|
|---------------|---------------------------|
|所有名词||
|所有谓词|包括"Is"和其他形式的"若要为"|
|所有副词|包括"不是"和"时间"|
|所有的形容词|包括"This"和"That"|
|所有代词|包括所有格"Its"以及"它是"，如代词的缩写式"it"和谓词"is"|
|第一个和最后一个单词，而不考虑词类||
|介词属于谓词短语|"所有 Windows 出正在关闭"或者"关闭系统"|
|缩写词的所有字母|HTML、 XML、 URL、 IDE、 RGB|
|如果它是一个名词或专有形容词或字具有相等的权重，第二个 word 在一个组合词|预 Microsoft 软件的交叉引用，读/写访问权限，运行时|

|小写|示例|
|---------------|--------------|
|如果它是另一个语音部件或修改的第一个单词分词一个组合词中的第二个词|操作指南、 采用关闭|
|文章，除非其中一个是标题中的第一个单词|a、 an、 the|
|协调连词|并且，但是，也没有，或|
|介词的单词的谓词短语以外的四个或更少字母|到，到，作为为带，在最前面的|
|"收件人"无穷短语中使用时|"如何设置您的硬盘的格式"|

##### <a name="sentence-case"></a>句子首字母大写
 句子大小写标准大小写的方法是以写入中只有第一个句子的词而大写，以及任何专有名词和代词"I"。 一般情况下，句首大写容易为全球的客户，若要阅读，尤其是当内容将被转换一台计算机。 使用句子大小写的：

1. **状态栏消息。** 这些很简单，简单地说，并只提供状态信息。 示例:"正在加载项目文件"

2. **所有其他 UI 元素**，其中包括标签、 复选框、 单选按钮和列表框项。 示例:"列表中选择所有项"

### <a name="text-formatting"></a>文本格式设置
 由控制格式设置 Visual Studio 2013 中的默认文本[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。 此服务可帮助确保整个 IDE （集成的开发环境），具有一致的字体的外观，并且必须使用它能够保证你的用户提供一致的体验。

 使用 Visual Studio 字体服务的默认大小来自 Windows，将显示为 9 pt。

 您可以应用到环境字体格式。 本主题介绍如何以及在何处使用样式。 有关实现的信息，请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

#### <a name="bold-text"></a>粗体文本
 粗体文本在 Visual Studio 中尽量少使用，并应将其保留为：

- 在向导中的问题标签

- 指定活动项目在解决方案资源管理器

- 重写属性工具窗口中的值

- Visual Basic 编辑器下拉列表中的特定事件

- 服务器生成 web pages 文档大纲中的内容

- 在复杂的对话框或设计器用户界面的部分标头

#### <a name="italics"></a>斜体
 Visual Studio 不使用斜体或粗体斜体文本。

#### <a name="color"></a>颜色

- 蓝色保留的超链接 （导航和命令），并且永远不会用于方向。

- 可以针对这些目的着色更大的标题 （环境字体 x 155%或更高版本）：

  - 若要提供与 Visual Studio UI 的签名的视觉效果

  - 呼吁人们关注的特定区域

  - 提供基于标准的暗灰色/黑环境的文本颜色的缓解办法

- 在标题中的颜色应利用现有 Visual Studio 品牌颜色的颜色，主要是主要的紫色，#FF68217A。

- 在标题中使用颜色，则必须遵守[Windows 颜色准则](/windows/desktop/uxguide/vis-color)，包括对比率和其他辅助功能注意事项。

### <a name="font-size"></a>字体大小
 Visual Studio 用户界面设计功能具有更多的空白空间较浅外观。 在可能的情况下，chrome 和标题栏已减少或删除。 在 Visual Studio 中的要求的信息密度时，版式仍是重要的是，侧重于更加开放的行距和字体大小和权重的一种变体。

 下表包括设计的详细信息和使用 Visual Studio 中的显示字体的直观示例。 一些不同的显示字体具有的大小和权重，如 Semilight 或 Light，编码到它们的外观。

 中找不到所有显示字体的实现代码段[格式设置 （缩放/粗体） 引用](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)。

#### <a name="375-environment-font--light"></a>375%环境字体 + Light

|||
|-|-|
|**用法：** 极少数。 只有唯一的经过品牌打造的 UI。<br /><br /> **执行操作：**<br /><br /> -使用句子大小写<br />-始终使用轻量<br /><br /> **不要：**<br /><br /> 使用 ui 以外签名如起始页的 UI<br />-粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用工具窗口|**显示为：** 34 pt Segoe UI Light<br /><br /> **可视示例：**<br /><br /> *当前未使用。可以在 Visual Studio 2017 起始页中使用。*|

#### <a name="310-environment-font--light"></a>310%环境字体 + Light

::: moniker range="vs-2017"

|||
|-|-|
|**用法：**<br /><br /> 签名对话框中的较大标题<br />-主报表标题<br /><br /> **执行操作：**<br /><br /> -使用句子大小写<br />-始终使用轻量<br /><br /> **不要：**<br /><br /> 使用 ui 以外签名如起始页的 UI<br />-粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用工具窗口|**显示为：** 28 pt Segoe UI Light<br /><br /> **可视示例：**<br /><br /> ![310%环境字体的示例&#43;Light 标题](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202 a_EF310")|

::: moniker-end

::: moniker range=">=vs-2019"

|||
|-|-|
|**用法：**<br /><br /> 签名对话框中的较大标题<br />-主报表标题<br /><br /> **执行操作：**<br /><br /> -使用句子大小写<br />-始终使用轻量<br /><br /> **不要：**<br /><br /> 使用 ui 以外签名 UI<br />-粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用工具窗口|**显示为：** 28 pt Segoe UI Light<br /><br /> **可视示例：**<br /><br /> ![310%环境字体的示例&#43;Light 标题](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202 a_EF310")|

::: moniker-end

#### <a name="200-environment-font--semilight"></a>200%环境字体 + Semilight

|||
|-|-|
|**用法：**<br /><br /> -副标题<br />的小型和中型对话框中标题<br /><br /> **执行操作：**<br /><br /> -使用句子大小写<br />-始终使用 Semilight 权重<br /><br /> **不要：**<br /><br /> -粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用工具窗口|**显示为：** 18 磅 Segoe UI Semillight<br /><br /> **可视示例：**<br /><br /> ![200%环境字体的示例&#43;Semilight](../../extensibility/ux-guidelines/media/0202-b_ef200.png "0202 b_EF200")|

#### <a name="155-environment-font"></a>155%环境字体

|||
|-|-|
|**用法：**<br /><br /> 的在文档中节标题好用户界面<br />-报表<br /><br /> **执行操作：** 使用句子大小写<br /><br /> **不要：**<br /><br /> -粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用标准 Visual Studio 控件中<br />-使用工具窗口|**显示为：** 14 pt Segoe UI<br /><br /> **可视示例：**<br /><br /> ![155%环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-c_ef155.png "0202 c_EF155")|

#### <a name="133-environment-font"></a>133%环境字体

|||
|-|-|
|**用法：**<br /><br /> 的签名对话框中较小副标题<br />的在文档中较小副标题好用户界面<br /><br /> **执行操作：** 使用句子大小写<br /><br /> **不要：**<br /><br /> -粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用标准 Visual Studio 控件中<br />-使用工具窗口|**显示为：** 12 磅 Segoe UI<br /><br /> **可视示例：**<br /><br /> ![133%环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-d_ef133.png "0202 d_EF133")|

#### <a name="122-environment-font"></a>122%环境字体

|||
|-|-|
|**用法：**<br /><br /> 的签名对话框中节标题<br />的在树视图中顶级节点<br />的垂直选项卡导航<br /><br /> **执行操作：** 使用句子大小写<br /><br /> **不要：**<br /><br /> -粗体、 斜体或粗体斜体<br />-用于正文文本<br />-使用标准 Visual Studio 控件中<br />-使用工具窗口|**显示为：** 11 pt Segoe UI<br /><br /> **可视示例：**<br /><br /> ![122%环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-e_ef122.png "0202 e_EF122")|

#### <a name="environment-font--bold"></a>环境字体 + 粗体

|||
|-|-|
|**用法：**<br /><br /> -标签和签名对话框中的副标题<br />-标签和在报表中的副标题<br />-标签和文档中的副标题 UI<br /><br /> **执行操作：**<br /><br /> -使用句子大小写<br />-使用粗体粗细<br /><br /> **不要：**<br /><br /> -倾斜或加粗倾斜<br />-用于正文文本<br />-使用标准 Visual Studio 控件中<br />-使用工具窗口|**将显示为：** 粗体 9 pt Segoe UI<br /><br /> **可视示例：**<br /><br /> ![环境字体的示例&#43;加粗标题](../../extensibility/ux-guidelines/media/0202-f_efb.png "0202 f_EFB")|

#### <a name="environment-font"></a>环境字体

|||
|-|-|
|**用法：** 所有其他文本<br /><br /> **执行操作：** 使用句子大小写<br /><br /> **不要：** 斜体或粗体斜体|**显示为：** 9 pt Segoe UI<br /><br /> **可视示例：**<br /><br /> ![环境字体的示例](../../extensibility/ux-guidelines/media/0202-g_ef.png "0202 g_EF")|

### <a name="padding-and-spacing"></a>边距和间距
 标题需要它们来为他们提供适当的重点周围的空间。 此空间各不相同，具体取决于点大小和其他什么是附近的标题，例如水平标尺或环境字体中的文本行。

- 本身为标题的理想之选填充应为 90%的资金字符高度空间。 例如，28 pt Segoe UI Light 标题有 26 pt 帽高度和填充应大约为，23 pt 或大约 31 像素。

- 标题周围的最小空间应为 50%的资金字符高度。 当标题由规则或其他紧凑调整元素一起出现时，可能使用较少的空间。

- 加粗环境字体文本应遵循默认行距高度和填充。

## <a name="see-also"></a>请参阅

- [MSDN:字体 (Windows)](/windows/desktop/uxguide/vis-fonts)
- [MSDN:用户界面文本 (Windows)](/windows/desktop/uxguide/text-ui)
