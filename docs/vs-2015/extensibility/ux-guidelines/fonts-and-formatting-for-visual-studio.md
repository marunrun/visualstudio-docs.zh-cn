---
title: 字体和格式设置
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3e88f314ccdf2b91215fdfe579741591c7eb724d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544204"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Visual Studio 的字体和格式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a>环境字体
 Visual Studio 中的所有字体都必须向用户公开，以便进行自定义。 这主要通过 "**工具 > 选项**" 对话框中的 "**字体和颜色**" 页完成。 字体设置的三种主要类别是：

- **环境字体**-IDE （集成开发环境）的主要字体，适用于所有界面元素，包括对话框、菜单、工具窗口和文档窗口。 默认情况下，环境字体与当前版本的 Windows 中显示为 9 pt Segoe UI 的系统字体相关联。 为所有接口元素使用一种字体，有助于确保整个 IDE 中的字体外观一致。

- **文本编辑器**-可以在 "**工具" > 选项**的 "文本编辑器" 页中自定义在代码和其他基于文本的编辑器中进行自定义的元素。

- **特定集合**-提供其界面元素的用户自定义的设计器窗口可能会在**工具 > 选项**的 "设置" 页中公开其设计图面的特定字体。

### <a name="editor-font-customization-and-resizing"></a>编辑器字体自定义和调整大小
 用户经常会根据自己的偏好来扩大或缩小编辑器中文本的大小和/或颜色，而与常规用户界面无关。 由于环境字体用于可能出现在编辑器/设计器中或作为编辑器/设计器一部分的元素，因此，在更改其中一种字体分类时，请务必记下预期的行为。

 当创建显示在编辑器中但不包含在*内容*中的 UI 元素时，必须使用环境字体，而不是文本字体，以便元素以可预测的方式调整大小。

1. 对于编辑器中的代码文本，用代码文本字体设置调整大小并响应编辑器文本的缩放级别。

2. 接口的所有其他元素应绑定到环境字体设置，并对环境中的任何全局更改做出响应。 这包括（但不限于）：

    - 上下文菜单中的文本

    - 编辑器修饰中的文本，例如灯泡菜单文本、快速查找编辑器窗格，并导航到窗格

    - 在对话框中添加标签文本，如 "在文件中查找" 或 "重构"

### <a name="accessing-the-environment-font"></a>访问环境字体
 在本机代码或 WinForms 代码中，从 SID_SUIHostLocale 服务查询接口后，可以通过调用方法**IUIHostLocale：： GetDialogFont**来访问环境字体。

 对于 Windows Presentation Foundation （WPF），从 shell 的**DialogWindow**类派生对话框窗口类，而不是 WPF 的**窗口**类。

 在 XAML 中，代码如下所示：

```
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>

code behind:

internal partial class WebConfigModificationWindow : DialogWindow
{
}

```

 （替换 `Microsoft.VisualStudio.Shell.11.0` 为当前版本的 MPF dll。）

 若要显示该对话框，请对**ShowDialog （）** 调用类上的 "**ShowModal （）**"。 **ShowModal （）** 在 shell 中设置正确的模式状态，确保该对话框在父窗口中居中，依此类推。

 代码如下所示:

```
MyWindow window = new MyWindow();
window.ShowModal()

```

 **ShowModal**返回布尔值？ （可为 null 的布尔值）与**DialogResult**，可在需要时使用。 如果对话框已**关闭，则**返回值为 true。

 如果需要显示不是对话框并在其自己的**HwndSource**中承载的 wpf UI （如弹出窗口或 Win32/WinForms 父窗口窗口的 WPF 子窗口），则需要在 WPF 元素的根元素上设置**FontFamily**和**FontSize** 。 （Shell 在主窗口上设置属性，但不会继承 HWND）。 Shell 提供属性可以绑定到的资源，如下所示：

```
<Setter property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />

```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a>格式设置（缩放/粗体）参考
 某些对话框要求使用特定文本作为粗体或除环境字体之外的其他大小。 以前，大于环境字体的字体编码为 "环境字体 + 2" 或类似。 使用提供的代码段将支持高 DPI 监视器，并确保显示文本始终以正确的大小和权重显示（如光源或 Semilight）。

> **注意：在应用格式设置之前，请确保遵循[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)中的指南。**

 若要缩放环境字体，请设置 TextBlock 或标签的样式，如所示。 正确使用的每个代码片段都将生成正确的字体，包括适当的大小和权重变体。

 其中，"vsui" 是对命名空间 VisualStudio 的引用：

```
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"

```

#### <a name="375-environment-font--light"></a>375% 环境字体 + 浅色
 **显示为：** 34 Pt Segoe UI 浅色

 用于 **：** （罕见）唯一品牌 UI，如起始页中的

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>

