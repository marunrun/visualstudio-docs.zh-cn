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
ms.openlocfilehash: ede8844b34473e1c900bd6af040cac99ceee1514
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301319"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Visual Studio 的字体和格式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a>环境字体
 Visual Studio 中的所有字体都必须向用户公开以进行自定义。 这主要通过"**工具>选项**"对话框中的"**字体和颜色**"页完成。 字体设置的三个主要类别是：

- **环境字体**— IDE（集成开发环境）的主字体，用于所有接口元素，包括对话框、菜单、工具窗口和文档窗口。 默认情况下，环境字体绑定到当前版本的 Windows 中显示为 9 pt Segoe UI 的系统字体。 对所有接口元素使用一种字体有助于确保在整个 IDE 中保持一致的字体外观。

- **文本编辑器**– 在 **"工具>选项**"中的文本编辑器页面中，可以在代码和其他基于文本的编辑器中显示的元素进行自定义。

- **特定集合**– 提供用户自定义其界面元素的设计器窗口可能会在**工具>选项**）中自己的设置页中公开特定于其设计图面的字体。

### <a name="editor-font-customization-and-resizing"></a>编辑器字体自定义和调整大小
 用户通常会根据用户偏好放大或缩放编辑器中文本的大小和/或颜色，而与一般用户界面无关。 由于环境字体用于可能出现在编辑器/设计器内部或作为编辑器/设计器的一部分的元素，因此在更改这些字体分类之一时注意预期行为非常重要。

 创建出现在编辑器中但不是*内容*一部分的 UI 元素时，使用环境字体而不是文本字体非常重要，以便元素以可预测的方式调整大小。

1. 对于编辑器中的代码文本，请使用代码文本字体设置调整大小，并响应编辑器文本的缩放级别。

2. 接口的所有其他元素应绑定到环境字体设置，并响应环境中的任何全局更改。 这包括（但不限于）：

    - 上下文菜单中的文本

    - 编辑器修饰中的文本，如灯泡菜单文本、快速查找编辑器窗格以及导航到窗格

    - 在对话框中标注文本，如"在文件中查找"或"重构"

### <a name="accessing-the-environment-font"></a>访问环境字体
 在本机或 WinForms 代码中，可以通过调用方法**IUIHostLocale：：getDialogFont**在从SID_SUIHostLocale服务查询界面来访问环境字体。

 对于 Windows 演示文稿基础 （WPF），从 shell 的**对话框窗口**类而不是 WPF**的窗口类**派生对话框窗口类。

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

 （替换为`Microsoft.VisualStudio.Shell.11.0`MPF dll 的当前版本。

 要显示对话框，请通过**ShowDialog（）** 在类上调用"**显示模式（）"。** **ShowModal（）** 在 shell 中设置正确的模态状态，确保对话框在父窗口中居中，等等。

 代码如下所示:

```
MyWindow window = new MyWindow();
window.ShowModal()

```

 **显示模态**返回布尔？ （空布尔）与**对话框Result**，如果需要，可以使用。 如果对话框以 **"确定"** 关闭，则返回值为 true。

 如果需要显示一些不是对话框的 WPF UI，并且托管在其自己的**HwndSource**中，例如弹出窗口或 Win32/WinForms 父窗口的 WPF 子窗口，则需要在 WPF 元素的根元素上设置**FontFamily**和**FontSize。** （shell 在主窗口中设置属性，但不会继承到 HWND 之后）。 shell 提供可以绑定属性的资源，如下所示：

```
<Setter property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />

```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a>格式（缩放/粗体）引用
 某些对话框要求特定文本为粗体或环境字体以外的大小。 以前，大于环境字体的字体被编码为"环境字体 +2"或类似。 使用提供的代码段将支持高 DPI 监视器，并确保显示文本始终以正确的大小和重量显示（如"光"或"半光"）。

> **注意：在应用格式之前，请确保遵循[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)中的指南。**

 要缩放环境字体，可以按指示设置 TextBlock 或 Label 的样式。 正确使用的每个代码段都将生成正确的字体，包括适当的大小和重量变化。

 其中"vsui"是对名称空间 Microsoft 的引用。

```
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"

```

#### <a name="375-environment-font--light"></a>375% 环境字体 + 浅色
 **显示为：** 34 pt 塞戈 UI 灯

 **用于：（** 罕见）唯一品牌 UI，如"起始页"

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>

```

#### <a name="310-environment-font--light"></a>310% 环境字体 + 浅色
 **显示为：** 28 pt 塞戈 UI 灯

 **用于：** 大型签名对话框标题，报表中的主标题

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>

```

