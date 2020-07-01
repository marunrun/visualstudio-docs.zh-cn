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
ms.openlocfilehash: dd2b2723a5ecfe66e9471cfea1e8eb55ed7ced59
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547441"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio 的公共控件模式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="common-controls"></a><a name="BKMK_CommonControls"></a>公共控件

### <a name="overview"></a>概述
 公共控件构成了 Visual Studio 中的大部分用户界面。 Visual Studio 界面中使用的大多数常见控件应遵循[Windows 桌面交互指南](https://msdn.microsoft.com/library/windows/desktop/dn742399.aspx)。 本文档特定于 Visual Studio，涵盖了一些特殊情况或补充这些 Windows 准则的详细信息。

#### <a name="common-controls-in-this-topic"></a>本主题中的公共控件

- [条](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [输入字段](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [组合框和下拉列表](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [复选框](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [单选按钮](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [组框架](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [树视图](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>视觉样式
 在设置控件的样式时要考虑的第一件事是控件是否将在主题 UI 中使用。 标准 UI 中的控件是非主题 UI，并且必须遵循[正常的 Windows 桌面样式](https://msdn.microsoft.com/library/windows/desktop/dn742399\(v=vs.85\).aspx)，这意味着它们不会重新设置模板并且应显示在其默认控件外观中。

- **标准（实用工具）对话框：** 没有主题。 不要重新模板。 使用基本控件样式默认值。

- **工具窗口、文档编辑器、设计图面和主题对话框：** 使用颜色服务的专用主题外观。

### <a name="scrollbars"></a><a name="BKMK_Scrollbars"></a>条
 滚动条应遵循[Windows 滚动条的常见交互模式](https://msdn.microsoft.com/library/windows/desktop/bb787527\(v=vs.85\).aspx)，除非它们增加了内容信息（如代码编辑器中的）。

### <a name="input-fields"></a><a name="BKMK_InputFields"></a>输入字段
 对于典型的交互行为，请遵循[Windows 桌面的文本框指导原则](https://msdn.microsoft.com/library/windows/desktop/dn742442\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式

- 不应在实用工具对话框中为输入字段设计样式。 使用控件的内部基本样式。

- 主题输入字段只应在主题对话框和工具窗口中使用。

#### <a name="specialized-interactions"></a>专用交互

- 只读字段将具有灰色（禁用）背景，但默认为（活动）前景。

- 必填字段的其中应有 **\<Required>** 水印。 在极少数情况下，不应更改背景的颜色。

- 错误验证：请参阅[Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- 应调整输入字段的大小以适合内容，而不是适应显示窗口的宽度，也不是任意匹配长字段的长度，如路径。 长度可能表示用户对字段中允许的字符数的限制。

     ![不正确的输入字段控件宽度](../../extensibility/ux-guidelines/media/0707-01-incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")**不正确的输入字段长度：名称不太可能是这样的。**

     ![正确的输入字段控件宽度](../../extensibility/ux-guidelines/media/0707-02-correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")**正确输入字段长度：输入字段是预期内容的合理宽度。**

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a>组合框和下拉列表
 对于典型的交互行为，请遵循[适用于下拉列表和组合框的 Windows 桌面指导原则](https://msdn.microsoft.com/library/windows/desktop/dn742404\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式

- 在实用工具对话框中，不要重新模板控件。 使用控件的内部基本样式。

- 在主题 UI 中，组合框和下拉端遵循控件的标准主题。

#### <a name="layout"></a>Layout
 组合框和下拉端应调整大小以适应内容，而不是适应显示窗口的宽度，也不是任意匹配长字段的长度，如路径。

 ![下拉&#45;关闭布局不正确](../../extensibility/ux-guidelines/media/0707-03-incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")

 **下拉控件的字段长度不正确**

 ![更正 drop&#45;向下布局](../../extensibility/ux-guidelines/media/0707-04-correctdropdownlayout.png "0707-04_CorrectDropDownLayout")

 **下拉控件的正确字段长度**

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a>复选框
 对于典型的交互行为，请遵循[Windows 桌面的复选框指导原则](https://msdn.microsoft.com/library/windows/desktop/dn742401\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式

- 在实用工具对话框中，不要重新模板控件。 使用控件的内部基本样式。

- 在主题 UI 中，复选框遵循控件的标准主题。

#### <a name="specialized-interactions"></a>专用交互

- 与复选框的交互决不能弹出对话框或导航到其他区域。

- 将复选框与第一行文本的基线对齐。

     ![不正确的复选框对齐](../../extensibility/ux-guidelines/media/0707-05-incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")**不正确复选框对齐方式：复选框位于文本的中心。**

     ![正确的复选框对齐](../../extensibility/ux-guidelines/media/0707-06-correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")**正确复选框对齐方式：复选框与第一行文本的基线对齐。**

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a>单选按钮
 对于典型的交互行为，请遵循[适用于单选按钮的 Windows 桌面指导原则](https://msdn.microsoft.com/library/windows/desktop/dn742436\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式
 在实用工具对话框中，不对单选按钮进行样式。 使用控件的内部基本样式。

#### <a name="specialized-interactions"></a>专用交互
 不需要使用组框架来包围广播选项。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a>组框架
 对于典型的交互行为，请遵循[适用于组框架的 Windows 桌面指导原则](https://msdn.microsoft.com/library/windows/desktop/dn742405\(v=vs.85\).aspx)。

#### <a name="visual-style"></a>视觉样式
 在实用工具对话框中，不要将组框的样式。 使用控件的内部基本样式。

#### <a name="layout"></a>Layout

- 除非您需要在严格布局中维护组区分，否则不需要使用组框架来包围广播选项。

- 不要对单个控件使用组框。

- 有时使用水平规则而不是组帧容器是可接受的。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a>文本控件

### <a name="labels"></a>标签

#### <a name="active-label-state"></a>活动标签状态

##### <a name="utility-standard-dialogs"></a>实用工具（标准）对话框）

- 通常，请遵循适用于控件标签的 Windows 桌面指南。

- 在实用工具对话框中，标签应以非粗体显示在标准环境的字体和文本颜色中。 请参阅[Visual Studio 的字体和格式设置](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)。

- 省略号应始终跟随标签。

##### <a name="signature-themed-dialogs"></a>签名（主题）对话框）
 标签控件可能为粗体或浅灰色。

#### <a name="disabled-label-state"></a>禁用的标签状态
 标签应反映与其关联的控件的外观。 例如，如果禁用了关联控件，则标签应显示为灰色且处于禁用状态。 这通常由 OS 处理，无需任何特殊处理。

#### <a name="dynamic-labels"></a>动态标签
 动态标签根据当前所选内容进行更改。 请尽可能使用主/详细布局中的动态标签，以帮助用户了解显示的信息与特定的选择相关，而不是与一般信息相关。

 ![与动态内容一起使用的动态标签](../../extensibility/ux-guidelines/media/070702-01-dynamiclabel.png "070702-01_DynamicLabel")

 **用于动态内容的动态标签的示例**

#### <a name="instructional-text"></a>说明文本
 某些接口元素受益于说明文本，以帮助用户了解 UI 用途或指示要执行的操作。

- 说明文本在对话框顶部最常见，但可以出现在其他区域，以向复杂的控件分组指定说明。

- 说明文本是非交互式的，但可能包含指向帮助主题的超链接。

- 请慎用说明文本，仅在需要时使用。

##### <a name="formatting"></a>格式化
 说明文本应为环境字体、标准（非主题）控件文本。 请参阅[Visual Studio 的字体和格式设置](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)。

 有关编写说明文本的详细信息，请参阅[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)。

 ![说明文本格式设置](../../extensibility/ux-guidelines/media/070702-02-instructionaltextformatting.png "070702-02_InstructionalTextFormatting")

 **Visual Studio 对话框中的说明文本**

#### <a name="informational-text"></a>信息文本
 信息文本是向用户提供附加信息的文本。 它可以是静态或动态的，也可以用作通知。 它始终是只读的，但如果它对用户能够复制信息很有用，则应将动态文本放置在控件容器（如只读文本字段）中。

##### <a name="dynamic-context-specific-text"></a>动态（特定于上下文的）文本
 动态信息文本根据上下文（例如用户切换焦点时）更改。 动态内容通常（但不总是）与动态标签配对。

 ![动态信息文本](../../extensibility/ux-guidelines/media/070702-03-informationaldynamictext.png "070702-03_InformationalDynamicText")

 **动态信息文本随上下文的变化而变化。**

##### <a name="formatting"></a>格式化
 可以通过两种方法来显示只读文本字段：直接在 UI 图面上（请参见上文），也可以包含在另一个控件中（如组框架或文本框）。 无论情况如何都是正确的。 功能设计器负责确定如何显示只读信息。

 文本可以在只读文本框内。 这通常表示可以选择和复制内容，尽管不能对其进行编辑。

 ![仅读取&#45;字段的信息性文本格式](../../extensibility/ux-guidelines/media/070702-04-informationalformatting.png "070702-04_InformationalFormatting")

 **只读字段的信息性文本格式设置**

#### <a name="watermarks"></a>水印
 尽管措辞可能相同，水印和说明文本之间的区别在于，当控件/窗口不为空时，水印会替换为内容，并且说明文本将始终可见。

 当窗口或控件为空时，应使用水印。 它们指示填充区域时需要执行的操作，并且可能包括用于打开相关窗口（例如拖动源）的操作链接。

##### <a name="visual-style"></a>视觉样式

- 水印应在窗口中水平居中。

- 水印应居中对齐，而不是左对齐。

- 水印可以垂直居中或定位在区域的顶部附近。 如果位于区域顶部附近，则必须有足够的空间，以便水印突出。

- 使用 `Environment.GrayText` 颜色标记和标准环境字体。 超链接应使用标准超链接共享令牌： `Environment.PanelHyperlink` 、 `Environment.PanelHyperlinkHover` 、 `Environment.PanelHyperlinkPressed` 和 `Environment.PanelHyperlinkDisabled` 。

- 无法在背景上选择水印

- 如果可能，请在水印中包含链接，以帮助用户入门。

  ![设计器窗口中的水印文本](../../extensibility/ux-guidelines/media/070702-05-watermark1.png "070702-05_Watermark1")

  ![工具窗口中的水印文本](../../extensibility/ux-guidelines/media/070702-06-watermark2.png "070702-06_Watermark2")

  **Visual Studio 中水印文本的示例**

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a>按钮和超链接

### <a name="overview"></a>概述
 按钮和链接控件（超链接）应遵循有关使用情况、措辞、大小调整和间距的[超链接上的基本 Windows 桌面指南](https://msdn.microsoft.com/library/windows/desktop/dn742406\(v=vs.85\).aspx)。

### <a name="choosing-between-buttons-and-links"></a>在按钮和链接之间进行选择
 在传统上，按钮已用于操作，并且已保留用于导航的超链接。 按钮在所有情况下均可使用，但在 Visual Studio 中扩展了链接角色，以便在某些情况下，按钮和链接的可互换。

 何时使用命令按钮：

- 主要命令

- 显示用于收集输入或做出选择的窗口，即使它们是辅助命令

- 破坏性或不可逆操作

- 向导和页面流中的提交按钮

  避免工具窗口中的命令按钮，如果标签需要两个以上的单词，则为。 链接可以具有较长的标签。

  何时使用链接：

- 导航到另一个窗口、文档或网页

- 需要较长的标签或短句子来描述操作意图的情况

- 按钮会严重影响 UI 的空间，前提是该操作不是破坏性或不可逆

- 在存在多个命令的情况下取消强调辅助命令

#### <a name="examples"></a>示例
 ![后跟状态消息的信息栏命令链接](../../extensibility/ux-guidelines/media/070703-01-commandlinkinfobar.png "070703-01_CommandLinkInfobar")

 **状态消息后面的信息栏中使用的命令链接**

 ![CodeLens 弹出中使用的链接](../../extensibility/ux-guidelines/media/070703-02-linksincodelens.png "070703-02_LinksInCodeLens")

 **CodeLens 弹出中使用的链接**

 ![用作辅助命令的链接](../../extensibility/ux-guidelines/media/070703-03-linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")

 **用于辅助命令的链接，其中按钮会吸引太多的注意力**

### <a name="common-buttons"></a>常用按钮

#### <a name="text"></a>文本
 遵循[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)中的写作指导原则。

#### <a name="visual-style"></a>视觉样式

##### <a name="standard-dialogs"></a>标准对话框
 Visual Studio 中的大多数按钮将显示在标准对话框中，不应进行样式化。 它们应该反映操作系统所规定的按钮的标准外观。

##### <a name="themed"></a>主题
 在某些情况下，可能会在样式的 UI 中使用按钮，并且必须相应地对这些按钮进行样式。 有关主题控件的信息，请参阅[对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)。

### <a name="special-buttons"></a>特殊按钮

#### <a name="browse-buttons"></a>浏览 .。。 按钮
 **[浏览 ...]** 按钮在网格、对话框和工具窗口以及其他无模式 UI 元素中使用。 它们显示一个选取器，帮助用户在控件中填充值。 此按钮有两种变体： long 和 short。

 ![长 &#91;浏览 ... &#93; "按钮](../../extensibility/ux-guidelines/media/070703-04-browselong.gif "070703-04_BrowseLong")

 **长 [浏览 ...] 按钮**

 ![Short 省略号&#45;仅 &#91;浏览 ... &#93; "按钮](../../extensibility/ux-guidelines/media/070703-05-browseshort.gif "070703-05_BrowseShort")

 **仅省略号 short [...] 按钮**

 何时使用仅限省略号的短按钮：

- 如果对话框中有多个长 **[浏览 ...]** 按钮（例如多个字段允许浏览时），则为。 为每个使用简短的 **[...]** 按钮，以避免此情况下创建的混乱的访问密钥（&在同一对话框中**浏览**和**B&浏览**）。

- 在紧密型对话框中，或者当没有合理的位置来放置长按钮时。

- 如果按钮将显示在网格控件中，则为。

  按钮使用指南：

- 不要使用访问密钥。 若要使用键盘进行访问，用户必须从相邻的控件中进行 tab 键。 确保 tab 键顺序为 "任何浏览" 按钮紧接在它将填充的字段之后。 在第一个句点下面不要使用下划线。

- 将 "Microsoft Active Accessibility （MSAA）**名称**" 属性设置为 "**浏览 ...** " （包括省略号），以便屏幕阅读器将其读取为 "浏览" 而不是 "圆点即点" 或 "句点-句点"。 对于托管控件，这意味着设置**AccessibleName**属性。

- 请勿将省略号 **[...]** 按钮用于除浏览操作之外的任何内容。 例如，如果需要 **[New ...]** 按钮，但没有足够的空间用于文本，则需要重新设计对话框。

##### <a name="sizing-and-spacing"></a>大小调整和间距
 ![调整 &#91;浏览 ... &#93; 按钮](../../extensibility/ux-guidelines/media/070703-06-browsesizing.png "070703-06_BrowseSizing")

 **调整 [浏览 ...] 按钮大小**

 ![&#91;浏览 ... &#93; 按钮的间距](../../extensibility/ux-guidelines/media/070703-07-browsespacing.png "070703-07_BrowseSpacing")

 **间距 [浏览 ...] 按钮**

#### <a name="graphical-buttons"></a>图形按钮
 某些按钮应始终使用图形图像而不包含文本来节省空间，避免本地化问题。 它们通常用于字段选取器和其他可排序列表。

> [!NOTE]
> 用户必须按 tab 键进入这些按钮（没有访问密钥），因此请按合理的顺序进行设置。 将按钮的 "名称" 属性映射到所执行的操作，以便屏幕阅读器正确解释按钮操作。

|名称|映像|
|-|-|
|添加|![图形“添加”按钮](../../extensibility/ux-guidelines/media/070703-08-buttonadd.png "070703-08_ButtonAdd")|
|删除|![图形“删除”按钮](../../extensibility/ux-guidelines/media/070703-09-buttonremove.png "070703-09_ButtonRemove")|
|全部添加|![图形“全部添加”按钮](../../extensibility/ux-guidelines/media/070703-10-buttonaddall.png "070703-10_ButtonAddAll")|
|全部删除|![图形“全部删除”按钮](../../extensibility/ux-guidelines/media/070703-11-buttonremoveall.png "070703-11_ButtonRemoveAll")|
|“上移”|![图形“上移”按钮](../../extensibility/ux-guidelines/media/070703-12-buttonmoveup.png "070703-12_ButtonMoveUp")|
|“下移”|![图形“下移”按钮](../../extensibility/ux-guidelines/media/070703-13-buttonmovedown.png "070703-13_ButtonMoveDown")|
|删除|![图形“删除”按钮](../../extensibility/ux-guidelines/media/070703-14-buttondelete.png "070703-14_ButtonDelete")|

##### <a name="sizing-and-spacing"></a>大小调整和间距
 图形按钮的大小与 "**浏览 ...** " 按钮的短版本（26x23 像素）的大小相同：

 ![使用和不使用透明颜色显示的按钮](../../extensibility/ux-guidelines/media/070703-15-graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")

 **按钮上图形图像的外观，显示和不显示透明颜色**

### <a name="hyperlinks"></a>超链接
 超链接非常适合用于基于导航的操作，如打开帮助主题、模式对话框或向导。 如果某个命令使用超链接，则它应始终显示对 UI 的可见且明显的更改。 通常，使用按钮可以更好地传达提交给操作的操作（如 "保存"、"取消" 和 "删除"）。

#### <a name="writing-style"></a>写入样式
 按照[Windows 桌面指南](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)中的说明进行操作。 不要使用 "了解详细信息"、"告诉我详细信息" 或 "通过此短语获取帮助"。 短语会根据帮助内容所回答的主要问题来帮助链接文本。 例如，"**如何实现将服务器添加到服务器资源管理器？**"

#### <a name="visual-style"></a>视觉样式

- 超链接应始终使用[VSColor 服务](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。 如果超链接的样式不正确，则它会在活动时闪烁红色，或在访问后显示不同的颜色。

- 不要在控件的 "休眠" 状态中包含下划线，除非该链接是整个句子（例如水印）中的句子片段。

- 悬停时不应显示下划线。 相反，向用户发送的链接处于活动状态时，会有轻微的颜色更改和相应的链接光标。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a>树视图

### <a name="overview"></a>概述
 树视图提供了一种将复杂列表组织到父-子组中的方法。 用户可以展开或折叠父组以显示或隐藏基础项。 可以选择树视图中的每个项以提供进一步的操作。

 本主题介绍可接受的使用、适当的设计和树视图的功能。

#### <a name="in-this-topic"></a>本主题内容

- [视觉样式](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewVisualStyle)

- [交互](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewInteractions)

### <a name="visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a>视觉样式

#### <a name="expanders"></a>扩展器
 树视图控件应符合 Windows 和 Visual Studio 使用的扩展程序设计。 每个节点都使用扩展器控件来显示或隐藏基础项。 使用扩展器控件为可能遇到 Windows 和 Visual Studio 中的不同树视图的用户提供一致性。

 ![正确的树视图控件](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705-1_TreeViewCorrect")

 **正确：使用扩展器控件正确的树视图节点样式**

 ![不正确的树视图节点](../../extensibility/ux-guidelines/media/070705-2-treeviewincorrect1.png "070705-2_TreeViewIncorrect1")

 **错误：树视图节点的样式不正确**

#### <a name="selection"></a>选择
 如果在树视图中选择了节点，则突出显示应扩展到树视图控件的整个宽度。 这有助于用户清楚地识别他们所选的项。 选择颜色应反映当前的 Visual Studio 主题。

 ![正确的树视图控件](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705-1_TreeViewCorrect")

 **正确：所选节点的突出显示适合整个树视图控件的宽度。**

 ![不正确的树视图突出显示](../../extensibility/ux-guidelines/media/070705-3-treeviewincorrect2.png "070705-3_TreeViewIncorrect2")

 **错误：所选节点的突出显示不符合树视图控件的整个宽度。**

#### <a name="icons"></a>图标
 如果在树视图控件中有助于直观地标识项之间的差异，则应仅在树视图控件中使用图标。 通常，仅应在其图标携带信息以区分元素类型的异类列表中使用图标。 使用图标的同类列表中经常会出现干扰，应避免这样做。 在这种情况下，组图标（父）可以传达其中的项的类型。 此规则的例外情况是：图标是动态的，并用于指示状态。

#### <a name="scroll-bars"></a>滚动栏
 如果内容适合树视图控件，则应始终隐藏滚动条。 滚动条处于隐藏状态，或在可滚动窗口中处于半透明状态，并且在包含树视图的窗口具有焦点或悬停于树视图本身时出现。

 ![带滚动条的树视图](../../extensibility/ux-guidelines/media/070705-4-scrollbars.png "070705-4_Scrollbars")

 **将显示垂直滚动条和水平滚动条，因为内容超出了树视图控件的限制。**

### <a name="interactions"></a><a name="BKMK_TreeViewInteractions"></a>互动

#### <a name="context-menus"></a>上下文菜单
 树视图节点可以显示上下文菜单中的子菜单选项。 通常情况下，当用户右键单击某项，或在 Windows 键盘上按下菜单键时，会发生这种情况。 此节点必须获得焦点并处于选中状态，这一点很重要。 这可以帮助用户标识子菜单所属的项。

 ![所选树节点和上下文菜单](../../extensibility/ux-guidelines/media/070705-5-contextmenu.png "070705-5_ContextMenu")

 **生成上下文菜单的项获得焦点，以通知用户已选择了哪个项。**

#### <a name="keyboard"></a>键盘
 树视图应提供选择项和使用键盘展开/折叠节点的功能。 这可以确保导航满足我们的辅助功能要求。

##### <a name="tree-view-control"></a>树视图控件
 Visual Studio 树控件应遵循常见的键盘导航：

- **向上键：** 通过向上移动树选择项

- **下箭头：** 通过向下移动树来选择项

- **向右箭头：** 展开树中的节点

- **左箭头：** 折叠树中的节点

- **输入密钥：** 启动、加载、执行选定项

##### <a name="trid-tree-view-and-grid-view"></a>Trid （树视图和网格视图）
 Trid 控件是包含网格中的树视图的复杂控件。 展开、折叠和导航树应遵循与树视图相同的键盘命令，同时添加以下内容：

- **向右箭头：** 展开节点。 节点展开后，应继续导航到右侧最近的列。 导航应在行尾停止。

- **选项卡：** 导航到右侧最近的单元格。  在行的末尾，导航将继续到下一行。

- **Shift + Tab：** 导航到左侧最近的单元格。  在行的开头，导航将继续到上一行中最右边的单元格。

  ![Visual Studio 中的 Trid 控件](../../extensibility/ux-guidelines/media/070705-6-trid.png "070705-6_Trid")

  **Visual Studio 中的 trid 控件**