```

#### <a name="310-environment-font--light"></a>310% 环境字体 + 浅色
 **显示为：** 28 Pt Segoe UI 浅色

 **用途：** 大型签名对话框标题，报表中的主标题

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>

```

#### <a name="200-environment-font--semilight"></a>200% 环境字体 + Semilight
 **显示为：** 18 Pt Segoe UI Semilight

 用于：副标题，小型和中型对话框中**的**标题

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>

```

#### <a name="155-environment-font"></a>155% 环境字体
 **显示为：** 14 pt Segoe UI

 **使用 for：** 文档好的 UI 或报表中的节标题

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>

```

#### <a name="133-environment-font"></a>133% 环境字体
 **显示为：** 12 pt Segoe UI

 用于：签名对话框中较小**的**子标题和文档好 UI

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>

```

#### <a name="122-environment-font"></a>122% 环境字体
 **显示为：** 11 pt Segoe UI

 用于：签名对话框中的节标题，树视图中**的**顶级节点，垂直选项卡导航

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>

```

#### <a name="environment-font--bold"></a>环境字体 + 粗体
 **显示为：** 加粗 9 pt Segoe UI

 **使用 for：** 签名对话框、报表和文档用户界面中的标签和副标题

 **过程代码：** 其中，"textBlock" 是以前定义的 TextBlock，"label" 是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);

```

 **XAML：** 设置 TextBlock 或标签的样式，如所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>

```

### <a name="localizable-styles"></a>可本地化样式
 在某些情况下，本地化人员需要针对不同的区域设置修改字体样式，如从中文语言的文本中删除粗体。 为了能够实现字体样式的本地化，这些样式必须在 .resx 文件中。 实现此目的并在 Visual Studio 窗体设计器中编辑字体样式的最佳方式是在设计时显式设置字体样式。 尽管这会创建一个完整的字体对象，并可能看起来中断了父字体的继承，但只有 FontStyle 属性用于设置字体。

 解决方案是挂钩对话框窗体的**FontChanged**事件。 在**FontChanged**事件中，遍历所有控件并检查其字体是否已设置。 如果已设置，则将其更改为基于窗体字体和控件上一个字体样式的新字体。 代码中的示例如下：