#### <a name="200-environment-font--semilight"></a>200% 环境字体 + 半光
 **显示为：** 18 pt 塞戈 UI 半光

 **用于：** 副标题，中小型对话框中的标题

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>

```

#### <a name="155-environment-font"></a>155% 环境字体
 **显示为：** 14 pt 塞戈 UI

 **用于：** 文档井 UI 或报表中的节标题

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>

```

#### <a name="133-environment-font"></a>133% 环境字体
 **显示为：** 12 pt 塞戈 UI

 **用于：** 签名对话框中较小的副标题和文档 ui

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>

```

#### <a name="122-environment-font"></a>122% 环境字体
 **显示为：** 11 pt Segoe UI

 **用于：** 签名对话框中的节标题、树视图中的顶部节点、垂直选项卡导航

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>

```

#### <a name="environment-font--bold"></a>环境字体 = 粗体
 **显示为：** 粗体 9 pt Segoe UI

 **用于：** 签名对话框、报表和文档中的标记和子头 UI

 **程序代码：** 其中"文本块"是以前定义的 TextBlock，"标签"是以前定义的标签。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);

```

 **XAML：** 设置文本块或标签的样式，如图所示。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>

```

### <a name="localizable-styles"></a>可本地化样式
 在某些情况下，本地化人员需要修改不同区域设置的字体样式，例如从东亚语言的文本中删除粗体。 为了使字体样式的本地化成为可能，这些样式必须存在于 .resx 文件中。 在 Visual Studio 窗体设计器中实现此目的并仍在编辑字体样式的最佳方法是在设计时显式设置字体样式。 尽管这将创建一个完整的字体对象，并且似乎可能会破坏父字体的继承，但只有 FontStyle 属性用于设置字体。

 解决方案是挂接对话框表单的**Font"更改**"事件。 在**Font"更改"** 事件中，遍历所有控件并检查其字体是否已设置。 如果已设置，则根据窗体的字体和控件以前的字体样式将其更改为新字体。 代码中这方面的一个示例是：

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

 使用此代码可确保在更新窗体的字体时，控件的字体也将更新。 还应从窗体的构造函数调用此方法，因为对话框可能无法获取**IUIService**的实例，**而 FontGet 事件**永远不会触发。 钩**字体更改**将允许对话框动态选取新字体，即使对话框已打开也是如此。

### <a name="testing-the-environment-font"></a>测试环境字体
 为确保 UI 使用环境字体并尊重大小设置，请打开 **"工具>选项>环境>字体和颜色**"，并在"显示设置"下拉菜单下选择"环境字体"。

 !["工具&#62;选项"对话框中的字体和颜色页面](../../extensibility/ux-guidelines/media/0201-a-optionsfonts.png "0201-a_OptionsFonts")

 **"工具>选项"对话框中的字体和颜色设置**

 将字体设置为与默认值非常不同的内容。 为了明显哪个 UI 不更新，请选择带有衬线（如"时代新罗马"）的字体，并设置非常大的大小。 然后测试 UI 以确保它尊重环境。 下面是使用许可证对话框的示例：

 ![不使用环境字体的对话框的示例](../../extensibility/ux-guidelines/media/0201-b-wrongfontdialog.png "0201-b_WrongFontDialog")

 **不尊重环境字体的 UI 文本示例**

 在这种情况下，"用户信息"和"产品信息"不尊重字体。 在某些情况下，这可能是一个明确的设计选择，但如果显式字体未指定为红线规范的一部分，则可能是一个错误。

 要重置字体，请单击 **"工具>选项 >>字体和颜色"** 下"使用默认值"。

## <a name="text-style"></a><a name="BKMK_TextStyle"></a>文本样式
 文本样式是指字体大小、粗细和大小写。 有关实现指南，请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

### <a name="text-casing"></a>文本大小写

#### <a name="all-caps"></a>全部大写
 请勿在视觉工作室中对标题或标签使用所有大写字母。

#### <a name="all-lowercase"></a>所有小写
 请勿对视觉工作室中的标题或标签使用所有小写。

#### <a name="sentence-and-title-case"></a>句子和标题案例
 Visual Studio 中的文本应使用标题案例或句子案例，具体取决于具体情况。

|使用标题案例：|使用句子案例：|
|-------------------------|----------------------------|
|对话框标题|标签|
|组框|复选框|
|菜单项|单选按钮|
|上下文菜单项|列表框项目|
|按钮|状态栏|
|表标签||
|列标题||
|工具提示||

##### <a name="title-case"></a>标题格式
 标题大小写是一种样式，其中短语中大多数或所有单词的第一个字母大写。 在 Visual Studio 中，标题案例用于许多项目，包括：

- **提示。** 示例："预览所选项目"

- **列标题。** 示例："系统响应"

