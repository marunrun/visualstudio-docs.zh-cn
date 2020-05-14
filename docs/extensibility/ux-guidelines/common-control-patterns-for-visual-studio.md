---
title: 视觉工作室的常见控制模式 |微软文档
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b0b5a1904c01f5688a00e45de7feed7ae326d9b3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698717"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio 的公共控件模式
## <a name="common-controls"></a><a name="BKMK_CommonControls"></a>常见控件

### <a name="overview"></a>概述
常见控件占可视化工作室中用户界面的大多数。 可视化工作室界面中使用的大多数常见控件应遵循[Windows 桌面交互指南](/windows/desktop/uxguide/controls)。 本主题特定于 Visual Studio，并介绍增强这些 Windows 指南的特殊情况或详细信息。

#### <a name="common-controls-in-this-topic"></a>本主题中的常见控件

- [滚动条形图](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [输入字段](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [组合框和下拉列表](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [复选框](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [单选按钮](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [组帧](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [树视图](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>视觉样式
样式控件时首先要考虑的是控件是否将在主题 UI 中使用。 标准 UI 中的控件是非主题 UI，必须遵循[正常的 Windows 桌面样式](/windows/desktop/uxguide/controls)，这意味着它们不会重新模板化，并且应出现在其默认控件外观中。

- **标准（实用程序）对话框：** 非主题对话框。 不要重新模板化。 使用基本控件样式默认值。

- **工具窗口、文档编辑器、设计曲面和主题对话框：** 使用彩色服务使用专门的主题外观。

### <a name="scroll-bars"></a><a name="BKMK_Scrollbars"></a>滚动条形图
 滚动条应遵循[Windows 滚动栏的常见交互模式](/windows/desktop/Controls/about-scroll-bars)，除非它们包含内容信息（如代码编辑器中）。"

### <a name="input-fields"></a><a name="BKMK_InputFields"></a>输入字段
 对于典型的交互行为，请遵循[文本框的 Windows 桌面指南](/windows/desktop/uxguide/ctrl-text-boxes)。

#### <a name="visual-style"></a>视觉样式

- 输入字段不应在实用程序对话框中设置样式。 使用控件固有的基本样式。

- 主题输入字段应仅用于主题对话框和工具窗口。

#### <a name="specialized-interactions"></a>专业互动

- 只读字段将具有灰色（禁用）背景，但默认（活动）前景。

- 所需的字段应具有**\<所需的>** 作为水印。 除非在极少数情况下，否则不应更改背景的颜色。

- 错误验证：请参阅[可视化工作室的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- 输入字段的大小应适合内容，而不是适合显示它们的窗口的宽度，也不应任意匹配长字段的长度（如路径）。 长度可能向用户指示字段中允许的字符数的限制。

     ![输入字段长度不正确：名称不太可能长。](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")<br />输入字段长度不正确：名称不太可能长。

     ![正确的输入字段长度：输入字段是预期内容的合理宽度。](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")<br />正确的输入字段长度：输入字段是预期内容的合理宽度。

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a>组合框和下拉列表
对于典型的交互行为，请遵循[Windows 桌面指南，查看下拉列表和组合框](/windows/desktop/uxguide/ctrl-drop)。

#### <a name="visual-style"></a>视觉样式

- 在实用程序对话框中，不要重新模板控件。 使用控件固有的基本样式。

- 在主题 UI 中，组合框和下拉列表遵循控件的标准主题。

#### <a name="layout"></a>布局
组合框和下拉列表的大小应适合内容，不适合显示它们的窗口的宽度，也不必像路径一样任意匹配长字段的长度。

![不正确：下拉宽度太长，无法显示内容。](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")<br />不正确：下拉宽度太长，无法显示内容。

![正确：下拉列表的大小允许翻译增长，但并非不必要地长。](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707-04_CorrectDropDownLayout")<br />正确：下拉列表的大小允许翻译增长，但并非不必要地长。

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a>复选框
对于典型的交互行为，请按照["Windows 桌面"指南进行复选框](/windows/desktop/uxguide/ctrl-check-boxes)。

#### <a name="visual-style"></a>视觉样式

- 在实用程序对话框中，不要重新模板控件。 使用控件固有的基本样式。

- 在主题 UI 中，复选框遵循控件的标准主题。

#### <a name="specialized-interactions"></a>专业互动

- 与复选框的交互绝不能弹出对话框或导航到其他区域。

- 将复选框与第一行文本的基线对齐。

     ![不正确：复选框以文本为中心。](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")<br />不正确：复选框以文本为中心。

     ![正确：复选框与文本的第一行对齐。](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")<br />正确：复选框与文本的第一行对齐。

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a>单选按钮
对于典型的交互行为，请遵循[Windows 桌面指南进行单选按钮](/windows/desktop/uxguide/ctrl-radio-buttons)。

#### <a name="visual-style"></a>视觉样式
在实用程序对话框中，不要设置单选按钮的样式。 使用控件固有的基本样式。

#### <a name="specialized-interactions"></a>专业互动
不需要使用组帧来封闭无线电选择，除非您需要在紧凑的布局中保持组区分。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a>组帧
对于典型的交互行为，请遵循[组帧的 Windows 桌面指南](/windows/desktop/uxguide/ctrl-group-boxes)。

#### <a name="visual-style"></a>视觉样式
在实用程序对话框中，不要对组框架进行样式设置。 使用控件固有的基本样式。

#### <a name="layout"></a>布局

- 不需要使用组帧来封闭无线电选择，除非您需要在紧凑的布局中保持组区分。

- 切勿将组帧用于单个控件。

- 有时可以使用水平规则而不是组帧容器。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a>文本控件

### <a name="static-text-fields"></a>静态文本字段

静态文本字段显示只读信息，用户无法选择。 避免将其用于用户可能想要复制到剪贴板的任何文本。 但是，只读静态文本可以更改以反映状态的变化。 在下面的示例中，"信息"组下的"输出名称"静态文本将更改以反映对它上方的根命名空间文本框所做的任何更改。

有两种方法可以显示静态文本信息。

当不存在分组冲突时，静态文本可以在对话框中自行显示，没有任何包含。 确定是否确实有必要使用框的额外行。 例如，在组行创建的节下显示目录路径，如下所示：

![文本控件中的静态文本信息](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "显示静态文本.png")<br />文本控件中的静态文本信息

在存在其他分组区域的对话框中，信息包含将有助于可读性，并且当可以隐藏或显示节（如 **"属性"窗口**描述窗格中）或希望与类似 UI 保持一致时，将静态文本放在框中。 此组框应为单个规则，并带有 以下`ButtonShadow`颜色：

!["属性"窗口中的静态文本](../../extensibility/ux-guidelines/media/PropertiesWindow.png "属性窗口.png")<br />"属性"窗口中的静态文本

### <a name="read-only-text-box"></a>只读文本框

这允许用户选择字段中的文本，但不能编辑它。 这些文本框与通常的 3D 凿子接壤，带有`ButtonShadow`填充。

当用户更改关联的控件（如选中/取消选中复选框或选择/取消选择单选按钮）时，文本框可能会变为活动（可编辑）。 例如，在下面显示**的&gt;"工具选项**"页中，"**主页"文本**框在取消选中 **"使用默认**"复选框时变为活动状态。

![只读文本框，显示非活动状态和活动状态](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "阅读唯一文本框.png")<br />只读文本框，显示非活动状态和活动状态

### <a name="using-text-in-dialogs"></a>在对话框中使用文本

对话框中文本的关键准则：

- 文本框、列表框和框架的标签在非主题对话框中以动词开头，仅对第一个单词具有初始大写，以冒号结尾。

    > 主题对话框中的文本控件遵循[Windows 桌面 UX 准则](/windows/desktop/uxguide/top-violations)，不采用结束标点符号，但帮助链接中的问号除外。

- 复选框和选项按钮的标签以动词开头，第一个单词的初始大写字母，并且没有结束标点符号。

- 按钮、菜单、菜单项和选项卡的标签在每个单词（标题大小写）上都有初始大写字母。

- 标签术语应与其他对话框中的类似标签一致。

- 如果可能，请让编写器/编辑器在文本提交开发人员进行实现之前编写或批准该文本。

- 所有控件都应具有标签，除非在选项卡已足够的特殊情况下。
在适当时使用帮助器文本。

### <a name="helper-text"></a>帮助者文本

包含在对话框中，以帮助用户了解对话框的用途或指示要执行的操作。 仅当需要时才应使用帮助器文本，以避免使简单对话框变得杂乱无章。 帮助器文本的两种变体是对话框和水印。

遵循帮助器文本的常见位置，并选择性地引入新区域。 帮助器文本的常见方案包括：

- 对话框中的帮助器文本，以提供有关如何与复杂对话框交互的其他方向。

- 在空工具窗口或对话框中为文本加水印，以解释为什么没有内容可见。

- 描述窗格，如 **"属性"窗口**的底部。

- 在空编辑器中添加水印文本，以解释用户应该采取哪些操作来开始。

### <a name="dialog-helper-text"></a>对话框帮助程序文本

用户体验设计器可以帮助确定帮助器文本何时合适。 设计器可以定义帮助器文本的显示位置及其一般内容。 用户帮助可以编写/编辑实际文本。

### <a name="watermarks"></a>水印

对话框受益于略有不同的水印准则。 由于对话框可能显示许多 UI 元素（标签、提示文本、按钮和其他包含文本的容器控件），因此，尤其是当这些控件以黑色显示时，水印在深灰色（VSColor： `ButtonShadow`） 中效果更好。 通常，水印出现在控件内，就像带有白色背景的列表框 （VSColor： `Window`）。

- 文本以深灰色显示 （VSColor： `ButtonShadow`）。 但是，如果水印出现在中等灰色或其他颜色 （VSColor： `ButtonFace`） 背景上，并且担心其可读性，请使用黑色文本 （VSColor： `WindowText`）。

- 水印可以居中或向左刷新。 在做出对齐决策时应用标准设计规则。 无法在背景上选择水印。

![水印文本示例](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />水印文本示例

### <a name="context-specific-dynamic-text"></a>特定于上下文（动态）的文本

动态文本可以在对话框或无模式 UI 中使用两种方式之一：作为动态标签或动态内容。

- 动态标签：动态文本的常见用在描述性面板中，这些面板为所选项目提供了更多信息，例如，在对话框中，其中包含显示在右侧网格中的元素和属性的列表。 属性网格的标签可能是动态的，因此当在左侧选择项目时，右侧的网格将显示该特定项的信息。

- 动态文本：在需要以这种方式显示特定信息而不是常规信息的情况下非常有用，但应注意不要过度使用。

如果希望用户能够复制信息，则动态文本应位于只读文本字段中。

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a>按钮和超链接

### <a name="overview"></a>概述
按钮和链接控件（超链接）应遵循[有关超链接的基本 Windows 桌面指南](/windows/desktop/uxguide/ctrl-links)，以便进行使用、措辞、大小调整和间距。

### <a name="choosing-between-buttons-and-links"></a>在按钮和链接之间进行选择
传统上，按钮已用于操作，超链接已保留用于导航。 按钮可用于所有情况，但链接的角色已在 Visual Studio 中扩展，以便在某些情况下，按钮和链接更容易互换。

何时使用命令按钮：

- 主要命令

- 显示用于收集输入或做出选择的窗口，即使它们是辅助命令

- 破坏性或不可逆转的行动

- 向导和页面流中的承诺按钮

避免在工具窗口中出现命令按钮，或者需要标签的单词超过两个单词。 链接可以具有较长的标签。

 何时使用链接：

- 导航到其他窗口、文档或网页

- 需要较长的标签或短句来描述行动意图的情况

- 按钮将淹没 UI 的狭小空间，前提是该操作不具有破坏性或不可逆性

- 在存在许多命令的情况下取消强调辅助命令

#### <a name="examples"></a>示例
![状态消息后信息栏中使用的命令链接](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703-01_CommandLinkInfobar")<br />状态消息后信息栏中使用的命令链接

![CodeLens 弹出中使用的链接](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703-02_LinksInCodeLens")<br />CodeLens 弹出中使用的链接

![用于次要命令的链接，其中按钮会吸引太多注意力](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")<br />用于次要命令的链接，其中按钮会吸引太多注意力

### <a name="common-buttons"></a>常用按钮

#### <a name="text"></a>Text
遵循[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)中的编写指南。

#### <a name="visual-style"></a>视觉样式

##### <a name="standard-unthemed"></a>标准（无主题）
Visual Studio 中的大多数按钮将显示在实用程序对话框中，不应设置样式。 它们应反映操作系统规定的按钮的标准外观。

##### <a name="themed"></a>主题
在某些情况下，可以在样式的 UI 中使用按钮，并且这些按钮必须正确设置样式。 有关主题控件的信息[，请参阅对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)。

### <a name="special-buttons"></a>特殊按钮

#### <a name="browse-buttons"></a>浏览。。。按钮
**[浏览...]** 按钮用于网格、对话框、工具窗口以及其他无模式 UI 元素。 它们显示一个选取器，可帮助用户将值填充到控件中。 此按钮有两种变体，长和短。

![长 [浏览...] 按钮](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703-04_BrowseLong")<br />长 [浏览...] 按钮

![仅省略号短 [...] 按钮](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703-05_BrowseShort")<br />仅省略号短 [...] 按钮

何时使用仅椭圆短按钮：

- 如果对话框中有多个长 **[Browse... ]** 按钮，例如多个字段允许浏览时。 使用每个短 **[...]** 按钮，以避免此情况创建的混乱访问密钥 **（&浏览**和 B **&行**在同一对话框）。

- 在紧密对话框中，或者当没有合理位置放置长按钮时。

- 如果按钮将显示在网格控件中。

使用按钮的指南：

- 不要使用访问密钥。 要使用键盘访问它，用户必须从相邻控件选项卡。 确保选项卡顺序使任何浏览按钮在将填充的字段之后立即落下。 切勿在第一个期间下方使用下划线。

- 将 Microsoft 活动辅助功能 （MSAA）**名称**属性设置为 **"浏览..."（** 包括省略号），以便屏幕阅读器将其读取为"浏览"，而不是"点点"或"周期周期"。 对于托管控件，这意味着设置 **"可访问名称"** 属性。

- 切勿对除浏览操作以外的任何内容使用省略**号 [...]** 按钮。 例如，如果您需要 **[New...]** 按钮，但没有足够的空间用于文本，则需要重新设计对话框。

##### <a name="sizing-and-spacing"></a>大小调整和间距
![大小调整 [浏览... ] 按钮：标准版本为 75x23 像素，短版本为 26x23 像素](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703-06_BrowseSizing")<br />调整[浏览...]按钮大小

![间距 [浏览...] 按钮：相关控件和标准浏览按钮 7 像素之间的间距，相关控件和短浏览按钮之间的间距 5 像素](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703-07_BrowseSpacing")<br />设置[浏览...]按钮间距

#### <a name="graphical-buttons"></a>图形按钮
某些按钮应始终使用图形图像，并且绝不包含文本以节省空间并避免本地化问题。 这些通常用于字段选取器和其他可排序列表。

> [!NOTE]
> 用户必须选项卡到这些按钮（没有访问键），所以将它们按合理的顺序排列。 将`name`按钮的属性映射到它所执行的操作，以便屏幕阅读器正确解释按钮操作。

| 函数 | Button |
| --- | --- |
| 添加 | ![图形“添加”按钮](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703-08_ButtonAdd") |
| 删除 | ![图形“删除”按钮](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703-09_ButtonRemove") |
| 全部添加 | ![图形“全部添加”按钮](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703-10_ButtonAddAll") |
| 全部删除 | ![图形“全部删除”按钮](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703-11_ButtonRemoveAll") |
| “上移” | ![图形“上移”按钮](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703-12_ButtonMoveUp") |
| “下移” | ![图形“下移”按钮](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703-13_ButtonMoveDown") |
| 删除 | ![图形“删除”按钮](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703-14_ButtonDelete") |

##### <a name="sizing-and-spacing"></a>大小调整和间距
图形按钮的尺寸与 **[Browse...]** 按钮（26x23 像素）的简短版本相同：

![按钮上的图形图像的外观，带透明颜色显示，不显示透明颜色](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")<br />按钮上的图形图像的外观，带透明颜色显示，不显示透明颜色

### <a name="hyperlinks"></a>超链接
超链接非常适合基于导航的操作，例如打开帮助主题、模式对话框或向导。 如果用于命令的超链接，它应始终显示对 UI 的可见且明显的更改。 通常，最好使用按钮传达提交操作的操作（如保存、取消和删除）。

#### <a name="writing-style"></a>写入样式
按照[Windows 桌面指南进行用户界面文本](/windows/desktop/uxguide/text-ui)。 不要使用"了解更多"，"告诉我更多关于"或"获取有关此帮助"的短语。 相反，短语"帮助"会链接文本，以表示帮助内容回答的主要问题。 例如，"**如何向服务器资源管理器添加服务器？"**

#### <a name="visual-style"></a>视觉样式

- 超链接应始终使用[VSColor 服务](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。 如果超链接的样式不正确，则在激活时闪烁红色，或在访问后显示其他颜色。

- 除非链接是完整句子中的句子片段（如水印中）中，否则不要在控件静止状态处包含下划线。

- 下划线不应显示在悬停上。 相反，向用户反馈的链接处于活动状态是轻微的颜色变化和相应的链接光标。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a>树视图

树视图提供了一种将复杂列表组织到父子组的方法。 用户可以展开或折叠父组以显示或隐藏基础子项。 可以选择树视图中的每个项以提供进一步操作。

### <a name="tree-view-visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a>树视图视觉样式

#### <a name="expanders"></a>扩展器
树视图控件应符合 Windows 和可视化工作室使用的扩展程序设计。 每个节点使用扩展器控件来显示或隐藏基础项。 使用扩展器控件为在 Windows 和 Visual Studio 中遇到不同树视图的用户提供一致性。

![正确：使用扩展器控件正确设置树视图节点样式](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正确：使用扩展器控件正确设置树视图节点样式

![不正确：树视图节点的样式不正确](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705-2_TreeViewIncorrect1")<br />不正确：树视图节点的样式不正确

#### <a name="selection"></a>选项
在树视图中选择节点时，高光应扩展到树视图控件的完整宽度。 这有助于用户清楚地识别他们选择了哪些项目。 选择颜色应反映当前视觉工作室主题。

![正确：所选节点的高光适合树视图控件的整个宽度。](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正确：所选节点的高光适合树视图控件的整个宽度。

![不正确：所选节点的高光不适合树视图控件的整个宽度。](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705-3_TreeViewIncorrect2")<br />不正确：所选节点的高光不适合树视图控件的整个宽度。

#### <a name="icons"></a>图标
仅当图标有助于直观地识别项之间的差异时，才应在树视图控件中使用图标。 通常，图标应仅在异构列表中使用，其中图标携带信息以区分元素的类型。 在使用图标的同质列表中通常可以被视为噪声，应避免使用图标。 在这种情况下，组图标（父图标）可以传达其中的项目类型。 此规则的例外情况是，如果图标是动态的，并且用于指示状态。

#### <a name="scroll-bars"></a>滚动栏
如果内容适合树视图控件，应始终隐藏滚动条。 滚动条可以隐藏，或在可滚动窗口中半透明，并在包含树视图的窗口具有焦点时或在树视图本身的悬停时显示。

![显示垂直滚动条和水平滚动条，因为内容已超过树视图控件的限制。](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705-4_Scrollbars")<br />显示垂直滚动条和水平滚动条，因为内容已超过树视图控件的限制。

### <a name="tree-view-interactions"></a><a name="BKMK_TreeViewInteractions"></a>树视图交互

#### <a name="context-menus"></a>上下文菜单
树视图节点可以在上下文菜单中显示子菜单选项。 通常，当用户右键单击某个项目或在选择该项目的情况下按下 Windows 键盘上的"菜单"键时，将发生这种情况。 节点获得焦点并被选中非常重要。 这有助于用户识别子菜单属于哪个项。

![已生成上下文菜单的项获得焦点，以通知用户已选择哪个项。](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705-5_ContextMenu")<br />已生成上下文菜单的项获得焦点，以通知用户已选择哪个项。

#### <a name="keyboard"></a>键盘
树视图应提供使用键盘选择项和展开/折叠节点的能力。 这可确保导航满足我们的辅助功能要求。

##### <a name="tree-view-control"></a>树视图控件
可视化工作室树控件应遵循常见的键盘导航：

- **向上箭头：** 通过向上移动树来选择项目

- **向下箭头：** 通过向下移动树来选择项目

- **右箭头：** 展开树中的节点

- **左箭头：** 折叠树中的节点

- **输入键：** 启动、加载、执行所选项目

##### <a name="trid-tree-view-and-grid-view"></a>Trid（树视图和网格视图）
trid 控件是一种复杂控件，其中包含网格中的树视图。 展开、折叠和导航树应遵循与树视图相同的键盘命令，并添加以下内容：

- **右箭头：** 展开节点。 扩展节点后，它应继续导航到右侧最近的列。 导航应在行的末尾停止。

- **选项卡：** 导航到右侧最近的单元格。  在行的末尾，导航继续到下一行。

- **移位 + 选项卡：** 导航到左侧最近的单元格。  在行的开头，导航继续到上一行中最右侧的单元格。

![视觉工作室中的一个三恶维控制](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705-6_Trid")<br />视觉工作室中的一个三恶维控制
