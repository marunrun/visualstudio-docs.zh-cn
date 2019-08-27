---
title: Visual Studio 的常见控件模式 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33becb67adb0453adef111ca2c8fb0d2b2e6edfc
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67890975"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio 的常见控件模式
## <a name="BKMK_CommonControls"></a> 公共控件

### <a name="overview"></a>概述
公共控件构成了大多数 Visual Studio 中的用户界面。 在 Visual Studio 界面中使用的最常见控件应遵循[Windows 桌面的交互指南](/windows/desktop/uxguide/controls)。 本主题是特定于 Visual Studio，并介绍了特殊情形或扩充这些 Windows 准则的详细信息。

#### <a name="common-controls-in-this-topic"></a>本主题中的公共控件

- [滚动条](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [输入的字段](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [组合框和下拉列表](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [复选框](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [单选按钮](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [组帧](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [树视图](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>视觉样式
设置控件的样式时要考虑的第一个操作是是否主题化 UI 中使用的控件。 标准用户界面中的控件为非主题 UI 并且必须遵循[普通的 Windows 桌面样式](/windows/desktop/uxguide/controls)，这意味着它们不是重新模板化，应会出现在其默认控件外观。

- **标准 （实用工具） 对话框：** 不主题化。 不重新创建模板。 使用基本的控件样式的默认值。

- **工具窗口、 文档编辑器，设计图面和主题化的对话框：** 使用专用应用主题外观，可以使用颜色服务。

### <a name="BKMK_Scrollbars"></a> 滚动条
 滚动条应遵循[Windows 的常见交互模式滚动条](/windows/desktop/Controls/about-scroll-bars)除非它们增加内容的信息，如代码编辑器中。

### <a name="BKMK_InputFields"></a> 输入的字段
 典型的交互行为，请按照[文本框中的 Windows 桌面准则](/windows/desktop/uxguide/ctrl-text-boxes)。

#### <a name="visual-style"></a>视觉样式

- 实用程序对话框中，输入的字段不应设置样式。 使用该控件中的内部的基本样式。

- 主题化的输入的字段应仅用于主题化的对话框和工具窗口。

#### <a name="specialized-interactions"></a>专用的交互

- 只读字段将具有灰色 （禁用） 背景但 （活动） 的默认前景色。

- 所需的字段应有 **\<所需>** 一样中其水印。 不应更改除中极少数情况下的背景的颜色。

- 错误验证：请参阅[Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- 输入的字段，应调整以适应其内容，不适合在其中显示它们，在窗口的宽度也以任意匹配长的字段，例如，路径的长度。 长度可能会向用户指示的关于字段中允许多少个字符的限制。

     ![不正确的输入的字段长度： 不太可能的名称将是这么一段时间。](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707年 01_IncorrectInputFieldControl")<br />不正确的输入的字段长度： 不太可能的名称将是这么一段时间。

     ![更正输入的字段长度： 输入的字段是预期的内容的合理宽度。](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707年 02_CorrectInputFieldControl")<br />更正输入的字段长度： 输入的字段是预期的内容的合理宽度。

### <a name="BKMK_ComboBoxesAndDropDowns"></a> 组合框和下拉列表
典型的交互行为，请按照[下拉列表和组合框的 Windows 桌面准则](/windows/desktop/uxguide/ctrl-drop)。

#### <a name="visual-style"></a>视觉样式

- 在实用程序对话框中，该控件不重新创建模板。 使用该控件中的内部的基本样式。

- 在主题 UI 中，组合框和下拉列表按照标准主题的控件。

#### <a name="layout"></a>布局
组合框和下拉列表确定应将其调整为适应内容，不适合在其中显示它们，在窗口的宽度也以任意匹配长的字段，例如，路径的长度。

![不正确： 下拉列表宽度是将显示的内容太长。](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707年 03_IncorrectDropDownLayout")<br />不正确： 下拉列表宽度是将显示的内容太长。

![正确： 下拉列表会调整大小以允许转换的增长，但不是会不必要地长。](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707年 04_CorrectDropDownLayout")<br />正确： 下拉列表会调整大小以允许转换的增长，但不是会不必要地长。

### <a name="BKMK_CheckBoxes"></a> 复选框
典型的交互行为，请按照[复选框的 Windows 桌面准则](/windows/desktop/uxguide/ctrl-check-boxes)。

#### <a name="visual-style"></a>视觉样式

- 在实用程序对话框中，该控件不重新创建模板。 使用该控件中的内部的基本样式。

- 在主题 UI 中的复选框按照标准主题的控件。

#### <a name="specialized-interactions"></a>专用的交互

- 有一个复选框的交互必须永远不会弹出一个对话框，或导航到另一个区域。

- 使复选框与的第一行文本基线对齐。

     ![不正确： 复选框的文本为居中。](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707年 05_IncorrectCheckBoxAlign")<br />不正确： 复选框的文本为居中。

     ![正确： 复选框与文本的第一行。](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707年 06_CorrectCheckBoxAlign")<br />正确： 复选框与文本的第一行。

### <a name="BKMK_RadioButtons"></a> 单选按钮
典型的交互行为，请按照[单选按钮的 Windows 桌面准则](/windows/desktop/uxguide/ctrl-radio-buttons)。

#### <a name="visual-style"></a>视觉样式
实用程序对话框中执行操作样式的单选按钮。 使用该控件中的内部的基本样式。

#### <a name="specialized-interactions"></a>专用的交互
不需要使用一个组框以便包含单选选项，除非您需要维护组紧密布局中的差异。

### <a name="BKMK_GroupFrames"></a> 组帧
典型的交互行为，请按照[组帧的 Windows 桌面准则](/windows/desktop/uxguide/ctrl-group-boxes)。

#### <a name="visual-style"></a>视觉样式
实用程序对话框中未设置样式组帧。 使用该控件中的内部的基本样式。

#### <a name="layout"></a>布局

- 不需要使用一个组框以便包含单选选项，除非您需要维护组紧密布局中的差异。

- 单个控件永远不会使用一个组框。

- 有时是可接受使用水平规则而不是组帧容器。

## <a name="BKMK_TextControls"></a> 文本控件

### <a name="static-text-fields"></a>静态文本字段

静态文本字段不能由用户选择和显示只读信息。 避免使用它的任何文本，用户可能想要复制到剪贴板。 但是，只读的静态文本可以更改以反映状态的更改。 在以下示例中，信息组更改以反映其上方的根 Namespace 文本框中所做的任何更改下的输出名称静态文本。

有两种方法来显示静态文本的信息。

静态文本可以是在其自己在对话框中，而无需任何包含时，则没有分组会发生冲突。 决定框的多余的行是否确实必要。 显示创建的组行中，部分下的目录路径是一个示例，如下所示：

![在文本控件中的静态文本信息](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "DisplayingStaticText.png")<br />在文本控件中的静态文本信息

在对话框中，存在其他分组的区域，其中包含的信息有助于提高可读性，和一个部分可以隐藏或显示时 (如**属性窗口**说明窗格) 或你想要与类似 UI 保持一致将静态文本放在一个框内。 此组中应该是一条规则和带有`ButtonShadow`:

![在属性窗口中的静态文本](../../extensibility/ux-guidelines/media/PropertiesWindow.png "PropertiesWindow.png")<br />在属性窗口中的静态文本

### <a name="read-only-text-box"></a>只读文本框

这允许用户选择该字段内的文本，但无法编辑它。 通过使用常用的三维方形来界定这些文本框`ButtonShadow`填充。

文本框中就会被激活时用户更改关联的控件，如选中/取消选中复选框或选择/取消选择的单选按钮 （编辑）。 例如，在**工具&gt;选项**页，如下所示**主页**文本框中将变为活动状态时**使用默认的**复选框处于未选中状态。

![只读文本框中，显示非活动和活动状态](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "ReadOnlyTextBox.png")<br />只读文本框中，显示非活动和活动状态

### <a name="using-text-in-dialogs"></a>在对话框中使用文本

在对话框中的文本的重要原则：

- 文本框、 列表框中和帧 unthemed 对话框中的标签以动词开头、 对第一个单词，大写的缩写形式和以冒号结尾。

    > 主题对话框中的文本控件遵循[Windows 桌面的用户体验指南](/windows/desktop/uxguide/top-violations)且不会结束标点，除了帮助链接中的问号。

- 复选框和选项按钮的标签开头动词，第一个单词，首字母大写，并且有没有结束标点。

- 按钮、 菜单、 菜单项和选项卡的标签对每个单词 （首字母大写） 的首字母大写。

- 标签术语应与其他对话框中的类似标签一致。

- 如果可能，具有写入或先转到实现开发人员批准文本编写器/编辑器。

- 所有控件都应都具有除标签的特殊情况下在哪些按 tab 键就足够了。
使用在适当的帮助程序文本。

### <a name="helper-text"></a>帮助程序文本

包含在对话框以帮助用户了解在对话框的目的或以指示要采取的操作。 帮助程序文本应使用仅在需要时以避免导致简单的对话框。 帮助程序文本的两个变体是对话框和水印。

按照常用帮助程序文本的位置并将有选择地引入了新的区域。 帮助程序文本的常见方案是：

- 在对话框中，提供有关如何与复杂对话框进行交互的其他方向的帮助程序文本。

- 中的空工具窗口或对话框，以解释为什么没有内容是可见的水印文本。

- 说明窗格中，就像在底部**属性窗口**。

- 水印文本在空编辑器，以解释用户若要开始所应采取什么操作。

### <a name="dialog-helper-text"></a>对话框帮助程序文本

用户体验设计器可帮助确定何时适合帮助程序文本。 在设计器可以定义帮助程序文本以及其常规内容的显示位置。 用户协助可以写入/编辑的实际文本。

### <a name="watermarks"></a>水印

对话框受益于略有不同的水印指导原则。 由于出现一个对话框，可以正忙，有很多 UI 元素 （标签、 提示文本、 按钮和其他容器控件中的使用文本），尤其是水印时所显示为黑色，脱颖而出深灰色更好 (VSColor: `ButtonShadow`)。 水印通常显示在具有白色背景的列表框之类的控件 (VSColor: `Window`)。

- 文本显示在深灰色 (VSColor: `ButtonShadow`)。 但是，如果出现于中等灰色或其他颜色 (VSColor: `ButtonFace`) 背景，并且没有其可读性感到担忧，请转底黑字 (VSColor: `WindowText`)。

- 水印可以居中或两端对齐。 决定对齐方式时，将应用标准设计规则。 不能在背景上选择水印。

![水印文本示例](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />水印文本示例

### <a name="context-specific-dynamic-text"></a>特定于上下文的 （动态） 文本

动态文本可以是使用的一个对话框或无模式的用户界面中有两种： 或动态标签作为动态内容。

- 动态标签： 动态文本的常见用途是提供详细信息对于所选的项，如在对话框中，其中包含的元素和属性到右侧网格中显示这些元素的列表的描述性面板中。 在属性网格的标签可能是动态的以便在左侧选择的项，在右侧网格会显示该特定项的信息。

- 动态文本： 在其中需要这种方式，显示的特定信息并不是一般信息，但应格外小心，不使用过度的实例可能非常有用。

如果你希望用户能够复制信息，动态文本应为只读的文本字段中。

## <a name="BKMK_ButtonsAndHyperlinks"></a> 按钮和超链接

### <a name="overview"></a>概述
按钮和链接控件 （的超链接） 应遵循[上的超链接的基本 Windows 桌面指南](/windows/desktop/uxguide/ctrl-links)的使用情况，措词、 调整大小，和间距。

### <a name="choosing-between-buttons-and-links"></a>按钮和链接之间进行选择
传统上，操作使用按钮和导航保留的超链接。 按钮可在所有情况下，但链接的角色扩展了 Visual Studio，以便按钮和链接是更可互换的一些条件。

何时使用命令按钮：

- 主命令

- 显示用于收集输入的 windows 或做出选择，即使它们是辅助命令

- 破坏性或不可逆的操作

- 向导和页面流内的承诺按钮

避免在工具窗口中的命令按钮或如果标签需要两个以上的单词。 链接具有更长的标签。

 何时使用链接：

- 导航到另一个窗口、 文档或网页

- 情况下，需要更长的标签或简短句子来描述操作的目的

- 其中一个按钮将会严重影响 UI，前提是该操作不破坏性或不可逆的紧密空格

- 取消加重辅助命令的情况下在其中有很多命令

#### <a name="examples"></a>示例
![命令链接在以下状态消息信息栏中使用](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703 01_CommandLinkInfobar")<br />使用以下状态消息的信息栏命令链接

![使用 CodeLens 弹出窗口中的链接](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703 02_LinksInCodeLens")<br />CodeLens 弹出中使用的链接

![链接用于辅助命令的按钮会吸引投入大量精力](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703 03_LinksAsSecondaryCommands")<br />用于在辅助命令的按钮会吸引过多注意力的链接

### <a name="common-buttons"></a>常见的按钮

#### <a name="text"></a>Text
遵循中的写入准则[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)。

#### <a name="visual-style"></a>视觉样式

##### <a name="standard-unthemed"></a>标准 (unthemed)
在 Visual Studio 中的大多数按钮将显示实用程序对话框中，并且不应设置样式。 规定的操作系统，它们应反映标准按钮的外观。

##### <a name="themed"></a>主题
在某些情况下，可能带样式的用户界面中使用按钮，这些按钮必须适当地设置样式。 请参阅[对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)主题化控件上的信息。

### <a name="special-buttons"></a>特殊按钮

#### <a name="browse-buttons"></a>浏览...按钮
**[浏览...]** 按钮使用网格、 对话框和工具窗口和其他无模式的 UI 元素。 它们显示的选取器，可帮助用户填充到控件的值。 有两种变体，此按钮，长、 短。

![长 [浏览...] 按钮](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703 04_BrowseLong")<br />长 [浏览...] 按钮

![短仅省略号 [...] 按钮](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703 05_BrowseShort")<br />短仅省略号 [...] 按钮

何时使用仅限省略号的短按钮：

- 如果有多个长 **[浏览...]** 在对话框中，如当多个字段允许的浏览按钮。 使用短 **[...]** 为每个要避免这种情况下创建的令人困惑访问项的按钮 ( **& 浏览**并**B (&)** 相同对话框中)。

- 在紧密的对话框中，或没有合理的位置将很长的按钮。

- 如果该按钮将显示一个网格控件中。

使用该按钮的准则：

- 不要使用访问密钥。 若要访问它使用键盘，用户必须按 tab 键从相邻的控件。 请确保 tab 键顺序，以便其将填充的字段后立即处于任何浏览按钮。 永远不会使用下面的第一个期间下划线。

- 设置 Microsoft Active Accessibility (MSAA)**名称**属性设置为**浏览...** （包括省略号） 这样的屏幕阅读器将读取它作为"浏览"并不是"圆点点点"或"期间期期间。" 对于托管控件，这意味着设置**AccessibleName**属性。

- 永远不会使用省略号 **[...]** 用于浏览操作以外的按钮。 例如，如果您需要 **[新建...]** 按钮，但没有足够的空间的文本，然后在对话框需要重新设计。

##### <a name="sizing-and-spacing"></a>调整大小和间距
![大小调整 [浏览...] 按钮： 标准版为 75 x 23 像素，简短版本为 26 x 23 像素](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703 06_BrowseSizing")<br />调整[浏览...]按钮大小

![间距 [浏览...] 按钮： 相关的控件和标准的浏览按钮 7 像素之间的间距，相关的控件和简短浏览之间的间距按钮 5 像素](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703 07_BrowseSpacing")<br />设置[浏览...]按钮间距

#### <a name="graphical-buttons"></a>图形按钮
某些按钮应始终使用图形化的图像，并且永远不会包含文本以节省空间并避免本地化问题。 这些通常用于字段选取器和其他可排序的列表中。

> [!NOTE]
> 用户必须对这些按钮 （没有任何访问密钥） 选项卡上，因此将其放置在合理的顺序。 映射`name`属性，以便屏幕读取器正确解释此按钮的操作所需的操作的按钮。

| 函数 | Button |
| --- | --- |
| 添加 | ![图形"添加"按钮](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703 08_ButtonAdd") |
| 删除 | ![图形"删除"按钮](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703 09_ButtonRemove") |
| 全部添加 | ![图形"全部添加"按钮](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703 10_ButtonAddAll") |
| 删除所有 | ![图形"全部删除"按钮](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703 11_ButtonRemoveAll") |
| 上移 | ![图形"上移"按钮](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703 12_ButtonMoveUp") |
| 下移 | ![图形"下移"按钮](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703 13_ButtonMoveDown") |
| 删除 | ![图形"删除"按钮](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703 14_ButtonDelete") |

##### <a name="sizing-and-spacing"></a>调整大小和间距
大小调整图形按钮简短版本的相同 **[浏览...]** 按钮 （26 x 23 像素为单位）：

![在按钮上，使用和不透明颜色显示图形图像的外观](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703 15_GraphicalButtonSpacing")<br />在按钮上，使用和不透明颜色显示图形图像的外观

### <a name="hyperlinks"></a>超链接
超链接是非常适用于基于导航功能的操作，例如打开帮助主题、 模式对话框或向导。 如果命令使用超链接，则它应始终显示 ui 的可见和明显更改。 一般情况下，提交到操作 （例如，保存，取消，并删除） 的操作更好地传达使用一个按钮。

#### <a name="writing-style"></a>编写样式
请按照[用户界面文本的 Windows 桌面指南](/windows/desktop/uxguide/text-ui)。 不要使用"了解更多关于，""告诉我详细 about，"或"get-help 与此"表述。 相反，短语在回答的帮助内容的主要问题方面的帮助链接文本。 例如，"**如何将服务器添加到服务器资源管理器？** "

#### <a name="visual-style"></a>视觉样式

- 应始终使用超链接[The VSColor Service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。 如果超链接的样式设置不正确，它会闪烁红色活动时或在被访问后显示不同的颜色。

- 不包含下划线上停留状态，除非该链接是在完整句子中的句子片段等水印中的控件。

- 下划线不应出现的悬停。 相反，对链接处于活动状态的用户的反馈是轻微的颜色更改和相应的链接游标。

## <a name="BKMK_TreeViews"></a> 树视图

树视图提供了到父-子组列出了组织复杂的方法。 用户可以展开或折叠父组，以显示或隐藏基础子项目。 可以选择树视图中的每个项目，以提供进一步的操作。

### <a name="BKMK_TreeViewVisualStyle"></a> 树视图的视觉样式

#### <a name="expanders"></a>扩展器
使用 Windows 和 Visual Studio 的扩展器设计应符合树视图控件。 每个节点使用 expander 控件以显示或隐藏基础项。 使用扩展器控件的用户可能会遇到 Windows 和 Visual Studio 中的不同的树视图中提供一致性。

![正确： 使用 expander 控件的树视图节点的正确样式](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705 1_TreeViewCorrect")<br />使用 expander 控件的树视图节点的正确： 正确样式

![不正确： 树视图节点的不正确样式](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705 2_TreeViewIncorrect1")<br />不正确： 不正确样式的树视图节点

#### <a name="selection"></a>选择
在树视图中选择一个节点后，突出显示应扩展到整个树视图控件的宽度。 这有助于用户清楚地标识他们选择了哪个项。 选择颜色应反映当前的 Visual Studio 主题。

![正确： 突出显示所选节点的适用于的树视图控件的整个宽度。](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705 1_TreeViewCorrect")<br />正确： 突出显示所选节点的适用于的树视图控件的整个宽度。

![不正确： 突出显示所选节点不能容纳树视图控件的整个的宽度。](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705 3_TreeViewIncorrect2")<br />不正确： 突出显示所选节点不能容纳树视图控件的整个的宽度。

#### <a name="icons"></a>图标
如果它们帮助直观地确定项之间的差异，则仅应在树视图控件中使用图标。 一般情况下，应仅在异类列表中的图标的执行信息来区分类型的元素中使用的图标。 在同类列表程序使用图标经常被视为干扰，应当避免。 在这种情况下 （父级） 中的组图标可传达其中的项的类型。 此规则的例外就是如果图标是动态的用于指示状态。

#### <a name="scroll-bars"></a>滚动条
如果内容适合树视图控件中，应始终隐藏滚动条。 它是树的可接受的滚动条可滚动的窗口中处于隐藏或半透明和包含在树视图的窗口具有焦点时显示或鼠标悬停时视图自身中。

![因为内容已经超出了树视图控件的限制，会显示这两个垂直和水平滚动条。](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705 4_Scrollbars")<br />因为内容已经超出了树视图控件的限制，会显示这两个垂直和水平滚动条。

### <a name="BKMK_TreeViewInteractions"></a> 树视图交互

#### <a name="context-menus"></a>上下文菜单
树视图节点可以显示上下文菜单中的子菜单选项。 通常，当用户右键单击某个项或与选择的项的 Windows 键盘上按菜单键时出现此情况。 务必节点获得焦点并处于选中状态。 这有助于用户确定子菜单属于哪个项。

![选择已生成上下文菜单获得焦点，以通知用户哪些项的项。](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705 5_ContextMenu")<br />选择已生成上下文菜单获得焦点，以通知用户哪些项的项。

#### <a name="keyboard"></a>键盘
在树视图应提供选择项和展开/折叠节点使用键盘的能力。 这可确保导航满足我们的可访问性要求。

##### <a name="tree-view-control"></a>树视图控件
Visual Studio 树控件应遵循通用的键盘导航：

- **向上键：** 选择项目树中向上移动

- **向下箭头：** 选择通过树向下移动的项

- **向右箭头：** 展开树中的节点

- **向左的箭头：** 折叠树中的节点

- **输入密钥：** 启动、 加载和执行所选的项

##### <a name="trid-tree-view-and-grid-view"></a>Trid （树视图和网格视图）
Trid 控件是包含 grid 中的树视图的复杂控件。 展开、 折叠，和导航树应遵守相同的键盘命令为树视图中，添加以下内容：

- **向右箭头：** 展开的节点。 展开节点后，它应继续导航到在右侧最接近的列。 导航应停止的行的末尾。

- **选项卡上：** 导航到最接近的单元格右侧。  在行结束时，导航到下一行将继续。

- **Shift + 选项卡：** 导航到左侧的最接近的单元格。  在行的开头，导航到上一行中最右边的单元格将继续。

![在 Visual Studio 中的 trid 控件](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705 6_Trid")<br />在 Visual Studio 中的 trid 控件