- **菜单项。** 示例："全部保存"

  使用标题大小写时，以下是何时对单词进行大写以及何时保留小写字母的准则：

|大写|评论和示例|
|---------------|---------------------------|
|所有名词||
|所有谓词|包括"是"和其他形式的"要"|
|所有副词|包括"Than"和"何时"|
|所有形容词|包括"这个"和"那个"|
|所有代词|包括占有性的"它"和"它是"，代词"它"和动词"是"的收缩|
|第一个单词和最后一个单词，无论演讲的哪个部分||
|作为动词短语一部分的介词|"关闭所有窗口"或"关闭系统"|
|首字母缩略词的所有字母|HTML、 XML、 URL、 IDE、 RGB|
|复合词中的第二个单词，如果是名词或适当的形容词，或者单词具有相等的权重|交叉引用，微软前软件，读/写访问，运行时|

|小写|示例|
|---------------|--------------|
|复合词中的第二个单词，如果它是语音的另一部分或修改第一个单词的分词|如何，起飞|
|文章，除非标题中的第一个单词|a、an、the|
|坐标连合|和，但是，也不，或|
|动词短语之外有四个或更少字母的单词的介词|到，至于，出，在上面|
|在不定式短语中使用时的"To"|"如何格式化硬盘"|

##### <a name="sentence-case"></a>判刑案例
 句子案例是书写的标准大写方法，其中只有句子的第一个单词大写，以及任何正确的名词和代词"I"。 通常，对于全球受众来说，句子案例更容易阅读，尤其是当内容将由机器翻译时。 使用句子案例：

1. **状态栏消息。** 这些操作简单、简短，仅提供状态信息。 示例："加载项目文件"

2. **所有其他 UI 元素**，包括标签、复选框、单选按钮和列表框项。 示例："选择列表中的所有项目"

### <a name="text-formatting"></a>文本格式
 Visual Studio 2013 中的默认文本格式由[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)控制。 此服务有助于确保在整个 IDE（集成开发环境）中保持一致的字体外观，您必须使用它来保证用户获得一致的体验。

 Visual Studio 字体服务使用的默认大小来自 Windows，显示为 9 磅。

 您可以将格式应用于环境字体。 本主题介绍如何使用样式以及在哪里使用样式。 有关实现信息，请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

#### <a name="bold-text"></a>粗体文本
 粗体文本在视觉工作室中谨慎使用，应保留为：

- 向导中的问题标签

- 在解决方案资源管理器中指定活动项目

- "属性"工具窗口中的重写值

- 可视化基本编辑器下拉列表中的某些事件

- 网页文档大纲中的服务器生成的内容

- 复杂对话框或设计器 UI 中的节标题

#### <a name="italics"></a>斜体
 Visual Studio 不使用斜体或粗体斜体文本。

#### <a name="color"></a>Color

- 蓝色保留为超链接（导航和命令），绝不应用于方向。

- 出于以下目的，可以着色较大的标题（环境字体 x 155% 或更高）：

  - 为签名视觉工作室 UI 提供视觉吸引力

  - 呼吁关注特定区域

  - 提供从标准深灰色/黑色环境文本颜色的缓解

- 标题中的颜色应利用现有的 Visual Studio 品牌颜色，主要是主要的紫色、#FF68217A。

