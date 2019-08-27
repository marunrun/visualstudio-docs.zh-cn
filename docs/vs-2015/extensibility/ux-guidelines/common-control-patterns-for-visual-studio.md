---
title: 常见控件模式
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 246464baea7e07e4d97e3483b423d200cf2b960c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430037"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio 的常见控件模式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="BKMK_CommonControls"></a> 公共控件

### <a name="overview"></a>概述
 公共控件构成了大多数 Visual Studio 中的用户界面。 在 Visual Studio 界面中使用的最常见控件应遵循[Windows 桌面的交互指南](https://msdn.microsoft.com/library/windows/desktop/dn742399.aspx)。 本文档是特定于 Visual Studio，并介绍了特殊情形或扩充这些 Windows 准则的详细信息。

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
 设置控件的样式时要考虑的第一个操作是是否主题化 UI 中使用的控件。 标准用户界面中的控件为非主题 UI 并且必须遵循[普通的 Windows 桌面样式](https://msdn.microsoft.com/library/windows/desktop/dn742399\(v=vs.85\).aspx)，这意味着它们不是重新模板化，应会出现在其默认控件外观。

- **标准 （实用工具） 对话框：** 不主题化。 执行操作而不重新模板。 使用基本的控件样式的默认值。

- **工具窗口、 文档编辑器，设计图面和主题化的对话框：** 使用专用应用主题外观，可以使用颜色服务。

### <a name="BKMK_Scrollbars"></a> 滚动条
 滚动条应遵循[Windows 滚动条的常见交互模式](https://msdn.microsoft.com/library/windows/desktop/bb787527\(v=vs.85\).aspx)除非它们增加内容的信息，如代码编辑器中。

### <a name="BKMK_InputFields"></a> 输入的字段
 典型的交互行为，请按照[文本框中的 Windows 桌面准则](https://msdn.microsoft.com/library/windows/desktop/dn742442\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式

- 不是输入的字段实用程序对话框中设置样式。 使用该控件中的内部的基本样式。

- 主题化的输入的字段应仅用于主题化的对话框和工具窗口。

#### <a name="specialized-interactions"></a>专用的交互

- 只读字段将具有灰色 （禁用） 背景但 （活动） 的默认前景色。

- 所需的字段应有 **\<所需>** 一样中其水印。 不应更改除中极少数情况下的背景的颜色。

- 错误验证：请参阅[Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- 输入的字段，应调整以适应其内容，不适合在其中显示它们，在窗口的宽度也以任意匹配很长的字段，例如路径的长度。 长度可能会向用户指示的关于字段中允许多少个字符的限制。

     ![不正确的输入的字段控件宽度](../../extensibility/ux-guidelines/media/0707-01-incorrectinputfieldcontrol.png "0707年 01_IncorrectInputFieldControl") **不正确的输入的字段长度：不太可能的名称将是这么一段时间。**

     ![更正的输入的字段控件宽度](../../extensibility/ux-guidelines/media/0707-02-correctinputfieldcontrol.png "0707年 02_CorrectInputFieldControl") **更正输入字段长度：输入的字段是预期的内容的合理宽度。**

### <a name="BKMK_ComboBoxesAndDropDowns"></a> 组合框和下拉列表
 典型的交互行为，请按照[下拉列表和组合框的 Windows 桌面准则](https://msdn.microsoft.com/library/windows/desktop/dn742404\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式

- 实用程序对话框中执行操作而不重新模板控件。 使用该控件中的内部的基本样式。

- 在主题 UI 中，组合框和下拉列表按照标准主题的控件。

#### <a name="layout"></a>布局
 组合框和下拉列表确定应将其调整为适应内容，不适合在其中显示它们，在窗口的宽度也以任意匹配很长的字段，例如路径的长度。

 ![不正确放置&#45;下布局](../../extensibility/ux-guidelines/media/0707-03-incorrectdropdownlayout.png "0707年 03_IncorrectDropDownLayout")

 **下拉列表控件的不正确的字段长度**

 ![正确的拖放&#45;下布局](../../extensibility/ux-guidelines/media/0707-04-correctdropdownlayout.png "0707年 04_CorrectDropDownLayout")

 **下拉列表控件的正确的字段长度**

### <a name="BKMK_CheckBoxes"></a> 复选框
 典型的交互行为，请按照[复选框的 Windows 桌面准则](https://msdn.microsoft.com/library/windows/desktop/dn742401\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式

- 实用程序对话框中执行操作而不重新模板控件。 使用该控件中的内部的基本样式。

- 在主题 UI 中的复选框按照标准主题的控件。

#### <a name="specialized-interactions"></a>专用的交互

- 有一个复选框的交互必须永远不会弹出一个对话框，或导航到另一个区域。

- 使复选框与的第一行文本基线对齐。

     ![不正确的复选框对齐方式](../../extensibility/ux-guidelines/media/0707-05-incorrectcheckboxalign.png "0707年 05_IncorrectCheckBoxAlign") **不正确的复选框对齐方式：复选框的文本居中。**

     ![更正复选框对齐方式](../../extensibility/ux-guidelines/media/0707-06-correctcheckboxalign.png "0707年 06_CorrectCheckBoxAlign") **更正复选框对齐方式：复选框与文本的第一行基线对齐。**

### <a name="BKMK_RadioButtons"></a> 单选按钮
 典型的交互行为，请按照[单选按钮的 Windows 桌面准则](https://msdn.microsoft.com/library/windows/desktop/dn742436\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式
 实用程序对话框中执行操作样式的单选按钮。 使用该控件中的内部的基本样式。

#### <a name="specialized-interactions"></a>专用的交互
 不需要使用一个组框以便包含单选选项。

### <a name="BKMK_GroupFrames"></a> 组帧
 典型的交互行为，请按照[组帧的 Windows 桌面准则](https://msdn.microsoft.com/library/windows/desktop/dn742405\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式
 实用程序对话框中执行操作不样式组帧。 使用该控件中的内部的基本样式。

#### <a name="layout"></a>布局

- 不需要使用一个组框以便包含单选选项，除非您需要维护组紧密布局中的差异。

- 单个控件永远不会使用一个组框。

- 有时是可接受使用水平规则而不是组帧容器。

## <a name="BKMK_TextControls"></a> 文本控件

### <a name="labels"></a>标签

#### <a name="active-label-state"></a>活动标签状态

##### <a name="utility-standard-dialogs"></a>实用程序 （标准） 对话框）

- 一般情况下，按照控件标签的 Windows 桌面指导。

- 在实用工具对话框中，标签应显示非加粗，在标准环境字体和文本颜色。 请参阅[Visual Studio 的字体和格式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)。

- 省略号应始终遵循标签。

##### <a name="signature-themed-dialogs"></a>签名 （主题） 对话框）
 标签控件可能会变为粗体或浅灰色。

#### <a name="disabled-label-state"></a>禁用的标签状态
 标签应反映与之关联的控件的外观。 例如，如果关联的控件处于禁用状态，则标签应显示灰色且被禁用。 这通常由操作系统处理，并且需要任何特殊处理。

#### <a name="dynamic-labels"></a>动态标签
 基于当前所选内容的动态标签更改。 只要有可能，使用母版/详细信息为布局中动态标签以帮助用户了解所显示的信息是与所选特定和而不是一般信息。

 ![使用包含动态内容的动态标签](../../extensibility/ux-guidelines/media/070702-01-dynamiclabel.png "070702 01_DynamicLabel")

 **动态标签与动态内容一起使用的示例**

#### <a name="instructional-text"></a>说明文本
 某些界面元素受益于以帮助用户了解 UI 目的或以指示要采取的操作的说明文本。

- 说明文本顶部的对话框，最常见的是，但可以出现在其他区域提供的复杂控件分组的指令。

- 说明文本非交互式的但可能包含超链接的帮助主题。

- 使用说明文本，尽量少以及仅在需要时。

##### <a name="formatting"></a>格式化
 说明文本应环境字体的标准 （非主题） 的控件文本。 请参阅[Visual Studio 的字体和格式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)。

 有关编写说明文本的详细信息，请参阅[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)。

 ![说明文本格式设置](../../extensibility/ux-guidelines/media/070702-02-instructionaltextformatting.png "070702 02_InstructionalTextFormatting")

 **Visual Studio 对话框中的说明文本**

#### <a name="informational-text"></a>信息性文本
 信息性文本是可显示用户的其他信息的文本。 它可以是静态或动态的或用作通知。 始终是只读的但如果用户要复制的信息的功能非常有用，动态文本应该放在控件容器，如只读文本字段中。

##### <a name="dynamic-context-specific-text"></a>动态 （特定于上下文的） 文本
 根据上下文，如当用户切换焦点的动态信息文本更改。 通常，但不是总是与动态标签配对动态内容。

 ![动态信息文本](../../extensibility/ux-guidelines/media/070702-03-informationaldynamictext.png "070702 03_InformationalDynamicText")

 **具体取决于上下文的动态信息性文本更改。**

##### <a name="formatting"></a>格式化
 有两种方法来显示只读文本字段： 可以直接在 UI 上显示 （参阅上文） 或包含在另一个控件，例如组帧或文本框。 请正确无误根据具体情况。 负责功能设计器，以确定如何显示只读信息。

 文本可以是只读的文本框内。 这通常表示内容，可以选择并复制，但不能对其进行编辑。

 ![信息性文本格式读取&#45;仅字段](../../extensibility/ux-guidelines/media/070702-04-informationalformatting.png "070702 04_InformationalFormatting")

 **信息性文本格式设置为只读字段**

#### <a name="watermarks"></a>水印
 虽然用词可能相同，水印和说明文本之间的区别是，水印会用替换内容时控件/窗口不为空，并且始终会一直显示为说明文本。

 当窗口或控件为空时，应使用水印。 它们指示需要执行以填充区域的内容，并可能包含操作的链接可打开相关的窗口，如拖动源。

##### <a name="visual-style"></a>视觉样式

- 水印应在窗口中水平居中。

- 水印应为居中对齐，不是左对齐。

- 水印可能垂直居中或定位在区域的顶部附近。 如果位于区域的顶部附近，必须有足够的空间更高版本，以便突出显示水印。

- 使用`Environment.GrayText`颜色的令牌和标准环境字体。 超链接应使用标准的超链接共享令牌： `Environment.PanelHyperlink`， `Environment.PanelHyperlinkHover`， `Environment.PanelHyperlinkPressed`，和`Environment.PanelHyperlinkDisabled`。

- 水印不能选择背景上

- 如果可能，包括链接中的水印，以帮助用户入门。

  ![水印设计器窗口中的文本](../../extensibility/ux-guidelines/media/070702-05-watermark1.png "070702 05_Watermark1")

  ![水印文本工具窗口中的](../../extensibility/ux-guidelines/media/070702-06-watermark2.png "070702 06_Watermark2")

  **Visual Studio 中的水印文本的示例**

## <a name="BKMK_ButtonsAndHyperlinks"></a> 按钮和超链接

### <a name="overview"></a>概述
 按钮和链接控件 （的超链接） 应遵循[上的超链接的基本 Windows 桌面指南](https://msdn.microsoft.com/library/windows/desktop/dn742406\(v=vs.85\).aspx)的使用情况，措词、 调整大小，和间距。

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
 ![以下状态消息的信息栏命令链接](../../extensibility/ux-guidelines/media/070703-01-commandlinkinfobar.png "070703 01_CommandLinkInfobar")

 **使用以下状态消息的信息栏命令链接**

 ![使用 CodeLens 弹出窗口中的链接](../../extensibility/ux-guidelines/media/070703-02-linksincodelens.png "070703 02_LinksInCodeLens")

 **使用 CodeLens 弹出窗口中的链接**

 ![用作辅助命令链接](../../extensibility/ux-guidelines/media/070703-03-linksassecondarycommands.png "070703 03_LinksAsSecondaryCommands")

 **用于在辅助命令的按钮会吸引过多注意力的链接**

### <a name="common-buttons"></a>常见的按钮

#### <a name="text"></a>Text
 遵循中的写入准则[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)。

#### <a name="visual-style"></a>视觉样式

##### <a name="standard-dialogs"></a>标准对话框
 在 Visual Studio 中的大多数按钮将显示标准对话框中，并且不应设置样式。 规定的操作系统，它们应反映标准按钮的外观。

##### <a name="themed"></a>主题
 在某些情况下，可能带样式的用户界面中使用按钮，这些按钮必须适当地设置样式。 请参阅[对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)主题化控件上的信息。

### <a name="special-buttons"></a>特殊按钮

#### <a name="browse-buttons"></a>浏览... 按钮
 **[浏览...]** 按钮使用网格、 对话框和工具窗口和其他无模式的 UI 元素。 它们显示的选取器，可帮助用户填充到控件的值。 有两种变体，此按钮，长、 短。

 ![Long&#91;浏览...&#93;按钮](../../extensibility/ux-guidelines/media/070703-04-browselong.gif "070703 04_BrowseLong")

 **长 [浏览...] 按钮**

 ![简短的省略号&#45;仅&#91;浏览...&#93;按钮](../../extensibility/ux-guidelines/media/070703-05-browseshort.gif "070703 05_BrowseShort")

 **短仅省略号 [...] 按钮**

 何时使用仅限省略号的短按钮：

- 如果有多个长 **[浏览...]** 在对话框中，如当多个字段允许的浏览按钮。 使用短 **[...]** 为每个要避免这种情况下创建的令人困惑访问项的按钮 ( **& 浏览**并**B (&)** 相同对话框中)。

- 在紧密的对话框中，或没有合理的位置将很长的按钮。

- 如果该按钮将显示一个网格控件中。

  使用该按钮的准则：

- 不要使用访问密钥。 若要访问它使用键盘，用户必须按 tab 键从相邻的控件。 请确保 tab 键顺序，以便其将填充的字段后立即处于任何浏览按钮。 永远不会使用下面的第一个期间下划线。

- 设置 Microsoft Active Accessibility (MSAA)**名称**属性设置为**浏览...** （包括省略号） 这样的屏幕阅读器将读取它作为"浏览"并不是"圆点点点"或"期间期期间。" 对于托管控件，这意味着设置**AccessibleName**属性。

- 永远不会使用省略号 **[...]** 用于浏览操作以外的按钮。 例如，如果您需要 **[新建...]** 按钮，但没有足够的空间的文本，然后在对话框需要重新设计。

##### <a name="sizing-and-spacing"></a>调整大小和间距
 ![调整大小&#91;浏览...&#93;按钮](../../extensibility/ux-guidelines/media/070703-06-browsesizing.png "070703 06_BrowseSizing")

 **大小调整 [浏览...] 按钮**

 ![间距&#91;浏览...&#93;按钮](../../extensibility/ux-guidelines/media/070703-07-browsespacing.png "070703 07_BrowseSpacing")

 **间距 [浏览...] 按钮**

#### <a name="graphical-buttons"></a>图形按钮
 某些按钮应始终使用图形化的图像，并且永远不会包含文本以节省空间并避免本地化问题。 这些通常用于字段选取器和其他可排序的列表中。

> [!NOTE]
> 用户必须对这些按钮 （没有任何访问密钥） 选项卡上，因此将其放置在合理的顺序。 将按钮的 name 属性映射到以使屏幕读取器正确解释此按钮的操作所需的操作。

|||
|-|-|
|添加|![Graphical "Add" button](../../extensibility/ux-guidelines/media/070703-08-buttonadd.png "070703-08_ButtonAdd")|
|删除|![Graphical "Remove" button](../../extensibility/ux-guidelines/media/070703-09-buttonremove.png "070703-09_ButtonRemove")|
|全部添加|![图形"全部添加"按钮](../../extensibility/ux-guidelines/media/070703-10-buttonaddall.png "070703 10_ButtonAddAll")|
|删除所有|![Graphical "Remove All" button](../../extensibility/ux-guidelines/media/070703-11-buttonremoveall.png "070703-11_ButtonRemoveAll")|
|上移|![图形"上移"按钮](../../extensibility/ux-guidelines/media/070703-12-buttonmoveup.png "070703 12_ButtonMoveUp")|
|下移|![图形"下移"按钮](../../extensibility/ux-guidelines/media/070703-13-buttonmovedown.png "070703 13_ButtonMoveDown")|
|删除|![Graphical "Delete" button](../../extensibility/ux-guidelines/media/070703-14-buttondelete.png "070703-14_ButtonDelete")|

##### <a name="sizing-and-spacing"></a>调整大小和间距
 大小调整图形按钮简短版本的相同 **[浏览...]** 按钮 （26 x 23 像素为单位）：

 ![使用和不透明颜色显示的按钮](../../extensibility/ux-guidelines/media/070703-15-graphicalbuttonspacing.png "070703 15_GraphicalButtonSpacing")

 **在按钮上，使用和不透明颜色显示图形图像的外观**

### <a name="hyperlinks"></a>超链接
 超链接是很适合基于导航功能的操作，例如打开帮助主题、 模式对话框或向导。 如果命令使用超链接，则它应始终显示 ui 的可见和明显更改。 一般情况下，提交到的操作 （如取消，保存和删除） 的操作更好地传达使用一个按钮。

#### <a name="writing-style"></a>编写样式
 请按照[用户界面文本的 Windows 桌面指南](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)。 不要使用"了解更多关于，""告诉我详细 about，"或"get-help 与此"表述。 相反，短语在回答的帮助内容的主要问题方面的帮助链接文本。 例如，"**如何将服务器添加到服务器资源管理器？** "

#### <a name="visual-style"></a>视觉样式

- 应始终使用超链接[The VSColor Service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。 如果超链接的样式设置不正确，它会闪烁红色活动时或在被访问后显示不同的颜色。

- 不包括在停留状态，除非该链接是在完整句子中的句子片段如水印中的控件的下划线。

- 悬停时的情况下不应出现下划线。 相反，对链接处于活动状态的用户的反馈是轻微的颜色更改和相应的链接游标。

## <a name="BKMK_TreeViews"></a> 树视图

### <a name="overview"></a>概述
 树视图提供了到父-子组列出了组织复杂的方法。 用户可以展开或折叠父组，以显示或隐藏基础子项目。 可以选择树视图中的每个项目，以提供进一步的操作。

 本主题介绍可接受的使用、 正确设计和树视图的功能。

#### <a name="in-this-topic"></a>在本主题中

- [视觉样式](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewVisualStyle)

- [交互](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewInteractions)

### <a name="BKMK_TreeViewVisualStyle"></a> 视觉样式

#### <a name="expanders"></a>扩展器
 使用 Windows 和 Visual Studio 的扩展器设计应符合树视图控件。 每个节点使用 expander 控件以显示或隐藏基础项。 使用扩展器控件的用户可能会遇到 Windows 和 Visual Studio 中的不同的树视图中提供一致性。

 ![更正树视图控件](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705 1_TreeViewCorrect")

 **使用 expander 控件的树视图节点的正确： 正确样式**

 ![不正确的树视图节点](../../extensibility/ux-guidelines/media/070705-2-treeviewincorrect1.png "070705 2_TreeViewIncorrect1")

 **不正确： 不正确样式的树视图节点**

#### <a name="selection"></a>选择
 在树视图中选择一个节点后，突出显示应扩展到整个树视图控件的宽度。 这有助于用户清楚地标识他们选择了哪个项。 选择颜色应反映当前的 Visual Studio 主题。

 ![更正树视图控件](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705 1_TreeViewCorrect")

 **正确： 突出显示所选节点的适用于的树视图控件的整个宽度。**

 ![不正确的树视图突出显示](../../extensibility/ux-guidelines/media/070705-3-treeviewincorrect2.png "070705 3_TreeViewIncorrect2")

 **不正确： 突出显示所选节点的不符合树视图控件的整个的宽度。**

#### <a name="icons"></a>图标
 如果它们帮助直观地确定项之间的差异，则仅应在树视图控件中使用图标。 一般情况下，应仅在异类列表中的图标的执行信息来区分类型的元素中使用的图标。 在同类列表程序使用图标经常被视为干扰，应当避免。 在这种情况下 （父级） 中的组图标可传达其中的项的类型。 此规则的例外就是如果图标是动态的用于指示状态。

#### <a name="scroll-bars"></a>滚动条
 如果内容适合树视图控件中，应始终隐藏滚动条。 它是树的可接受的滚动条可滚动的窗口中处于隐藏或半透明和包含在树视图的窗口具有焦点时显示或鼠标悬停时视图自身中。

 ![树视图与滚动条](../../extensibility/ux-guidelines/media/070705-4-scrollbars.png "070705 4_Scrollbars")

 **因为内容已经超出了树视图控件的限制，会显示这两个垂直和水平滚动条。**

### <a name="BKMK_TreeViewInteractions"></a> 交互

#### <a name="context-menus"></a>上下文菜单
 树视图节点可以显示上下文菜单中的子菜单选项。 通常，当用户右键单击某个项或与选择的项的 Windows 键盘上按菜单键时出现此情况。 务必节点获得焦点并处于选中状态。 这有助于用户确定子菜单属于哪个项。

 ![选定的树节点和上下文菜单](../../extensibility/ux-guidelines/media/070705-5-contextmenu.png "070705 5_ContextMenu")

 **选择已生成上下文菜单获得焦点，以通知用户哪些项的项。**

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
 Trid 控件是一个复杂的控件，它包含 grid 中的树视图。 展开、 折叠，和导航树应遵守相同的键盘命令为树视图中，添加以下内容：

- **向右箭头：** 展开的节点。 展开节点后，它应继续导航到在右侧最接近的列。 导航应停止的行的末尾。

- **选项卡上：** 导航到最接近的单元格右侧。  在行结束时，导航到下一行将继续。

- **Shift + 选项卡：** 导航到左侧的最接近的单元格。  在行的开头，导航到上一行中最右边的单元格将继续。

  ![在 Visual Studio 中的 Trid 控件](../../extensibility/ux-guidelines/media/070705-6-trid.png "070705 6_Trid")

  **在 Visual Studio 中的 trid 控件**
