---
title: Visual Studio 的常见控件模式 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b0b5a1904c01f5688a00e45de7feed7ae326d9b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698717"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio 的公共控件模式
## <a name="common-controls"></a><a name="BKMK_CommonControls"></a> 公共控件

### <a name="overview"></a>概述
公共控件构成了 Visual Studio 中的大部分用户界面。 Visual Studio 界面中使用的大多数常见控件应遵循 [Windows 桌面交互指南](/windows/desktop/uxguide/controls)。 本主题专门针对 Visual Studio，涵盖了一些特殊情况或补充这些 Windows 准则的详细信息。

#### <a name="common-controls-in-this-topic"></a>本主题中的公共控件

- [滚动条](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [输入字段](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [组合框和下拉列表](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [复选框](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [单选按钮](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [组框架](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [树视图](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>视觉样式
在设置控件的样式时要考虑的第一件事是控件是否将在主题 UI 中使用。 标准 UI 中的控件是非主题 UI，并且必须遵循 [正常的 Windows 桌面样式](/windows/desktop/uxguide/controls)，这意味着它们不会重新设置模板并且应显示在其默认控件外观中。

- **标准 (实用程序) 对话框：** 没有主题。 不要重新模板。 使用基本控件样式默认值。

- **工具窗口、文档编辑器、设计图面和主题对话框：** 使用颜色服务的专用主题外观。

### <a name="scroll-bars"></a><a name="BKMK_Scrollbars"></a> 滚动条
 滚动条应遵循 [Windows 滚动条的常见交互模式](/windows/desktop/Controls/about-scroll-bars) ，除非它们增加了内容信息，如代码编辑器中所示。

### <a name="input-fields"></a><a name="BKMK_InputFields"></a> 输入字段
 对于典型的交互行为，请遵循 [Windows 桌面的文本框指导原则](/windows/desktop/uxguide/ctrl-text-boxes)。

#### <a name="visual-style"></a>视觉样式

- 输入字段不应在实用工具对话框中进行样式。 使用控件的内部基本样式。

- 主题输入字段只应在主题对话框和工具窗口中使用。

#### <a name="specialized-interactions"></a>专用交互

- 只读字段将 (禁用灰色) 背景，但默认 (活动) 前台。

- 必填字段的其中应有 **\<Required>** 水印。 在极少数情况下，不应更改背景的颜色。

- 错误验证：请参阅 [Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- 应调整输入字段的大小以适合内容，而不是适应显示窗口的宽度，也不是任意匹配长字段的长度（如路径）。 长度可能表示用户对字段中允许的字符数的限制。

     ![输入字段长度不正确：名称的长度不能太长。](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")<br />输入字段长度不正确：名称的长度不能太长。

     ![正确输入字段长度：输入字段是预期内容的合理宽度。](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")<br />正确输入字段长度：输入字段是预期内容的合理宽度。

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a> 组合框和下拉列表
对于典型的交互行为，请遵循 [适用于下拉列表和组合框的 Windows 桌面指导原则](/windows/desktop/uxguide/ctrl-drop)。

#### <a name="visual-style"></a>视觉样式

- 在实用工具对话框中，不要重新模板控件。 使用控件的内部基本样式。

- 在主题 UI 中，组合框和下拉端遵循控件的标准主题。

#### <a name="layout"></a>布局
组合框和下拉端应调整大小以适应内容，而不是适合显示这些内容的窗口的宽度，也不是任意匹配长字段的长度（如路径）。

![不正确：下拉宽度对于将显示的内容太长。](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")<br />不正确：下拉宽度对于将显示的内容太长。

![正确：下拉大小将调整为允许转换增长，但不会不必要地进行。](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707-04_CorrectDropDownLayout")<br />正确：下拉大小将调整为允许转换增长，但不会不必要地进行。

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a> 复选框
对于典型的交互行为，请遵循 [Windows 桌面的复选框指导原则](/windows/desktop/uxguide/ctrl-check-boxes)。

#### <a name="visual-style"></a>视觉样式

- 在实用工具对话框中，不要重新模板控件。 使用控件的内部基本样式。

- 在主题 UI 中，复选框遵循控件的标准主题。

#### <a name="specialized-interactions"></a>专用交互

- 与复选框的交互决不能弹出对话框或导航到其他区域。

- 将复选框与第一行文本的基线对齐。

     ![错误：该复选框位于文本的中心。](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")<br />错误：该复选框位于文本的中心。

     ![更正：复选框与文本的第一行对齐。](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")<br />更正：复选框与文本的第一行对齐。

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a> 单选按钮
对于典型的交互行为，请遵循 [适用于单选按钮的 Windows 桌面指导原则](/windows/desktop/uxguide/ctrl-radio-buttons)。

#### <a name="visual-style"></a>视觉样式
在实用工具对话框中，不对单选按钮进行样式。 使用控件的内部基本样式。

#### <a name="specialized-interactions"></a>专用交互
除非您需要在严格布局中维护组区分，否则不需要使用组框架来包围广播选项。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a> 组框架
对于典型的交互行为，请遵循 [适用于组框架的 Windows 桌面指导原则](/windows/desktop/uxguide/ctrl-group-boxes)。

#### <a name="visual-style"></a>视觉样式
在实用工具对话框中，不要将组框的样式。 使用控件的内部基本样式。

#### <a name="layout"></a>布局

- 除非您需要在严格布局中维护组区分，否则不需要使用组框架来包围广播选项。

- 不要对单个控件使用组框。

- 有时可以使用水平规则而不是组帧容器。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a> 文本控件

### <a name="static-text-fields"></a>静态文本字段

静态文本字段提供只读信息，用户不能选择。 避免将其用于用户可能想要复制到剪贴板的任何文本。 不过，只读静态文本可能会更改，以反映状态更改。 在下面的示例中，信息组下的 "输出名称" 静态文本会更改，以反映对其上方的根命名空间文本框所做的任何更改。

可以通过两种方式显示静态文本信息。

当没有分组冲突时，静态文本可以在没有任何包含任何内容的情况下，在对话框中单独使用。 决定是否确实需要额外的框。 例如，在组行所创建的节下显示目录路径，如下所示：

![文本控件中的静态文本信息](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "DisplayingStaticText.png")<br />文本控件中的静态文本信息

在其他分组区域存在并包含信息的对话框中，可以帮助您提高可读性，并可以隐藏或显示节 (如 **属性窗口** 的 "说明" 窗格中所示) 或者您希望与类似的 UI 保持一致，请将静态文本置于框中。 此分组框应为单一规则并带有 `ButtonShadow` 以下颜色：

![属性窗口中的静态文本](../../extensibility/ux-guidelines/media/PropertiesWindow.png "PropertiesWindow.png")<br />属性窗口中的静态文本

### <a name="read-only-text-box"></a>只读文本框

这样，用户就可以选择字段中的文本，但不能对其进行编辑。 这些文本框由使用填充的常用三维雕刻界定 `ButtonShadow` 。

当用户更改关联的控件（例如选中/取消选中复选框或选择/取消选择单选按钮）时，文本框可以变为处于活动状态的 (可编辑) 。 例如，在下面所示的 "**工具 &gt; 选项**" 页中，当 "**使用默认值**" 复选框处于未选中状态时，"**主页**" 文本框将变为活动状态。

![只读文本框，显示 "非活动" 和 "活动" 状态](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "ReadOnlyTextBox.png")<br />只读文本框，显示 "非活动" 和 "活动" 状态

### <a name="using-text-in-dialogs"></a>使用对话框中的文本

对话框中的文本的关键准则：

- Unthemed 对话框中的文本框、列表框和框架的标签以动词开头，在第一个单词上使用首字母大写，并以冒号结束。

    > 主题对话框中的文本控件遵循 [Windows 桌面 UX 准则](/windows/desktop/uxguide/top-violations) ，并且不接受结尾标点符号，帮助链接中的问号除外。

- 复选框和选项按钮的标签以动词开头，第一个单词的首字母大写，无结束标点。

- 按钮、菜单、菜单项和选项卡的标签在每个单词 (词首大写) 。

- 标签术语应该与其他对话框中类似的标签一致。

- 如果可能，请在文本进入开发人员之前编写或批准文本。

- 所有控件都应具有标签，但在特殊情况下，tab 键是足够的。
适当时使用 helper 文本。

### <a name="helper-text"></a>帮助器文本

包含在对话框中，可帮助用户了解对话的目的或指示要执行的操作。 只有在需要时才应使用帮助器文本，以免干扰简单对话框。 帮助程序文本的两种变体是对话框和水印。

关注帮助程序文本的常见位置，并在引入新区域时有选择地。 帮助程序文本的常见方案包括：

- 对话框中的帮助器文本，用于为如何与复杂对话框进行交互提供附加方向。

- 空工具窗口或对话框中的水印文本，用于说明内容不可见的原因。

- 说明窗格，如 **属性窗口**的底部。

- 空编辑器中的水印文本，用于说明用户开始使用的操作。

### <a name="dialog-helper-text"></a>对话框帮助程序文本

用户体验设计器可以帮助确定帮助器文本何时合适。 设计器可以定义帮助器文本显示的位置以及其常规内容。 用户帮助可以编写/编辑实际文本。

### <a name="watermarks"></a>水印

对话框受益于略有不同的水印原则。 因为对话框可能会像使用文本) 的多个 UI 元素（ (标签、提示文本、按钮和其他容器控件）显得繁忙，特别是当这些元素以黑色显示时，水印会在深灰色 (VSColor：) 中更好地突出 `ButtonShadow` 。 通常，水印在控件内出现，如列表框中有白色背景 (VSColor： `Window`) 。

- 文本以深灰色显示 (VSColor： `ButtonShadow`) 。 但是，如果水印出现在中等灰色或彩色的 (VSColor： `ButtonFace`) 背景上，并且有关于可读性的问题，请使用黑色文本 (VSColor： `WindowText`) 。

- 水印可以居中或靠左对齐。 进行对齐决策时应用标准设计规则。 无法在背景上选择水印。

![水印文本示例](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />水印文本示例

### <a name="context-specific-dynamic-text"></a>特定于上下文的 (动态) 文本

动态文本可以在对话框或无模式 UI 中使用以下两种方式之一：作为动态标签或动态内容。

- 动态标签：动态文本的常见用途是在说明面板中提供所选项目的详细信息，例如，在包含在右侧网格中显示的元素和属性列表的对话框中。 属性网格的标签可能是动态的，因此，当在左侧选择某项时，右侧的网格将显示该特定项的信息。

- 动态文本：在需要以这种方式显示特定信息而不是常规信息的情况下非常有用，但应小心不要过度利用。

如果希望用户能够复制信息，则动态文本应位于只读文本字段中。

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a> 按钮和超链接

### <a name="overview"></a>概述
 (超链接) 的按钮和链接控件应遵循有关使用情况、措辞、大小调整和间距的 [超链接上的基本 Windows 桌面指南](/windows/desktop/uxguide/ctrl-links) 。

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
![状态消息后面的信息栏中使用的命令链接](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703-01_CommandLinkInfobar")<br />状态消息后面的信息栏中使用的命令链接

![CodeLens 弹出中使用的链接](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703-02_LinksInCodeLens")<br />CodeLens 弹出中使用的链接

![用于辅助命令的链接，其中按钮会吸引太多的注意力](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")<br />用于辅助命令的链接，其中按钮会吸引太多的注意力

### <a name="common-buttons"></a>常用按钮

#### <a name="text"></a>文本
遵循 [UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)中的写作指导原则。

#### <a name="visual-style"></a>视觉样式

##### <a name="standard-unthemed"></a>标准 (unthemed) 
Visual Studio 中的大多数按钮将出现在实用工具对话框中，不应进行样式化。 它们应该反映操作系统所规定的按钮的标准外观。

##### <a name="themed"></a>主题
在某些情况下，可能会在样式的 UI 中使用按钮，并且必须相应地对这些按钮进行样式。 有关主题控件的信息，请参阅 [对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) 。

### <a name="special-buttons"></a>特殊按钮

#### <a name="browse-buttons"></a>浏览 .。。按钮
**[浏览 ...]** 按钮在网格、对话框和工具窗口以及其他无模式 UI 元素中使用。 它们显示一个选取器，帮助用户在控件中填充值。 此按钮有两种变体： long 和 short。

![长 [浏览 ...] 按钮](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703-04_BrowseLong")<br />长 [浏览 ...] 按钮

![仅省略号 short [...] 按钮](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703-05_BrowseShort")<br />仅省略号 short [...] 按钮

何时使用仅限省略号的短按钮：

- 如果对话框中有多个长 **[浏览 ...]** 按钮（例如多个字段允许浏览时），则为。 请为每个使用简短的 **[...]** 按钮，以避免此情况下所创建的混乱的访问密钥 (**&浏览** 和 **B&** 同一对话框) 中的浏览。

- 在紧密型对话框中，或者当没有合理的位置来放置长按钮时。

- 如果按钮将显示在网格控件中，则为。

按钮使用指南：

- 不要使用访问密钥。 若要使用键盘进行访问，用户必须从相邻的控件中进行 tab 键。 确保 tab 键顺序为 "任何浏览" 按钮紧接在它将填充的字段之后。 在第一个句点下面不要使用下划线。

- 将 "Microsoft Active Accessibility (MSAA) **名称** " 属性设置为 " **浏览 ...** (包括省略号) ，以便屏幕阅读器将其读取为" 浏览 "而不是" 句点-句点 "或" 句点-句点 "。 对于托管控件，这意味着设置 **AccessibleName** 属性。

- 请勿将省略号 **[...]** 按钮用于除浏览操作之外的任何内容。 例如，如果需要 **[New ...]** 按钮，但没有足够的空间用于文本，则需要重新设计对话框。

##### <a name="sizing-and-spacing"></a>大小调整和间距
![调整大小 [浏览 ...] 按钮：标准版本为75x23 像素，短版本为26x23 像素](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703-06_BrowseSizing")<br />调整[浏览...]按钮大小

![间距 [浏览 ...] 按钮：相关控件和标准浏览按钮之间的间距7像素，相关控件和简短浏览按钮之间的间距5像素](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703-07_BrowseSpacing")<br />设置[浏览...]按钮间距

#### <a name="graphical-buttons"></a>图形按钮
某些按钮应始终使用图形图像而不包含文本来节省空间，避免本地化问题。 它们通常用于字段选取器和其他可排序列表。

> [!NOTE]
> 用户必须按 tab 键进入这些按钮 (没有) 的访问密钥，因此应将其设置为明智的顺序。 将 `name` 按钮的属性映射到它所采取的操作，以便屏幕阅读器正确解释按钮操作。

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
调整图形按钮的大小与 " **浏览 ...** " 按钮的简短版本相同 (26x23 像素) ：

![按钮上图形图像的外观，显示和不显示透明颜色](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")<br />按钮上图形图像的外观，显示和不显示透明颜色

### <a name="hyperlinks"></a>超链接
超链接非常适合用于基于导航的操作，如打开帮助主题、模式对话框或向导。 如果某个命令使用超链接，则它应始终显示对 UI 的可见且明显的更改。 通常，使用按钮可以更好地使用提交到操作 (如保存、取消和删除) 的操作。

#### <a name="writing-style"></a>写入样式
按照 [Windows 桌面指南](/windows/desktop/uxguide/text-ui)中的说明进行操作。 不要使用 "了解详细信息"、"告诉我详细信息" 或 "通过此短语获取帮助"。 短语会根据帮助内容所回答的主要问题来帮助链接文本。 例如，"**如何实现将服务器添加到服务器资源管理器？**"

#### <a name="visual-style"></a>视觉样式

- 超链接应始终使用 [VSColor 服务](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。 如果超链接的样式不正确，则它会在活动时闪烁红色，或在访问后显示不同的颜色。

- 不要在控件的 "静止" 状态下包含下划线，除非该链接是整个句子中的句子片段（如水印）。

- 悬停时不应出现下划线。 相反，向用户发送的链接处于活动状态时，会有轻微的颜色更改和相应的链接光标。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a> 树视图

树视图提供了一种将复杂列表组织到父-子组中的方法。 用户可以展开或折叠父组以显示或隐藏基础项。 可以选择树视图中的每个项以提供进一步的操作。

### <a name="tree-view-visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a> 树视图视觉样式

#### <a name="expanders"></a>扩展器
树视图控件应符合 Windows 和 Visual Studio 使用的扩展程序设计。 每个节点都使用扩展器控件来显示或隐藏基础项。 使用扩展器控件为可能遇到 Windows 和 Visual Studio 中的不同树视图的用户提供一致性。

![正确：使用扩展器控件正确的树视图节点样式](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正确：使用扩展器控件正确的树视图节点样式

![错误：树视图节点的样式不正确](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705-2_TreeViewIncorrect1")<br />错误：树视图节点的样式不正确

#### <a name="selection"></a>选择
如果在树视图中选择了节点，则突出显示应扩展到树视图控件的整个宽度。 这有助于用户清楚地识别他们所选的项。 选择颜色应反映当前的 Visual Studio 主题。

![正确：所选节点的突出显示适合整个树视图控件的宽度。](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正确：所选节点的突出显示适合整个树视图控件的宽度。

![错误：所选节点的突出显示不符合树视图控件的整个宽度。](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705-3_TreeViewIncorrect2")<br />错误：所选节点的突出显示不符合树视图控件的整个宽度。

#### <a name="icons"></a>图标
如果在树视图控件中有助于直观地标识项之间的差异，则应仅在树视图控件中使用图标。 通常，仅应在其图标携带信息以区分元素类型的异类列表中使用图标。 使用图标的同类列表中经常会出现干扰，应避免这样做。 在这种情况下，组图标 (父) 可以传达其中的项的类型。 此规则的例外情况是：图标是动态的，并用于指示状态。

#### <a name="scroll-bars"></a>滚动栏
如果内容适合树视图控件，则应始终隐藏滚动条。 滚动条处于隐藏状态，或在可滚动窗口中处于半透明状态，并且在包含树视图的窗口具有焦点或悬停于树视图本身时出现。

![将显示垂直滚动条和水平滚动条，因为内容超出了树视图控件的限制。](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705-4_Scrollbars")<br />将显示垂直滚动条和水平滚动条，因为内容超出了树视图控件的限制。

### <a name="tree-view-interactions"></a><a name="BKMK_TreeViewInteractions"></a> 树视图交互

#### <a name="context-menus"></a>上下文菜单
树视图节点可以显示上下文菜单中的子菜单选项。 通常情况下，当用户右键单击某项，或在 Windows 键盘上按下菜单键时，会发生这种情况。 此节点必须获得焦点并处于选中状态，这一点很重要。 这可以帮助用户标识子菜单所属的项。

![生成上下文菜单的项获得焦点，以通知用户已选择了哪个项。](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705-5_ContextMenu")<br />生成上下文菜单的项获得焦点，以通知用户已选择了哪个项。

#### <a name="keyboard"></a>Keyboard
树视图应提供选择项和使用键盘展开/折叠节点的功能。 这可以确保导航满足我们的辅助功能要求。

##### <a name="tree-view-control"></a>树视图控件
Visual Studio 树控件应遵循常见的键盘导航：

- **向上键：** 通过向上移动树选择项

- **下箭头：** 通过向下移动树来选择项

- **向右箭头：** 展开树中的节点

- **左箭头：** 折叠树中的节点

- **输入密钥：** 启动、加载、执行选定项

##### <a name="trid-tree-view-and-grid-view"></a>Trid (树视图和网格视图) 
Trid 控件是包含网格中的树视图的复杂控件。 展开、折叠和导航树应遵循与树视图相同的键盘命令，同时添加以下内容：

- **向右箭头：** 展开节点。 节点展开后，应继续导航到右侧最近的列。 导航应在行尾停止。

- **选项卡：** 导航到右侧最近的单元格。  在行的末尾，导航将继续到下一行。

- **Shift + Tab：** 导航到左侧最近的单元格。  在行的开头，导航将继续到上一行中最右边的单元格。

![Visual Studio 中的 trid 控件](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705-6_Trid")<br />Visual Studio 中的 trid 控件