- 在标题中使用颜色时，必须遵守[Windows 颜色准则](https://msdn.microsoft.com/library/dn742482.aspx)，包括对比度和其他辅助功能注意事项。

### <a name="font-size"></a>字号
 Visual Studio UI 设计具有更轻的外观和更多的空白空间。 在可能的情况下，铬和标题条已减少或删除。 虽然信息密度是 Visual Studio 中的一项要求，但排版仍然很重要，重点是更开放的线条间距和字体大小和权重的变化。

 下表包括 Visual Studio 中使用的显示字体的设计详细信息和可视化示例。 某些显示字体变体的大小和权重（如半光或轻）已编码到其外观中。

 所有显示字体的实现代码段都可以在[格式（缩放/粗体）引用](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)中找到。

#### <a name="375-environment-font--light"></a>375% 环境字体 + 浅色

|||
|-|-|
|**用法：** 罕见。 仅具有唯一品牌 UI。<br /><br /> **执行：**<br /><br /> - 使用句子案例<br />- 始终使用重量轻<br /><br /> **请勿：**<br /><br /> - 用于签名 UI 以外的 UI，如起始页<br />- 粗体、斜体或粗斜体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：** 34 pt 塞戈 UI 灯<br /><br /> **视觉示例：**<br /><br /> *当前未使用。可在"开始页"中使用。*|

#### <a name="310-environment-font--light"></a>310% 环境字体 + 浅色

|||
|-|-|
|**使用：**<br /><br /> - 签名对话框中较大的标题<br />- 主要报告标题<br /><br /> **执行：**<br /><br /> - 使用句子案例<br />- 始终使用重量轻<br /><br /> **请勿：**<br /><br /> - 用于签名 UI 以外的 UI，如起始页<br />- 粗体、斜体或粗斜体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：** 28 pt 塞戈 UI 灯<br /><br /> **视觉示例：**<br /><br /> ![310% 环境字体&#43;光标题的示例](../../extensibility/ux-guidelines/media/0202-a-ef310.png "0202-a_EF310")|

#### <a name="200-environment-font--semilight"></a>200% 环境字体 + 半光

|||
|-|-|
|**使用：**<br /><br /> - 副标题<br />- 中小型对话框中的标题<br /><br /> **执行：**<br /><br /> - 使用句子案例<br />- 始终使用半轻重量<br /><br /> **请勿：**<br /><br /> - 粗体、斜体或粗斜体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：** 18 pt 塞戈 UI 塞米莱特<br /><br /> **视觉示例：**<br /><br /> ![200% 环境字体&#43;半光的示例](../../extensibility/ux-guidelines/media/0202-b-ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>155% 环境字体

|||
|-|-|
|**使用：**<br /><br /> - 文档井 UI 中的节标题<br />- 报告<br /><br /> **执行：** 使用句子案例<br /><br /> **请勿：**<br /><br /> - 粗体、斜体或粗斜体<br />- 用于正文文本<br />- 在标准视觉工作室控件中使用<br />- 在工具窗口中使用|**显示为：** 14 pt 塞戈 UI<br /><br /> **视觉示例：**<br /><br /> ![155% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-c-ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>133% 环境字体

|||
|-|-|
|**使用：**<br /><br /> - 签名对话框中的较小子标题<br />- 文档井 UI 中的较小子标题<br /><br /> **执行：** 使用句子案例<br /><br /> **请勿：**<br /><br /> - 粗体、斜体或粗斜体<br />- 用于正文文本<br />- 在标准视觉工作室控件中使用<br />- 在工具窗口中使用|**显示为：** 12 pt 塞戈 UI<br /><br /> **视觉示例：**<br /><br /> ![133% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-d-ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>122% 环境字体

|||
|-|-|
|**使用：**<br /><br /> - 签名对话框中的节标题<br />- 树视图中的顶部节点<br />- 垂直选项卡导航<br /><br /> **执行：** 使用句子案例<br /><br /> **请勿：**<br /><br /> - 粗体、斜体或粗斜体<br />- 用于正文文本<br />- 在标准视觉工作室控件中使用<br />- 在工具窗口中使用|**显示为：** 11 pt Segoe UI<br /><br /> **视觉示例：**<br /><br /> ![122% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-e-ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>环境字体 = 粗体

|||
|-|-|
|**使用：**<br /><br /> - 签名对话框中的标签和子头<br />- 报表中的标签和子头<br />- 文档井 UI 中的标签和子头<br /><br /> **执行：**<br /><br /> - 使用句子案例<br />- 使用粗体重量<br /><br /> **请勿：**<br /><br /> - 斜体或粗斜体<br />- 用于正文文本<br />- 在标准视觉工作室控件中使用<br />- 在工具窗口中使用|**显示为：** 粗体 9 pt Segoe UI<br /><br /> **视觉示例：**<br /><br /> ![环境字体&#43;粗体标题的示例](../../extensibility/ux-guidelines/media/0202-f-efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>环境字体

|||
|-|-|
|**用法：** 所有其他文本<br /><br /> **执行：** 使用句子案例<br /><br /> **不要：** 斜体或粗斜体|**显示为：** 9 pt Segoe UI<br /><br /> **视觉示例：**<br /><br /> ![环境字体的示例](../../extensibility/ux-guidelines/media/0202-g-ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>填充和间距
 标题需要围绕它们的空间来给予适当的强调。 此空间因点大小和标题附近的其他内容而异，例如水平规则或环境字体中的一行文本。

- 标题本身的理想填充应为大写字符高度空间的 90%。 例如，28 pt Segoe UI Light 标题的上限高度为 26 磅，填充高度应约为 23 pt，即大约 31 像素。

- 标题周围的最小空间应为大写字符高度的 50%。 当标题附带规则或其他紧密拟合元素时，可以使用较少的空间。

- 带粗体环境字体文本应遵循默认行高度间距和填充。

## <a name="see-also"></a>另请参阅
 [MSDN： 字体 （窗口）](https://msdn.microsoft.com/library/windows/desktop/dn742483\(v=vs.85\).aspx) [MSDN： 用户界面文本 （窗口）](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)