```
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

 使用此代码可保证在更新窗体的字体时，控件的字体也会更新。 还应从窗体的构造函数中调用此方法，因为该对话框可能无法获取**IUIService**的实例，并且**FontChanged**事件永远不会激发。 挂钩**FontChanged**将允许对话框动态选取新字体，即使此对话框已打开。

### <a name="testing-the-environment-font"></a>测试环境字体
 若要确保 UI 使用环境字体并遵守大小设置，请打开 "工具" **> 选项 > 环境 > 字体和颜色**，然后在 "显示其设置：" 下拉菜单下选择 "环境字体"。

 ![工具 &#62; 选项 "对话框中的" 字体和颜色 "页](../../extensibility/ux-guidelines/media/0201-a-optionsfonts.png "0201-a_OptionsFonts")

 **"工具" > 选项 "对话框中的字体和颜色设置**

 将字体设置为与默认值不同的内容。 若要使其很明显不会更新的 UI，请选择带衬线的字体（如 "New Roman"）并设置一个非常大的大小。 然后测试 UI，以确保其符合环境。 下面是使用 "许可证" 对话框的示例：

 ![不使用环境字体的对话框的示例](../../extensibility/ux-guidelines/media/0201-b-wrongfontdialog.png "0201-b_WrongFontDialog")

 **不遵守环境字体的 UI 文本的示例**

 在这种情况下，"用户信息" 和 "产品信息" 不遵从字体。 在某些情况下，这可能是一种显式的设计选择，但是如果未将显式字体指定为红线规范的一部分，则它可能是一个 bug。

 若要重置字体，请在 "工具" **> 选项 "> 环境 > 字体和颜色**" 下，单击 "使用默认值"。

## <a name="text-style"></a><a name="BKMK_TextStyle"></a>文本样式
 文本样式指的是字体大小、粗细和大小写。 有关实现指南，请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

### <a name="text-casing"></a>文本大小写

#### <a name="all-caps"></a>全部大写
 不要在 Visual Studio 中将所有标题或标签全部使用。

#### <a name="all-lowercase"></a>全部小写
 对于 Visual Studio 中的标题或标签，不要使用全部小写形式。

#### <a name="sentence-and-title-case"></a>句子和词首大写
 Visual Studio 中的文本应使用词首大写或句子大小写，具体取决于具体情况。

|使用词首字母大写：|使用句子 case：|
|-------------------------|----------------------------|
|对话框标题|标签|
|分组框|复选框|
|菜单项|单选按钮|
|上下文菜单项|列表框项|
|按钮|状态栏|
|表标签||
|列标题||
|工具提示||

##### <a name="title-case"></a>标题格式
 "标题大小写" 是指短语中大部分或全部单词的首字母大写的样式。 在 Visual Studio 中，"标题大小写" 用于多个项目，包括：

- **Tooltip.** 示例： "预览选定项"

- **列标头。** 示例： "系统响应"

- **菜单项。** 示例： "全部保存"

  使用词首字母大写时，以下是在何时将单词和何时变为小写的准则：

|大写|注释和示例|
|---------------|---------------------------|
|所有名词||
|所有谓词|包括 "Is" 和其他窗体 "是"|
|所有副词|包括 "大于" 和 "When"|
|所有形容词|包括 "This" 和 "This"|
|所有代词|其中包括所有格 "其" 以及 "It"、"缩写式" 和 "is" 这一代词|
|第一个和最后一个单词，与语音的部分无关||
|属于动词短语的介词|"关闭所有窗口" 或 "关闭系统"|
|首字母缩写词的所有字母|HTML、XML、URL、IDE、RGB|
|组合词中的第二个单词（如果它是名词或正确的形容词），或者单词的权重相等|交叉引用，Microsoft Microsoft 软件，读/写访问，运行时|

|小写|示例|
|---------------|--------------|
|组合词中的第二个单词（如果它是词性的另一个部分，或修改第一个单词的分词）|操作说明、卸载|
|文章，除非标题中的第一个词是|a、an、the|
|坐标连词|and、or、and 或|
|动词短语之外的字母包含四个或更少字符的介词|into，放入，在|
|无穷短语中使用时的 "To"|"如何格式化硬盘"|

##### <a name="sentence-case"></a>句子大小写
 句子 case 是用于写入的标准大写方法，其中只有句子的第一个词是大写的，以及任何正确名词和代词 "I"。 一般情况下，对于全球受众来说，句子案例更容易阅读，尤其是在计算机翻译内容时。 使用句子 case：

1. **状态栏消息。** 它们简单、简短，只提供状态信息。 示例： "正在加载项目文件"

2. **所有其他 UI 元素**，包括标签、复选框、单选按钮和列表框项。 示例： "选择列表中的所有项目"

### <a name="text-formatting"></a>文本格式
 Visual Studio 2013 中的默认文本格式由[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)控制。 此服务可帮助确保整个 IDE （集成开发环境）中的字体外观一致，并且你必须使用它来保证用户的一致体验。

 Visual Studio 字体服务使用的默认大小来自 Windows，并显示为 9 pt。

 可以将格式设置应用于环境字体。 本主题介绍使用样式的方式和位置。 有关实现的信息，请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

#### <a name="bold-text"></a>粗体文本
 在 Visual Studio 中，粗体文本会慎用，应保留为：

- 向导中的试题标签

- 指定活动项目解决方案资源管理器

- "属性" 工具窗口中的重写值

- Visual Basic 编辑器下拉列表中的某些事件

- 网页文档大纲中服务器生成的内容

- 复杂对话框或设计器 UI 中的节标头

#### <a name="italics"></a>斜体
 Visual Studio 不使用斜体或粗体斜体文本。

#### <a name="color"></a>颜色

- 为超链接（导航和命令）保留蓝色，不应用于方向。

- 更大的标题（环境字体 x 155% 或更高）可用于以下目的：

  - 向 visual Studio UI 签名提供视觉吸引力

  - 若要注意特定区域

  - 从标准暗灰色/黑色环境文本颜色中提供止裂槽

- 标题中的颜色应利用现有的 Visual Studio 品牌颜色，主要为紫色 #FF68217A。

- 在标题中使用颜色时，必须遵守[Windows 颜色准则](https://msdn.microsoft.com/library/dn742482.aspx)，包括对比度和其他辅助功能注意事项。

### <a name="font-size"></a>字体大小
 Visual Studio UI 设计功能具有更好的空白外观，具有更多空白。 如果可能，则会减少或删除 chrome 和 title 栏。 尽管 Visual Studio 中的信息密度是必需的，但版式仍非常重要，重点强调更开放的行距和字体大小和粗细的变体。

 下表包含 Visual Studio 中使用的显示字体的设计详细信息和视觉对象示例。 某些显示字体变体具有大小和权重，如 "Semilight" 或 "浅色"，编码为其外观。

 所有显示字体的实现代码片段可以在 "[格式设置（缩放/粗体）参考](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)" 中找到。

#### <a name="375-environment-font--light"></a>375% 环境字体 + 浅色

|使用情况|外观|
|-|-|
|**用法：** 极少数. 仅限唯一品牌的 UI。<br /><br /> **看**<br /><br /> -Use 句型 case<br />-始终使用轻量<br /><br /> **请勿：**<br /><br /> -用于除签名 UI （如起始页）以外的 UI<br />-粗体、斜体或粗体斜体<br />-用于正文文本<br />-在工具窗口中使用|**显示为：** 34 Pt Segoe UI 浅色<br /><br /> **Visual 示例：**<br /><br /> *当前未使用。可在起始页中使用。*|

#### <a name="310-environment-font--light"></a>310% 环境字体 + 浅色

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -签名对话框中的更大标题<br />-主报表标题<br /><br /> **看**<br /><br /> -Use 句型 case<br />-始终使用轻量<br /><br /> **请勿：**<br /><br /> -用于除签名 UI （如起始页）以外的 UI<br />-粗体、斜体或粗体斜体<br />-用于正文文本<br />-在工具窗口中使用|**显示为：** 28 Pt Segoe UI 浅色<br /><br /> **Visual 示例：**<br /><br /> ![310% 环境字体 &#43; 浅色标题的示例](../../extensibility/ux-guidelines/media/0202-a-ef310.png "0202-a_EF310")|

#### <a name="200-environment-font--semilight"></a>200% 环境字体 + Semilight

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -副标题<br />-小型和中型对话框中的标题<br /><br /> **看**<br /><br /> -Use 句型 case<br />-始终使用 Semilight 权重<br /><br /> **请勿：**<br /><br /> -粗体、斜体或粗体斜体<br />-用于正文文本<br />-在工具窗口中使用|**显示为：** 18 Pt Segoe UI Semillight<br /><br /> **Visual 示例：**<br /><br /> ![&#43; Semilight 的200% 环境字体的示例](../../extensibility/ux-guidelines/media/0202-b-ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>155% 环境字体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -文档好 UI 中的节标题<br />-报表<br /><br /> **Do：** 使用句子 case<br /><br /> **请勿：**<br /><br /> -粗体、斜体或粗体斜体<br />-用于正文文本<br />-用于标准 Visual Studio 控件<br />-在工具窗口中使用|**显示为：** 14 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![155% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-c-ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>133% 环境字体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -签名对话框中较小的子标题<br />-文档良好 UI 中的小标题<br /><br /> **Do：** 使用句子 case<br /><br /> **请勿：**<br /><br /> -粗体、斜体或粗体斜体<br />-用于正文文本<br />-用于标准 Visual Studio 控件<br />-在工具窗口中使用|**显示为：** 12 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![133% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-d-ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>122% 环境字体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -签名对话框中的节标题<br />-树视图中的顶级节点<br />-垂直选项卡导航<br /><br /> **Do：** 使用句子 case<br /><br /> **请勿：**<br /><br /> -粗体、斜体或粗体斜体<br />-用于正文文本<br />-用于标准 Visual Studio 控件<br />-在工具窗口中使用|**显示为：** 11 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![122% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-e-ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>环境字体 + 粗体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -签名对话框中的标签和副标题<br />-报表中的标签和副标题<br />-文档好 UI 中的标签和副标题<br /><br /> **看**<br /><br /> -Use 句型 case<br />-使用粗体<br /><br /> **请勿：**<br /><br /> -斜体或斜体<br />-用于正文文本<br />-用于标准 Visual Studio 控件<br />-在工具窗口中使用|**显示为：** 加粗 9 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![环境字体 &#43; 粗体标题的示例](../../extensibility/ux-guidelines/media/0202-f-efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>环境字体

|使用情况|外观|
|-|-|
|**用法：** 所有其他文本<br /><br /> **Do：** 使用句子 case<br /><br /> **请勿：** 斜体或斜体|**显示为：** 9 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![环境字体的示例](../../extensibility/ux-guidelines/media/0202-g-ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>填充和间距
 标题需要围绕它们的空间来为他们指定适当的强调。 此空间因点大小而异，其他在标题附近，例如水平标尺或环境字体中的文本行。

- 标题的理想填充方式应为大写字符高度空间的90%。 例如，一个 28 pt Segoe UI 光源标题的高度为26磅，并且填充长度应约为23磅，或者约31像素。

- 标题周围的最小空间应为大写字符高度的50%。 当标题附带一个规则或其他严格的元素时，可以使用较少的空间。

- 粗体环境字体文本应遵循默认行高度间距和填充。

## <a name="see-also"></a>另请参阅
 [Msdn： Fonts （windows）](https://msdn.microsoft.com/library/windows/desktop/dn742483\(v=vs.85\).aspx) [Msdn：用户界面文本（windows）](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)
