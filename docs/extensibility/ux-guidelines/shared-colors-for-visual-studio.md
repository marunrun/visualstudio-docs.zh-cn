---
title: Visual Studio 的共享颜色 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3e31e5d9c3d1dc284694bd2db2a9f37d863462ad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699934"
---
# <a name="shared-colors-for-visual-studio"></a>Visual Studio 的共享颜色
设计使用常见 Visual Studio shell 元素的 UI，或者希望 interface 元素与类似功能一致时，可使用包定义文件中的现有标记名称来选择和分配颜色。 这可确保 UI 与整体 Visual Studio 环境保持一致，并确保它在添加或更新主题时自动更新。

本文介绍公共 UI 元素以及它们使用的标记名称（可以在构建类似 UI 时引用这些名称）。 有关如何访问这些颜色标记的特定信息，请参见 [The VSColor Service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。

请确保正确使用标记名称：

- **使用基于功能的标记名称，而不是颜色本身。** 公共共享颜色与特定界面元素关联，仅用于相同或类似功能。 例如，不要仅仅因为你喜欢某个已按下组合框的颜色，便将该颜色重复用于旋转进度动画。 组合框和动画的功能不同，如果与组合框关联的颜色更改，则它可能不再是适合于动画元素的颜色。 以一致方法使用颜色可帮助使用户适应，防止产生混乱。

- **采用正确组合使用背景和文本颜色。** 要用于文本的背景色具有关联文本颜色。 不要使用为该背景指定的颜色之外的文本颜色。 如果没有关联的文本颜色，请勿将该背景色用于要在其上显示文本的任何图面。 文本和背景色的其他组合可能会导致不可读的界面。

- **使用适合于其位置的控件颜色。** 在某些状态下，某些 Visual Studio 控件没有单独的边框和背景色。 而是从它们之后的图面选取这些颜色。 请确保始终使用适合于要在其中放置控件的位置的标记名称。

> [!IMPORTANT]
> 请勿使用在 "起始页" 或 "Cider" 类别中找到的标记。

## <a name="common-shared-controls"></a>公共共享控件

在功能中使用标准 Visual Studio 命令栏时，你将可以访问带样式的 shell 控件。 不应重新将这些公共控件模板。 但是，如果需要构建自定义命令栏，则可能还需要构建自定义控件。 在这种情况下，请确保对以下每个控件使用正常标记名称，以便 UI 与 Visual Studio 的其余部分保持一致。

### <a name="button-controls"></a>按钮控件

![按钮控件红线](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303-155_ButtonControlRedline")

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于要与 Visual Studio 主题集成的文档中的按钮， (轻型、深色、蓝色或系统高对比度主题) 。 | ...对于将针对不属于 Visual Studio 主题一部分的自定义背景显示的按钮。 |

**按钮：标准状态**

![标准按钮](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03")<br />标准按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| Button | `CommonControls.Button` |
| 按钮边框 | `CommonControls.ButtonBorder` |

**Button：默认状态**

![默认按钮](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03")<br />默认按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonDefault` |
| 按钮边框 | `CommonControls.ButtonBorderDefault` |

**按钮：已禁用状态**

![禁用的按钮](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03 已禁用")<br />禁用的按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonDisabled` |
| 按钮边框 | `CommonControls.ButtonBorderDisabled` |

**Button：悬停状态**

![悬停时的按钮](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03 悬停")<br />悬停时的按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonHover` |
| 按钮边框 | `CommonControls.ButtonBorderHover` |

**按钮：按下状态**

![按下按钮](../../extensibility/ux-guidelines/media/03.03.Button.Pressed.png "03.03")<br />按下按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonPressed` |
| 按钮边框 | `CommonControls.ButtonBorderPressed` |

**按钮：聚焦状态**

![焦点按钮](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03")<br />焦点按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonFocused` |
| 按钮边框 | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>复选框控件
![ (红线) 的复选框 ](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303-161_CheckboxRedline")<br /> (红线) 的复选框

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于文档中包含的复选框控件。 | ...对于不是复选框控件的任何 UI。 |

**复选框：默认状态**

![复选框](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303-162_Checkbox")<br />默认复选框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackground` |
| 边框 | `CommonControls.CheckBoxBorder` |
| 文本 | `CommonControls.CheckBoxText` |
| 标志符号 | `CommonControls.CheckBoxGlyph` |

**复选框：禁用状态**

![禁用复选框](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303-163_CheckboxDisabled")<br />禁用复选框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundDisabled` |
| 边框 | `CommonControls.CheckBoxBorderDisabled` |
| 文本 | `CommonControls.CheckBoxTextDisabled` |
| 标志符号 | `CommonControls.CheckBoxGlyphDisabled` |

**复选框：悬停状态**

 ![悬停时的复选框](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303-164_CheckboxHover")<br />悬停时的复选框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundHover` |
| 边框 | `CommonControls.CheckBoxBorderHover` |
| 文本 | `CommonControls.CheckBoxTextHover` |
| 标志符号 | `CommonControls.CheckBoxGlyphHover` |

**复选框：按下状态**

![按下复选框](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303-165_CheckboxPressed")<br />按下复选框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundPressed` |
| 边框 | `CommonControls.CheckBoxBorderPressed` |
| 文本 | `CommonControls.CheckBoxTextPressed` |
| 标志符号 | `CommonControls.CheckBoxGlyphPressed` |

**复选框：焦点状态**

![重点复选框](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303-166_CheckboxFocused")<br />重点复选框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundFocused` |
| 边框 | `CommonControls.CheckBoxBorderFocused` |
| 文本 | `CommonControls.CheckBoxTextFocused` |
| 标志符号 | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>下拉框和组合框
![下拉/组合框 (红线) ](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")<br />下拉/组合框 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于文档中的下拉框和组合框。 | ...对于不是下拉框或组合框的任何 UI。 |
| | ...对于命令栏[下拉](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)[框或组合框](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)。 |

**下拉框和组合框：默认状态**

![默认下拉/组合框](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303-168_DropDownComboBox")<br />默认下拉/组合框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackground` |
| 边框 | `CommonControls.ComboBoxBorder` |
| 文本 | `CommonControls.ComboBoxText` |
| Separator | `CommonControls.ComboBoxSeparator` |
| 标志符号 | `CommonControls.ComboBoxGlyph` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackground` |

**下拉框和组合框：禁用状态**

![禁用的下拉/组合框](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")<br />禁用的下拉/组合框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundDisabled` |
| 边框 | `CommonControls.ComboBoxBorderDisabled` |
| 文本 | `CommonControls.ComboBoxTextDisabled` |
| Separator | `CommonControls.ComboBoxSeparatorDisabled` |
| 标志符号 | `CommonControls.ComboBoxGlyphDisabled` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**下拉框和组合框：悬停状态**

![悬停时的下拉/组合框](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")<br />悬停时的下拉/组合框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundHover` |
| 边框 | `CommonControls.ComboBoxBorderHover` |
| 文本 | `CommonControls.ComboBoxTextHover` |
| Separator | `CommonControls.ComboBoxSeparatorHover` |
| 标志符号 | `CommonControls.ComboBoxGlyphHover` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundHover` |

**下拉框和组合框：按下状态**

![按下的下拉/组合框](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")<br />按下的下拉/组合框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundPressed` |
| 边框 | `CommonControls.ComboBoxBorderPressed` |
| 文本 | `CommonControls.ComboBoxTextPressed` |
| Separator | `CommonControls.ComboBoxSeparatorPressed` |
| 标志符号 | `CommonControls.ComboBoxGlyphPressed` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**下拉列表和组合框列表项视图：按下状态**

 ![下拉/组合框按下列表项视图](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")<br />下拉/组合框按下列表项视图

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| 边框 | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| 项文本 | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| 背景阴影 | `CommonControls.ComboBoxListBackgroundShadow` |

**下拉框和组合框：焦点状态**

![具有焦点的下拉/组合框](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")<br />具有焦点的下拉/组合框

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundFocused` |
| 边框 | `CommonControls.ComboBoxBorderFocused` |
| 文本 | `CommonControls.ComboBoxTextFocused` |
| Separator | `CommonControls.ComboBoxSeparatorFocused` |
| 标志符号 | `CommonControls.ComboBoxGlyphFocused` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**下拉框和组合框：文本输入选择**

![下拉/组合框文本输入选择](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")<br />下拉/组合框文本输入选择

| 元素 | 标记名称：Category.color |
| --- | --- |
| 突出显示 | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>表格数据（网格）控件
表格数据控件（也称为网格控件）是可以用于在多列中呈现大量数据的 Visual Studio 公共控件。 可以在 Visual Studio 中的多个位置中找到标准表格数据控件：错误列表工具窗口、IntelliTrace 报告和内存堆视图及其他位置。 始终使用提供的标准表格数据控件。 在某些极少数情况下，你可能无法访问标准表格数据控件。 在这些情况下，请使用以下标记名称以确保 UI 与 Visual Studio 中的其他表格数据控件保持一致。

![表格数据/网格控件 (红线) ](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")<br />表格数据/网格控件 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于表格或网格控件。 | ...对于不是表格或网格控件的任何 UI。 |

#### <a name="column-headers"></a>列标题
列标题由背景、边框、标题文本和可选标志符号（通常在网格按该列进行排序时使用）组成。

**列标题：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Header.Default` |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（标志符号） | `Header.Glyph` |
| 边框 | `Header.SeparatorLine` |

**列标题：悬停状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Header.MouseOver` |
| 前景（文本） | `Environment.CommandBarTextHover` |
| 前景（标志符号） | `Header.MouseOverGlyph` |
| 边框 | `Header.SeparatorLine` |

**列标题：按下状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundPressed` |
| 前景（文本） | `CommonControls.CheckBoxBorderPressed` |
| 前景（标志符号） | `CommonControls.CheckBoxTextPressed` |
| 边框 | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>列表视图项
 列表视图项由背景和内容组成。 内容可以是文本、图标或两者。

**列表视图项：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 透明 |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 边框 | 无 |

**列表视图项：活动状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive` |
| 前景（文本） | `TreeView.SelectedItemActiveText` |
| 边框 | 无 |

**列表视图项：非活动状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive` |
| 前景（文本） | `TreeView.SelectedItemInactiveText` |
| 边框 | 无 |

### <a name="ui-text"></a>UI 文本

#### <a name="instructional-text"></a>说明文本
说明文本简要说明了如何在对话框或文档页中执行的操作。

![默认说明文本](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />默认说明文本

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>辅助说明文本
在包含大量文本和控件的文档页面中，某些说明文本将使用不同的颜色值。 这有助于传达最重要的信息并减小 UI 元素的总体密度。  (另请参阅下面有关提示文本的部分。 ) 

![辅助说明文本](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />辅助说明文本

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>提示文本
提示文本显示在空控件中、控件下方或空文档图面上，以向用户显示下一步操作。 可以通过窗口或控件背景使用提示文本。

**默认提示文本**

![默认提示文本](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />默认提示文本

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Environment.ControlEditHintText` |

**必需的提示文本**

![必需的提示文本](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />必需的提示文本

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Environment.ControlRequiredHintText` |
| 背景 | `Environment.ControlRequiredBackground` |

**搜索框控件文本**

> 查看与搜索控件相关的其他颜色标记的 [搜索框](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes) 。

![搜索框控件文本](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />搜索框控件文本

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>Hyperlink
超链接是一个没有前景/背景对的控件。 在所有情况下，都使用前景超链接颜色，它会在深色、灰色和白色背景上正确显示。 如果不使用超链接控件的颜色标记，则会看到 "已按下" 的默认系统颜色，它会以红色闪烁。 这就是控件未使用正确环境颜色标记的信号。

![Hyperlink (红线) ](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303-133_HyperlinkRedline")<br />Hyperlink (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...需要创建自定义超链接时。 | ...对于不是超链接的任何内容。 |

**Hyperlink：默认状态**

![默认超链接](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303-134_Hyperlink")<br />默认超链接

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlink` |

**Hyperlink：悬停状态**

![悬停时的超链接](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303-135_HyperlinkHover")<br />悬停时的超链接

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlinkHover` |

**Hyperlink：按下状态**

![按下超链接](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303-136_HyperlinkPressed")<br />按下超链接

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlinkPressed` |

**超链接：已禁用状态**

![禁用的超链接](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303-137_HyperlinkDisabled")<br />禁用的超链接

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>信息栏
信息栏用于提供有关给定上下文的详细信息，始终出现在文档窗口或工具窗口顶部。

![红线)  (信息栏 ](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303-138_InfobarRedline")<br />红线)  (信息栏

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...创建自定义信息栏时。 | ...对于与信息栏不相似的 UI 元素。 |

**信息栏：默认状态**

![默认信息栏](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303-139_Infobar")<br />默认信息栏

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.InfoBarBackground` |
| 前景（文本） | `InfoBar.InfoBar` |
| 边框 | `InfoBar.InfoBarBorder` |

**信息栏关闭 (&times;) 按钮：默认状态**

![默认信息栏关闭 (&times;) "按钮](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />默认信息栏关闭 (&times;) "按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.CloseButton` |
| 边框 | `InfoBar.CloseButtonBorder` |
| 标志符号 | `InfoBar.CloseButtonGlyph` |

**信息栏关闭 (&times;) 按钮：悬停状态**

![&times;悬停时的 "信息栏关闭" () 按钮](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />&times;悬停时的 "信息栏关闭" () 按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.CloseButtonHover` |
| 边框 | `InfoBar.CloseButtonHoverBorder` |
| 标志符号 | `InfoBar.CloseButtonHoverGlyph` |

**信息栏关闭 (&times;) 按钮：按下状态**

![按下了信息栏关闭 (&times;) "按钮](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />按下了信息栏关闭 (&times;) "按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.CloseButtonDown` |
| 边框 | `InfoBar.CloseButtonDownBorder` |
| 标志符号 | `InfoBar.CloseButtonDownGlyph` |

**信息栏超链接按钮：默认状态**

![默认信息栏超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />默认信息栏超链接按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `InfoBar.Hyperlink` |

**信息栏超链接按钮：悬停状态**

![悬停时的 "信息" 超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />悬停时的 "信息" 超链接按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Infobar.HyperlinkMouseOver`<br />带下划线的 ()  |

**信息栏超链接按钮：按下状态**

![按下信息链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />按下信息链接按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Infobar.HyperlinkMouseDown`<br />带下划线的 ()  |

** () 句子中的信息栏内联超链接：默认状态**

![默认内联信息栏超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />默认内联信息栏超链接按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `InfoBar.Hyperlink` |

** (句子中的信息栏内联超链接) ：悬停状态**

![悬停时的 "信息栏" 内联超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />悬停时的 "信息栏" 内联超链接按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Infobar.HyperlinkMouseOver`<br />带下划线的 ()  |

** (中的信息栏内联超链接) ：按下状态**

![按下信息栏内联超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />按下信息栏内联超链接按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景 (文本)  | `Infobar.HyperlinkMouseDown`<br />带下划线的 ()  |

**"信息栏" 按钮：默认状态**

![默认信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />默认信息栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.Button` |
| 前景 (文本)  | `InfoBar.Button` |
| 边框 | `InfoBar.ButtonBorder` |

**信息栏按钮：悬停状态**

![悬停时的 "信息栏" 按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />悬停时的 "信息栏" 按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonMouseOver` |
| 前景 (文本)  | `InfoBar.ButtonMouseOver` |
| 边框 | `InfoBar.ButtonMouseOverBorder` |

**"信息栏" 按钮：按下状态**

![按下信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />按下信息栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonMouseDown` |
| 前景 (文本)  | `InfoBar.ButtonMouseDown` |
| 边框 | `InfoBar.ButtonMouseDownBorder` |

**信息栏按钮：已禁用状态**

![禁用的 "信息栏" 按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />禁用的 "信息栏" 按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonDisabled` |
| 前景 (文本)  | `InfoBar.ButtonDisabled` |
| 边框 | `InfoBar.ButtonDisabledBorder` |

**"信息栏" 按钮：聚焦状态**

![重点信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />重点信息栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonFocus` |
| 前景 (文本)  | `InfoBar.ButtonFocus` |
| 边框 | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>滚动栏
滚动条由 Visual Studio 环境进行样式，无需具有主题。 但是，你可能会决定要利用滚动条中使用的颜色，以便你的 UI 始终与此部分 Visual Studio 环境一致。

![滚动条 (红线) ](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303-140_ScrollbarRedline")<br />滚动条 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...创建要与 Visual Studio 滚动条匹配的 UI 时。 | ...对于不希望始终与滚动条 UI 匹配的任何内容。 |

**滚动条：默认状态**

![默认滚动条](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303-141_Scrollbar")<br />默认滚动条

| 元素 | 标记名称：Category.color |
| --- | --- |
| 滚动条 | `Environment.ScrollBarBackground` |
| 前景（缩略） | `Environment.ScrollBarThumbBackground` |

**滚动条：悬停状态**

![悬停时的滚动条](../../extensibility/ux-guidelines/media/0303-143_scrollbarhover.png "0303-143_ScrollbarHover")<br />悬停时的滚动条

| 元素 | 标记名称：Category.color |
| --- | --- |
| 滚动条 | `Environment.ScrollBarBackground` |
| 前景（缩略） | `Environment.ScrollBarThumbMouseOverBackground` |

*滚动条：按下状态**

![按下的滚动条](../../extensibility/ux-guidelines/media/0303-145_scrollbarpressed.png "0303-145_ScrollbarPressed")<br />按下的滚动条

| 元素 | 标记名称：Category.color |
| --- | --- |
| 滚动条 | `Environment.ScrollBarBackground` |
| 前景（缩略） | `Environment.ScrollBarThumbPressedBackground` |

**滚动条箭头：默认状态**

![默认滚动条箭头](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303-142_ScrollbarArrow")<br />默认滚动条箭头

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ScrollBarArrowBackground`<br /> (设置为与滚动条相同的颜色。 )  |
| 前景（标志符号） | `Environment.ScrollBarArrowGlyph` |

**滚动条箭头：悬停状态**

![悬停时的滚动条箭头](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br />悬停时的滚动条箭头

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ScrollBarArrowMouseOverBackground`<br /> (设置为与滚动条相同的颜色。 )  |
| 前景（标志符号） | `Environment.ScrollBarArrowGlyphMouseOver` |

**滚动条箭头：按下状态**

![按下的滚动条箭头](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br />按下的滚动条箭头

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ScrollBarArrowPressedBackground`<br /> (设置为与滚动条相同的颜色。 )  |
| 前景（标志符号） | `Environment.ScrollBarArrowGlyphPressed` |

### <a name="search-boxes"></a><a name="BKMK_SearchBoxes"></a>搜索框
只要可能，便使用 Visual Studio 环境提供的公共搜索控件。 搜索框颜色位于 **ShellColors.pkgdef** 文件中“SearchControl”类别中，该文件包含输入字段、操作按钮、下拉按钮和下拉菜单中的标记名称。

搜索框可以具有多种状态之一，其中一些状态互相排斥：

- “已设定焦点”或“失去焦点”是指光标是否处于文本框中。

- “活动”或“非活动”是指用户是否在文本框中输入了搜索查询。

- “悬停”表示用户将鼠标指针置于搜索框上方（此状态优先于所有其他状态）。

- “已禁用”表示为当前上下文关闭了搜索功能。

![搜索框 (红线) ](../../extensibility/ux-guidelines/media/0303-110_searchboxredline.png "0303-110_SearchBoxRedline")<br />搜索框 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...设计自定义搜索框时。 | ...对于不是搜索框的任何内容。 |
| | ...对于不希望始终与搜索框 UI 匹配的任何内容。 |

**聚焦搜索输入字段**

![聚焦搜索输入字段](../../extensibility/ux-guidelines/media/0303-111_searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br />聚焦搜索输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.FocusedBackground` |
| 前景（文本） | `SearchControl.FocusedBackground` |
| 边框 | `SearchControl.FocusedBorder` |
| Separator | `SearchControl.FocusedDropDownSeparator` |

**失去焦点，活动搜索输入字段**

![失去焦点的搜索输入字段](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br />失去焦点，活动搜索输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.SearchActiveBackground` |
| 前景（文本） | `SearchControl.SearchActiveBackground` |
| 边框 | `SearchControl.UnfocusedBorder` |
| Separator | `SearchControl.DropDownSeparator` |

**失去焦点，非活动搜索输入字段**

![失去焦点，非活动搜索输入字段](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br />失去焦点，非活动搜索输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.Unfocused` |
| 前景（文本） | `SearchControl.Unfocused` |
| 边框 | `SearchControl.UnfocusedBorder` |
| Separator | `SearchControl.DropDownSeparator` |

**突出显示的搜索输入字段 (纯文本) **

![突出显示的搜索输入字段](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br />突出显示的搜索输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.Selection` |
| 前景（文本） | `SearchControl.FocusedBackground` |
| 边框 | 无 |
| Separator | `SearchControl.FocusedDropDownSeparator` |

**已禁用搜索输入字段**

![已禁用搜索输入字段](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br />已禁用搜索输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.Disabled` |
| 前景（文本） | `SearchControl.Disabled` |
| 边框 | `SearchControl.DisabledBorder` |
| Separator | `SearchControl.DropDownSeparator` |

**聚焦搜索操作按钮**

![已设定焦点的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br />聚焦搜索操作按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（搜索标志符号） | `SearchControl.SearchGlyph` |
| 前景（停止标志符号） | `SearchControl.StopGlyph` |
| 前景（清除标志符号） | `SearchControl.ClearGlyph` |
| 边框 | 空值 |

**失去焦点搜索操作按钮**

![失去焦点搜索操作按钮](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br />失去焦点搜索操作按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（搜索标志符号） | `SearchControl.SearchGlyph` |
| 前景（停止标志符号） | `SearchControl.StopGlyph` |
| 前景（清除标志符号） | `SearchControl.ClearGlyph` |
| 边框 | 空值 |

**按下的搜索操作按钮**

![按下的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br />按下的搜索操作按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.ActionButtonMouseDown` |
| 前景（标志符号） | `SearchControl.ActionButtonMouseDownGlyph` |
| 边框 | `SearchControl.ActionButtonMouseDownBorder` |

**禁用的搜索操作按钮**

![禁用的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br />禁用的搜索操作按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（标志符号） | `SearchControl.ActionButtonDisabledGlyph` |
| 边框 | 无 |

**聚焦搜索下拉按钮**

![聚焦搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br />聚焦搜索下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.FocusedDropDownButton` |
| 前景（标志符号） | `SearchControl.FocusedDropDownButtonGlyph` |
| 边框 | `SearchControl.FocusedDropDownButtonBorder` |

**失去焦点搜索下拉按钮**

![失去焦点搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br />失去焦点搜索下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.UnfocusedDropDownButton` |
| 前景（标志符号） | `SearchControl.UnfocusedDropDownButtonGlyph` |
| 边框 | `SearchControl.UnfocusedDropDownButtonBorder` |

**按下搜索下拉按钮**

![按下搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br />按下搜索下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.MouseDownDropDownButton` |
| 前景（标志符号） | `SearchControl.MouseDownDropDownButtonGlyph` |
| 边框 | `SearchControl.MouseDownDropDownButtonBorder` |

**禁用的搜索下拉按钮**

![禁用的搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br />禁用的搜索下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（标志符号） | `SearchControl.DisabledDownButtonGlyph` |
| 边框 | 无 |

#### <a name="search-drop-down-lists"></a>搜索下拉列表
"搜索框" 下拉菜单可能比 Visual Studio 中的其他下拉菜单稍微复杂一些。 "建议的搜索" 和 "搜索选项" 部分可以在菜单中单独或一起显示，每个部分单独着色。 当这两个部分一起出现时，还会有一条线分隔它们，并且有一个边框环绕整个下拉菜单。

![红线)  (搜索下拉列表 ](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303-124_SearchDropdownRedline")<br />红线)  (搜索下拉列表

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在创建自定义搜索下拉列表时。 | ...对于在其他上下文中出现的下拉列表。 |
| ...正确的列表组件的正确标记名称。 | ...在除指定之外的任何背景/前景组合中。 |

**搜索下拉列表元素**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 边框 | `SearchControl.PopupBorder` |
| Separator | `SearchControl.PopupSectionHeaderSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**建议的搜索：默认状态**

![建议的默认搜索](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303-125_SearchSuggested")<br />建议的默认搜索

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `SearchControl.PopupItemText` |

**建议的搜索：悬停状态**

![悬停时的建议搜索](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br />悬停时的建议搜索

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `SearchControl.PopupMouseOverItemText` |
| 边框 | `SearchControl.PopupControlMouseOverBorder` |

**搜索选项：默认状态**

![搜索复选框](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303-126_SearchCheckbox")<br />默认的搜索选项 (复选框) 

![搜索选项](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303-127_SearchOptions")<br /> (链接的默认搜索选项) 

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupSectionBackgroundGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（复选框文本） | `SearchControl.PopupCheckboxText` |
| 前景（链接文本） | `SearchControl.PopupButtonText` |
| 标题背景 | `SearchControl.PopupSectionHeaderGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（标题文本） | `SearchControl.PopupSectionHeaderText` |

**搜索选项：悬停状态**

![悬停时) 的搜索选项 (复选框](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br />悬停时) 的搜索选项 (复选框

![悬停时的搜索选项 (链接) ](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303-130_SearchOptionsHover")<br />悬停时的搜索选项 (链接) 

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（复选框文本） | `SearchControl.PopupCheckboxMouseDownText` |
| 前景（链接文本） | `SearchControl.PopupButtonMouseDownText` |
| 边框 | `SearchControl.PopupControlMouseOverBorder` |

**搜索选项：按下状态**

![按下搜索选项 (复选框) ](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br />按下搜索选项 (复选框) 

![按下搜索选项 (链接) ](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303-132_SearchOptionsPressed")<br />按下搜索选项 (链接) 

| 元素 | 标记名称：Category.color |
| --- | --- |
| 复选框背景 | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（复选框文本） | `SearchControl.PopupCheckboxMouseDownText` |
| 链接背景 | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（链接文本） | `SearchControl.PopupButtonMouseDownText` |

### <a name="tree-views"></a><a name="BKMK_TreeView"></a> 树视图
多个工具窗口（包括解决方案资源管理器、服务器资源管理器和类视图）实现了其颜色由类别中的颜色名称控制的分层组织方案 `TreeView` 。 树视图中的所有项都具有背景和文本颜色。 具有嵌套子元素的项还具有指示该项是展开还是折叠的标志符号。

![树视图 (红线) ](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303-147_TreeViewRedline")<br />树视图 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...需要实现分层组织视图的任何位置。 | ...对于不类似于树视图的任何内容。 |
| | ...在除指定之外的任何背景/前景组合中。 |

**树视图项：默认状态**

![默认树视图项](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303-148_TreeView")<br />默认树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.Background` |
| 前景（文本） | `TreeView.Background` |
| 前景（标志符号） | `TreeView.Glyph` |
| 边框 | 无 |

**树视图项：悬停状态**

![悬停时的树视图项](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303-149_TreeViewHover")<br />悬停时的树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.Background` |
| 前景（文本） | `TreeView.Background` |
| 前景（标志符号） | `TreeView.GlyphMouseOver` |
| 边框 | 无 |

**树视图项：拖过状态**

![拖过时的树视图项](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303-150_TreeViewDragOver")<br />拖过时的树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.DragOverItem` |
| 前景（文本） | `TreeView.DragOverItem` |
| 前景（标志符号） | `TreeView.DragOverItemGlyph` |
| 边框 | 无 |

**树视图项：已选择，重点状态**

![选定并突出显示的树视图项](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303-151_TreeViewFocused")<br />选定并突出显示的树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive` |
| 前景（文本） | `TreeView.SelectedItemActive` |
| 前景（标志符号） | `TreeView.SelectedItemActiveGlyph` |
| 边框 | `TreeView.FocusVisualBorder` |

**树视图项：已选择，失去焦点状态**

![所选和失去焦点树视图项](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303-152_TreeViewUnfocused")<br />所选和失去焦点树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive` |
| 前景（文本） | `TreeView.SelectedItemInactive` |
| 前景（标志符号） | `TreeView.SelectedItemInactiveGlyph` |
| 边框 | 无 |

**树视图项：悬停、选定和聚焦状态**

![悬停时的选定和突出显示的树视图项](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br />悬停时的选定和突出显示的树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive` |
| 前景（文本） | `TreeView.SelectedItemActive` |
| 前景（标志符号） | `TreeView.SelectedItemActiveGlyphMouseOver` |
| 边框 | `TreeView.FocusVisualBorder` |

**树视图项：悬停、选定和失去焦点状态**

![悬停时的选定和失去焦点树视图项](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br />悬停时的选定和失去焦点树视图项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive` |
| 前景（文本） | `TreeView.SelectedItemInactive` |
| 前景（标志符号） | `TreeView.SelectedItemActiveGlyphMouseOver` |
| 边框 | 无 |

## <a name="shell-appearance"></a>Shell 外观

### <a name="background"></a>背景
环境背景由两层组成。 下层是覆盖整个 IDE 的纯色。 上层位于命令架下，以及 IDE 左边缘和右边缘上的工具窗口自动隐藏通道之间。 在浅色和深色主题中，顶部和底部背景层设置为相同的颜色。

![Visual Studio shell 背景 (红线) ](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303-187_ShellBackgroundRedline")<br />Visual Studio shell 背景 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...需要与 Visual Studio 环境背景匹配的位置。 | ...作为不是背景图面的位置的填充。 |
| | ...作为要在其上放置前景元素的背景。 |

**底层 shell 外观**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.EnvironmentBackground` |

**顶层 shell 外观**

> 在 Visual Studio 2013 浅色和深色主题中设置为相同颜色值的梯度停止点。

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |

### <a name="command-shelf"></a>命令架
有两组标记名称用于命令架背景：一组用于菜单栏所在的位置，另一组用于命令栏所在的位置。 单个命令栏组具有自己的背景色值（在“命令栏”部分中进行更详细的讨论）。 菜单栏和命令栏文本分别在菜单和命令栏部分中进行了讨论。

![Visual Studio 命令货位 (红线) ](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303-188_CommandShelfRedline")<br />Visual Studio 命令货位 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...用于放置菜单或工具栏的区域。 | ...对于与命令架不相似的区域。 |
|...具有正确背景/前景标记名称组合的。 | |

**命令架菜单栏**

> 在 Visual Studio 2013 浅色和深色主题中设置为相同颜色值的梯度停止点。

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

**命令盘架命令栏**

> 在 Visual Studio 2013 浅色和深色主题中设置为相同颜色值的梯度停止点。

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>清单设计器
清单设计器旨在作为可用于更加轻松地在 Windows 8 和 Windows Phone 8 项目中编辑清单文件的方法。 虽然没有可供使用的共享框架，不过匹配方向/导航选项卡和整体结构的设计布局和颜色是合适的。 有关布局详细信息的更多信息，请参见 [Layout for Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md)。

![清单设计器 (红线) ](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303-175_ManifestDesignerRedline")<br />清单设计器 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于类似于清单设计器的设计器。 | ...如果有六个以上的选项卡。 |
| ...在文档中的编辑器的顶部使用公共选项卡控件。 | ...对于不像清单设计器那样构造的任何 UI。 |

**清单设计器选定的选项卡：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.TabActive` |
| 边框 | 无 |

**清单设计器选定的说明窗格：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.DescriptionPane` |

**清单设计器所选内容页：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.Background` |
| 对话框帮助程序文本 | `ManifestDesigner.WatermarkText`<br /> (此标记名称与其功能不匹配。 )  |

**清单设计器选项卡：未选择状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.Tab.Inactive` |

**清单设计器选项卡：悬停状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>命令结构

### <a name="menus"></a><a name="BKMK_CommandMenus"></a> 弹出式
菜单可以出现在 Visual Studio 中的多个位置：主菜单栏、嵌入在文档或工具窗口中，或者在整个 IDE 的各个位置右键单击。 与其他 UI 元素关联的菜单的实现在针对相应元素的部分中进行讨论。 应始终使用由 Visual Studio 环境提供的标准菜单实现。 但是，在某些极少数情况下，你可能无法访问标准 Visual Studio 菜单。 在这些情况下，请使用以下标记名称以确保 UI 与 Visual Studio 中的其他菜单保持一致。

![Visual Studio 菜单 (红线) ](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303-000_MenuRedline")<br />Visual Studio 菜单 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...需要创建自定义菜单时。| ...单独的背景色。 始终使用指定的背景/前景组合。 |
| ...当你具有要与 Visual Studio 菜单匹配的新 UI 组件时。| |

#### <a name="menu-titles"></a>菜单标题
菜单标题由背景、边框和标题文本以及可选的标志符号（通常是在菜单位于命令栏中使用）组成。

![菜单标题 (红线) ](../../extensibility/ux-guidelines/media/0303-001_menutitleredline.png "0303-001_MenuTitleRedline")<br />菜单标题 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...每当创建自定义菜单标题时。 | ...对于不希望始终与菜单标题匹配的任何内容。 |
| | ...在除指定之外的任何背景/前景组合中。 |

**菜单标题：默认状态**

![默认菜单标题](../../extensibility/ux-guidelines/media/0303-002_menutitledefault.png "0303-002_MenuTitleDefault")<br />默认菜单标题

![带有标志符号的默认菜单标题](../../extensibility/ux-guidelines/media/0303-003_menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br />带有标志符号的默认菜单标题

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景 (文本)  | `Environment.CommandBarTextActive` |
| 前景 (标志符号)  | `Environment.CommandBarMenuGlyph` |
| 边框 | 无 |

**菜单标题：悬停状态**

![悬停时的菜单标题](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303-004_MenuTitleHover")<br />悬停时的菜单标题

![悬停时的具有字形的菜单标题](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br />悬停时的具有字形的菜单标题

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景 (文本)  | `Environment.CommandBarTextHover` |
| 前景 (标志符号)  | `Environment.CommandBarMenuMouseOverGlyph` |
| 边框 | `Environment.CommandBarBorder` |

**菜单标题：按下状态**

![按下菜单标题](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303-006_MenuTitlePressed")<br />按下菜单标题

![按下了标志符号的菜单标题](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br />按下了标志符号的菜单标题

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（标志符号） | `Environment.CommandBarMenuMouseDownGlyph` |
| 边框 | `Environment.CommandBarMenuBorder`<br />仅 (左、上、右边缘。 )  |

**菜单标题：已禁用状态**

![禁用了标志符号的菜单标题](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br />禁用了标志符号的菜单标题

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（文本） | `Environment.CommandBarTextInactive` |
| 前景（标志符号） | `Environment.CommandBarTextInactive` |
| 边框 | 无 |

#### <a name="menu-items"></a>菜单项
各个菜单项由菜单文本和可选的图标、复选框或子菜单标志符号组成。 其背景和文本颜色会在鼠标悬停在上方时更改。 此颜色标记是前景/背景对。

![菜单项红线](../../extensibility/ux-guidelines/media/0303-009_menuitemredline.png "0303-009_MenuItemRedline")

| 使用 .。。 | 请勿使用 .。。 |
|---|---|
| ...对于从菜单栏或命令栏启动的任何下拉列表。 | ...对于其他上下文中的任何下拉列表。 |
| | ...在除指定之外的任何背景/前景组合中。 |

**菜单项：默认状态**

![默认菜单项](../../extensibility/ux-guidelines/media/0303-010_menudefault.png "0303-010_MenuDefault")<br />默认菜单项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMenuBackgroundGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（子菜单标志符号） | `Environment.CommandBarMenuSubmenuGlyph` |
| 边框 | `Environment.CommandBarMenuBorder` |
| 图标通道背景 | `Environment.CommandBarMenuIconBackground` |
| Separator | `Environment.CommandBarMenuSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**菜单项：选中并选中状态**

![选中的菜单](../../extensibility/ux-guidelines/media/0303-011_menuchecked.png "0303-011_MenuChecked")<br />选中的菜单项

![选定的菜单](../../extensibility/ux-guidelines/media/0303-012_menuselected.png "0303-012_MenuSelected")<br />选定菜单项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 选中标记 | `Environment.CommandBarCheckBox` |
| 复选标记背景 | `Environment.CommandBarSelectedIcon` |
| 图标背景 | `Environment.CommandBarSelected` |
| 图标边框 | `Environment.CommandBarSelectedBorder` |

**菜单项：悬停状态**

![菜单悬停](../../extensibility/ux-guidelines/media/0303-013_menuhover.png "0303-013_MenuHover")<br />悬停时的菜单项

![选中的菜单悬停](../../extensibility/ux-guidelines/media/0303-014_menuhoverchecked.png "0303-014_MenuHoverChecked")<br />悬停时的选中菜单项

![选定的菜单悬停](../../extensibility/ux-guidelines/media/0303-015_menuhoverselected.png "0303-015_MenuHoverSelected")<br />悬停时的选定菜单项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMenuItemMouseOver` |
| 前景（文本） | `Environment.CommandBarMenuItemMouseOverText` |
| 前景（子菜单标志符号） | `Environment.CommandBarMenuMouseOverSubmenuGlyph` |
| 选中标记 | `Environment.CommandBarCheckBoxMouseOver` |
| 复选标记背景 | `Environment.CommandBarHoverOverSelectedIcon` |
| 图标背景 | `Environment.CommandBarHoverOverSelected` |
| 图标边框 | `Environment.CommandBarHoverOverSelectedIconBorder` |

**菜单项：已禁用状态**

![禁用的菜单](../../extensibility/ux-guidelines/media/0303-016_menudisabled.png "0303-016_MenuDisabled")<br />禁用的菜单项

![选中的禁用的菜单](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303-017_MenuDisabledChecked")<br />带复选标记的禁用菜单项

| 元素 | 标记名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.CommandBarTextInactive` |
| 前景（子菜单标志符号） | `Environment.CommandBarMenuSubmenuGlyph` |
| 选中标记 | `Environment.CommandBarCheckBoxDisabled` |
| 复选标记背景 | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>命令栏
在 Visual Studio IDE 中，命令栏可以出现在多个位置，最值得注意的是命令架以及嵌入在工具或文档窗口中。

一般而言，需始终使用由 Visual Studio 环境提供的标准命令栏实现。 使用标准机制可确保所有视觉细节都正确显示，并且交互元素的行为与其他 Visual Studio 命令栏控件一致。 但是，如果你需要构建自己的命令栏，请确保使用以下标记名称正确设计其样式。

![命令栏红线](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303-018_CommandBarRedline")<br />命令栏 (红线) 

![“溢出”按钮红线](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303-019_OverflowButtonRedline")<br />溢出按钮 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在需要嵌入式命令栏，但无法使用标准 Visual Studio 命令栏实现的位置。 | ...对于与命令栏不相似的 UI 元素。 |
| | ...对于指定了其标记名称的命令栏组件之外的命令栏组件。 |

#### <a name="command-bar-groups"></a>命令栏组
命令栏组由一组相关命令栏控件组成，可能包含任何数量的按钮、拆分按钮、下拉菜单、组合框或菜单。 这些控件的颜色通过单独的标记名称进行控制，在本指南中的其他位置单独进行了讨论。 分隔线用于将命令栏组划分为相关子组。

![命令栏组红线](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303-020_CommandBarGroupRedline")<br />命令栏组 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在需要嵌入式命令栏，但无法使用标准 Visual Studio 命令栏实现的位置。 | ...对于与命令栏不相似的 UI 元素。 |
| | ...对于指定了其标记名称的命令栏组件之外的命令栏组件。 |

**命令栏组：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 边框 | `Environment.CommandBarToolBarBorder` |
| 拖拽句柄 | `Environment.CommandBarDragHandle` |
| Separator | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>命令图标
![“命令”图标红线](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303-021_CommandIconRedline1")<br />命令图标 (红线) 

![带有文本红线的命令图标](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303-022_CommandIconRedline2")<br />带有文本的命令图标 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于将放置在命令栏上的任何按钮。 | ...对于具有自己的标记名称的控件。 |
| | ...在除指定之外的任何背景/前景组合中。 |

**命令图标：默认状态**

![“命令”图标默认值](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303-023_CommandIconDefault")<br />默认命令图标

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 不适用（从命令栏背景继承） |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 边框 | 空值 |

**命令图标：默认状态，已选中**

![默认，选定的命令图标](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br />默认，选定的命令图标

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarSelected` |
| 前景（文本） | `Environment.CommandBarTextSelected` |
| 边框 | `Environment.CommandBarSelectedBorder` |

**命令图标：悬停状态或焦点状态**

![悬停或焦点上的命令图标](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303-025_CommandIconHover")<br />悬停或焦点上的命令图标

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.CommandBarTextHover` |
| 边框 | `Environment.CommandBarBorder` |

**命令图标：已选择的悬停状态或焦点状态**

![悬停或焦点上的选定命令图标](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br />悬停或焦点上的选定命令图标

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarHoverOverSelected` |
| 前景（文本） | `Environment.CommandBarTextHoverOverSelected` |
| 边框 | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **命令图标：按下状态**

![已按下命令图标](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303-027_CommandIconPressed")<br />已按下命令图标

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseDownBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.CommandBarTextMouseDown` |
| 边框 | `Environment.CommandBarBorder` |

**命令图标：已禁用状态**

![已禁用命令图标](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303-028_CommandIconDisabled")<br />已禁用命令图标

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 不适用（从命令栏背景继承） |
| 前景（文本） | `Environment.CommandBarTextInactive` |
| 边框 | 空值 |

#### <a name="command-bar-combo-boxes"></a><a name="BKMK_CommandComboBox"></a> 命令栏组合框

> [!IMPORTANT]
> 组合框类似于下拉列表，但包含一个可编辑文本区域。 如果下拉不包含可编辑文本区域，请使用 [命令栏下拉](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)标记的颜色标记。

!["命令栏" 组合框红线](../../extensibility/ux-guidelines/media/0303-029_comboboxredline.png "0303-029_ComboBoxRedline")<br />"命令栏" 组合框 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...生成自定义组合框时。 | ...对于您不希望始终与命令栏 UI 匹配的任何内容。 |
| ...创建类似于组合框的命令栏控件时。 | ...当你有权访问具有样式的组合框时。 |

**"命令栏" 组合框输入字段：默认状态**

!["命令栏" 组合框输入字段](../../extensibility/ux-guidelines/media/0303-030_comboboxinputfield.png "0303-030_ComboBoxInputField")<br />"命令栏" 组合框输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxBackground` |
| 前景（文本） | `Environment.ComboBoxText` |
| 边框 | `Environment.ComboBoxBorder` |
| Separator | 无分隔符 |

**命令栏下拉按钮：默认状态**

![组合框拖放&#45;向下按钮](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br />命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 不适用（从命令栏背景继承） |
| 前景（标志符号） | `Environment.ComboBoxGlyph` |

**命令栏下拉列表：默认状态**

![命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br />命令栏下拉列表

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxPopupBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.ComboBoxItemText` |
| 边框 | `Environment.ComboBoxPopupBorder` |

**"命令栏" 组合框输入字段：悬停状态**

![悬停时的 "命令栏" 组合框输入字段](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br />悬停时的 "命令栏" 组合框输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.ComboBoxMouseOverText` |
| 边框 | `Environment.ComboBoxMouseOverBorder` |
| Separator | `Environment.ComboBoxMouseOverSeparator` |

 **命令栏下拉按钮：悬停状态**

![悬停时的命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br />悬停时的命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxButtonMouseOverBackground` |
| 前景（标志符号） | `Environment.ComboBoxMouseOverGlyph` |

**命令栏下拉列表：悬停状态**

 ![悬停时的命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-035_comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br />悬停时的命令栏下拉列表

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景（菜单项） | `Environment.ComboBoxItemMouseOverBackground` |
| 前景（文本） | `Environment.ComboBoxItemMouseOverText` |
| 边框（菜单项） | `Environment.ComboBoxItemMouseOverBorder` |

 **"命令栏" 组合框输入字段：焦点状态**

![焦点命令栏组合框输入字段](../../extensibility/ux-guidelines/media/0303-036_comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br />焦点命令栏组合框输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxFocusedBackground` |
| 前景（文本） | `Environment.ComboBoxFocusedText` |
| 边框 | `Environment.ComboBoxFocusedBorder` |
| Separator | `Environment.ComboBoxFocusedButtonSeparator` |

**命令栏下拉按钮：焦点状态**

![重点命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br />重点命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxFocusedButtonBackground` |
| 前景（标志符号） | `Environment.ComboBoxFocusedGlyph` |

 **"命令栏" 组合框输入字段：按下状态**

![按下的命令栏组合框输入字段](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br />按下的命令栏组合框输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxMouseDownBackground` |
| 前景（文本） | `Environment.ComboBoxMouseDownText` |
| 边框 | `Environment.ComboBoxMouseDownBorder` |
| Separator | `Environment.ComboBoxMouseDownSeparator` |

**命令栏下拉按钮：按下状态**

![按下的命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br />按下的命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxButtonMouseDownBackground` |
| 前景（标志符号） | `Environment.ComboBoxMouseDownGlyph` |

**"命令栏" 组合框输入字段：已禁用状态**

![禁用的命令栏组合框输入字段](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br />禁用的命令栏组合框输入字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxDisabledBackground` |
| 前景（文本） | `Environment.ComboBoxDisabledText` |
| 边框 | `Environment.ComboBoxDisabledBorder` |
| Separator | 无分隔符 |

**命令栏下拉按钮：禁用状态**

![禁用的命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br />禁用的命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（标志符号） | `Environment.ComboBoxDisabledGlyph` |

#### <a name="command-bar-drop-downs"></a><a name="BKMK_CommandDropDown"></a> 命令栏下拉

> [!IMPORTANT]
> 下拉列表类似于组合框，但缺少可编辑文本区域。 如果下拉框中包含可编辑文本区域，请使用 " [命令栏" 组合框](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)的颜色标记。

![命令栏下拉 (红线) ](../../extensibility/ux-guidelines/media/0303-042_dropdownredline.png "0303-042_DropdownRedline")<br />命令栏下拉 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在创建自定义下拉列表控件时。 | ...对于不类似于下拉列表的任何内容。 |
| | ...对于组合框或拆分按钮。 |

**命令栏下拉选择字段：默认状态**

![默认命令栏下拉选择字段](../../extensibility/ux-guidelines/media/0303-043_dropdownselectionfield.png "0303-043_DropdownSelectionField")<br />默认命令栏下拉选择字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownBackground` |
| 前景（文本） | `DropDownText` |
| 边框 | `DropDownBorder` |
| Separator | 无分隔符 |

**命令栏下拉按钮：默认状态**

![默认命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303-044_DropdownButton")<br />默认命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（标志符号） | `Environment.DropDownGlyph` |

**命令栏下拉列表：默认状态**

![默认命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303-045_DropdownList")<br />默认命令栏下拉列表

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownPopupBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.ComboBoxItemText` |
| 边框 | `Environment.DropDownPopupBorder` |
| Shadow | `Environment.DropShadowBackground` |

**命令栏下拉选择字段：悬停状态**

![悬停时的命令栏下拉选择字段](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br />悬停时的命令栏下拉选择字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.DropDownMouseOverText` |
| 边框 | `Environment.DropDownMouseOverBorder` |
| Separator | `Environment.DropDownButtonMouseOverSeparator` |

**命令栏下拉按钮：悬停状态**

![悬停时的命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br />悬停时的命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownButtonMouseOverBackground` |
| 前景（标志符号） | `Environment.DropDownMouseOverGlyph` |

**命令栏下拉列表：悬停状态**

![悬停时的命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-048_dropdownlisthover.png "0303-048_DropdownListHover")<br />悬停时的命令栏下拉列表

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景（菜单项） | `Environment.ComboBoxItemMouseOverBackground` |
| 前景（文本） | `Environment.ComboBoxItemMouseOverText` |
| 边框（菜单项） | `Environment.ComboBoxItemMouseOverBorder` |

 **命令栏下拉选择字段：按下状态**

![下拉&#45;按下的选择字段](../../extensibility/ux-guidelines/media/0303-049_dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br />按下的命令栏下拉选择字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownMouseDownBackground` |
| 前景（文本） | `Environment.DropDownMouseDownText` |
| 边框 | `Environment.DropDownMouseDownBorder` |
| Separator | `Environment.DropDownButtonMouseDownSeparator` |

**命令栏下拉按钮：按下状态**

![按下的命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br />按下的命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownButtonMouseDownBackground` |
| 前景（标志符号） | `Environment.DropDownMouseDownGlyph` |

**命令栏下拉选择字段：已禁用状态**

![禁用的命令栏下拉选择字段](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")<br />禁用的命令栏下拉选择字段

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownDisabledBackground` |
| 前景（文本） | `Environment.DropDownDisabledText` |
| 边框 | `Environment.DropDownDisabledBorder` |
| Separator | 无分隔符 |

**命令栏下拉按钮：禁用状态**

![禁用的命令栏下拉按钮](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")<br />禁用的命令栏下拉按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（标志符号） | `Environment.DropDownDisabledGlyph` |

#### <a name="command-bar-split-buttons"></a>命令栏拆分按钮
拆分按钮与其他命令栏控件（如按钮、菜单和命令栏文本）共享许多令牌名称。 为方便起见，在此处重复了所有必要的操作和下拉按钮令牌名称。 拆分按钮下拉列表是 [命令栏菜单](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)的实现。

![“拆分”按钮红线](../../extensibility/ux-guidelines/media/0303-053_splitbuttonredline.png "0303-053_SplitButtonRedline")<br />命令栏拆分按钮 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...创建自定义拆分按钮时。 | ...对于其他类型的按钮。 |
| | ...在除指定之外的任何背景/前景组合中。 |

**命令栏拆分按钮：默认状态**

![默认命令栏拆分按钮](../../extensibility/ux-guidelines/media/0303-054_splitbutton.png "0303-054_SplitButton")<br />默认命令栏拆分按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 无 |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（标志符号） | `Environment.CommandBarSplitButtonGlyph` |
| 边框 | 空值 |
| Separator | 空值 |

**命令栏拆分按钮：悬停状态**

![悬停时的命令栏拆分按钮](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303-055_SplitButtonHover")<br />悬停时的命令栏拆分按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.CommandBarTextHover` |
| 前景（标志符号） | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| 边框 | `Environment.CommandBarBorder` |
| Separator | `Environment.CommandBarSplitButtonSeparator` |

**命令栏拆分按钮：按下状态**

![按下命令栏拆分按钮](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303-056_SplitButtonPressed")<br />按下命令栏拆分按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseDownBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.CommandBarTextMouseDown` |
| 前景（标志符号） | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| 边框 | `Environment.CommandBarBorder` |
| Separator | 空值 |

**命令栏拆分按钮：已禁用状态**

![禁用的命令栏拆分按钮](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br />禁用的命令栏拆分按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（文本） | `Environment.ComboBoxItemTextInactive` |
| 前景（标志符号） | `Environment.CommandBarTextInactive` |
| 边框 | 空值 |
| Separator | 空值 |

#### <a name="command-bar-more-options-and-overflow-buttons"></a>命令栏的 "更多选项" 和 "溢出" 按钮
通过添加或删除相关命令栏按钮来自定义命令栏组时，可使用“更多选项”按钮。 命令栏由于水平空间不足而被截断，以及在单击操作中显示包含无法显示的命令栏按钮的菜单时，会出现“溢出”按钮。 这两个按钮的颜色通过一组相同的标记名称进行控制。

![命令栏中的 "更多选项" 按钮 (红线) ](../../extensibility/ux-guidelines/media/0303-058_moreoptionsredline.png "0303-058_MoreOptionsRedline")<br />命令栏中的 "更多选项" 按钮 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于自定义 "更多选项" 或 "溢出" 按钮。 | ...对于没有类似于 "更多选项" 或 "溢出" 按钮的功能的按钮。 |

**命令栏的 "更多选项" 和 "溢出" 按钮：默认状态**

![默认命令栏的 "更多选项" 按钮](../../extensibility/ux-guidelines/media/0303-059_moreoptions.png "0303-059_MoreOptions")<br />默认命令栏的 "更多选项" 按钮

![默认命令栏 "溢出" 按钮](../../extensibility/ux-guidelines/media/0303-060_overflow.png "0303-060_Overflow")<br />默认命令栏 "溢出" 按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarOptionsBackground` |
| 前景（标志符号） | `Environment.CommandBarOptionsGlyph` |

**命令栏的 "更多选项" 和 "溢出" 按钮：悬停状态**

![悬停时的命令栏 "更多选项" 按钮](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303-061_MoreOptionsHover")<br />悬停时的命令栏 "更多选项" 按钮

![悬停时的命令栏 "溢出" 按钮](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303-062_OverflowOptions")<br />悬停时的命令栏 "溢出" 按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（标志符号） | `Environment.CommandBarOptionsMouseDownGlyph` |

**命令栏的 "更多选项" 和 "溢出" 按钮：按下状态**

![按下命令栏的 "更多选项" 按钮](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303-063_MoreOptionsPressed")<br />按下命令栏的 "更多选项" 按钮

![按下的“溢出”](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303-064_OverflowPressed")<br />按下命令栏的 "溢出" 按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（标志符号） | `Environment.CommandBarOptionsMouseDownGlyph` |

## <a name="document-windows"></a>文档窗口
无需复制文档窗口，因为它们由 Visual Studio 环境提供。 但是，你可能会决定要利用文档窗口中使用的颜色，以便你的 UI 显示方式始终与这部分 Visual Studio 环境一致。

使用文档窗口颜色标记时，请注意仅将它们用于类似元素，并且始终成对使用。 否则，你可能会在 UI 中收到意外结果。

### <a name="document-window-frames"></a>文档窗口框架
文档窗口可以在 IDE 中停靠或作为单独窗口浮动。 当文档窗口在 IDE 外部浮动时，它仍然处于文档中，并且具有与在 IDE 的一部分时相同的背景、边框、文本和选项卡颜色。 但是，文档位于具有自己的背景、边框和文本颜色的框架中。 当工具窗口停靠在文档井中时，它们会从文档窗口标记名称继承其选项卡的行为和颜色。

![停靠文档窗口 (红线) ](../../extensibility/ux-guidelines/media/0303-065_dockeddocumentwindowredline.png "0303-065_DockedDocumentWindowRedline")<br />停靠文档窗口 (红线) 

![浮动文档窗口 (红线) ](../../extensibility/ux-guidelines/media/0303-066_floatingdocumentwindowredline.png "0303-066_FloatingDocumentWindowRedline")<br />浮动文档窗口 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建要与文档窗口匹配的 UI 的任何位置。 | ... 对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**停靠或浮动文档窗口：默认状态**

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 取决于文档类型 |
| 前景（文本） | 取决于文档类型 |
| 边框 | `Environment.ToolWindowBorder` |

**聚焦的浮动文档窗口框架：默认状态**

![默认焦点，浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303-067_FrameFocused")<br />默认焦点，浮动文档窗口框架

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowFloatingFrame` |
| 前景（文本） | `Environment.ToolWindowFloatingFrame` |
| 前景（标志符号） | `Environment.RaftedWindowButtonActiveGlyph` |
| 边框 | `Environment.MainWindowActiveDefaultBorder` |
| 边框（标志符号） | `Environment.RaftedWindowButtonActiveBorder`<br /> (设置为透明)  |

**失去焦点，浮动文档窗口框架：默认状态**

![默认的失去焦点，浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303-068_FrameUnfocused")<br />默认的失去焦点，浮动文档窗口框架

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowFloatingFrameInactive` |
| 前景（文本） | `Environment.ToolWindowFloatingFrameInactive` |
| 前景（标志符号） | `Environment.RaftedWindowButtonInactiveGlyph` |
| 边框 | `Environment.MainWindowInactiveBorder` |
| 边框（标志符号） | `Environment.RaftedWindowButtonInactiveBorder`<br /> (设置为透明)  |

**聚焦的浮动文档窗口框架：悬停状态**

![悬停时的浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-069_framefocusedhover.png "0303-069_FrameFocusedHover")<br />悬停时的浮动文档窗口框架

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景（标志符号） | `Environment.RaftedWindowButtonHoverActive` |
| 前景（标志符号） | `Environment.RaftedWindowButtonHoverActiveGlyph` |
| 边框（标志符号） | `Environment.RaftedWindowButtonHoverActiveBorder` |

**失去焦点，浮动文档窗口框架：悬停状态**

![悬停时的失去焦点，浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-070_frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br />悬停时的失去焦点，浮动文档窗口框架

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景（标志符号） | `EnvironmentRaftedWindowButtonHoverInactive` |
| 前景（标志符号） | `Environment.RaftedWindowButtonHoverInactiveGlyph` |
| 边框（标志符号） | `Environment.RaftedWindowButtonHoverInactiveBorder` |

**聚焦的浮动文档窗口框架：按下状态**

![专注于按下的浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-071_framefocusedpressed.png "0303-071_FrameFocusedPressed")<br />专注于按下的浮动文档窗口框架

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景（标志符号） | `Environment.RaftedWindowButtonDown` |
| 前景（标志符号） | `Environment.RaftedWindowButtonDownGlyph` |
| 边框（标志符号） | `Environment.RaftedWindowButtonDownBorder` |

### <a name="document-tabs"></a>文档选项卡
文档选项卡位于选项卡通道中，以指示当前打开的文档，以及当前选择或活动的文档。 如果用户将工具窗口置于文档选项卡通道中，则这些窗口也可以在其中停靠。 在此情况下，它们使用与文档窗口相同的选项卡颜色。 如果你在创建要始终与文档窗口颜色匹配的 UI（包括主题更新，或如果安装新主题），则引用这些颜色标记。

![ (红线的文档选项卡) ](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303-072_DocumentTabRedline")<br /> (红线的文档选项卡) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建要与文档选项卡匹配并自动选取主题更新或新主题颜色的 UI 的任何位置。 | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

#### <a name="open-document-tabs"></a>打开文档选项卡
每个打开的文档都在文档选项卡通道中具有显示其名称的选项卡。 文档可以处于已选定状态，或在后台打开，其选项卡会反映这些状态：

- 已选定选项卡表示当前显示在文档井中的文档。 已选定选项卡具有沿文档井上边缘扩展的文档边框。

- 背景选项卡是指不是当前选定选项卡的任何文档选项卡。单击后，它们将成为选定的选项卡，并从这些标记名称获取所有背景、边框和文本颜色。

![ (红线打开文档选项卡) ](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")<br /> (红线打开文档选项卡) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...正在创建自定义文档选项卡。 | ...对于临时 (预览) 选项卡。 |
| | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**选定，重点文档选项卡**

![选定，重点文档选项卡](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303-074_SelectedTabFocused")<br />选定，重点文档选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabSelectedGradientTop`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.FileTabSelectedText` |
| 边框 | `Environment.FileTabSelectedBorder`<br /> (设置为与背景相同的颜色 )  |
| 文档边框 | `Environment.FileTabDocumentBorderBackground` |

**已选择，失去焦点文档选项卡**

![已选择，失去焦点文档选项卡](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br />已选择，失去焦点文档选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabInactiveGradientTop`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.FileTabInactiveText` |
| 边框 | `Environment.FileTabInactiveBorder`<br /> (设置为与背景相同的颜色 )  |
| 文档边框 | `Environment.FileTabInactiveDocumentBorderBackground` |

**"背景文档" 选项卡：默认状态**

![默认背景文档选项卡](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303-076_BackgroundTab")<br />默认背景文档选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabBackground` |
| 前景（文本） | `Environment.FileTabText` |
| 边框 | `Environment.FileTabBorder`<br /> (设置为与背景相同的颜色 )  |

**"背景文档" 选项卡：悬停状态**

![悬停时的背景文档选项卡](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303-077_BackgroundTabHover")<br />悬停时的背景文档选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabHotGradientTop`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.FileTabHotText` |
| 边框 | `Environment.FileTabHotBorder`<br /> (设置为与背景相同的颜色 )  |

#### <a name="preview-tab"></a>预览选项卡
也称为 "临时" 选项卡。当用户单击 "解决方案资源管理器工具" 窗口中的项时，"预览" 选项卡将显示在文档选项卡通道右侧。 它充当文档的预览，还为用户提供用于使文档在文档选项卡通道左侧保持打开状态的选项。 一次只能打开一个预览选项卡。 预览选项卡具有背景和选定状态（与打开的选项卡一样），可以在其活动状态下具有焦点或失去焦点。

![预览选项卡 (红线) ](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303-078_PreviewTabRedline")<br />预览选项卡 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建临时预览并希望某个元素与当前 "预览" 选项卡颜色匹配的任何位置。 | ...对于任何类型的文档或不是临时的选项卡 (预览) 。 |
| | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**重点，选择的预览选项卡**

![重点，选择的预览选项卡](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303-079_PreviewTabFocused")<br />重点，选择的预览选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalSelectedActive` |
| 前景（文本） | `Environment.FileTabProvisionalSelectedActiveForeground` |
| 边框 | `Environment.FileTabProvisionalSelectedActiveBorder`<br /> (设置为与背景相同的颜色 )  |
| 文档边框 | `Environment.FileTabProvisionalSelectedActiveBorder` |

**失去焦点，选择的预览选项卡**

![失去焦点，选择的预览选项卡](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br />失去焦点，选择的预览选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalSelectedInactive` |
| 前景（文本） | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| 边框 | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| 文档边框 | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**背景预览选项卡：默认状态**

![默认背景预览选项卡](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br />默认背景预览选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalInactive` |
| 前景（文本） | `Environment.FileTabProvisionalInactiveForeground` |
| 边框 | `Environment.FileTabProvisionalInactiveBorder`<br /> (设置为与背景相同的颜色 )  |

**背景预览选项卡：悬停状态**

![悬停时的 "背景预览" 选项卡](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br />悬停时的 "背景预览" 选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalHover` |
| 前景（文本） | `Environment.FileTabProvisionalHoverForeground` |
| 边框 | `Environment.FileTabProvisionalHoverBorder`<br /> (设置为与背景相同的颜色 )  |

#### <a name="document-overflow-button"></a>文档溢出按钮
如果有一个或多个文档打开，则无论当前配置中是否有垂直空间可容纳所有文档选项卡，都会提供文档溢出按钮。 "文档溢出" 下拉菜单（由 [命令栏菜单](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus) 颜色控制）显示所有打开的文档的列表（可见和隐藏），溢出标志符号会根据是否所有打开的文档都显示在选项卡通道中而发生变化。

![文档溢出按钮 (红线) ](../../extensibility/ux-guidelines/media/0303-083_overflowredline.png "0303-083_OverflowRedline")<br />文档溢出按钮 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...创建自定义文档溢出按钮时。 | ...对于不类似于溢出按钮的 UI。 |
| | ...对于命令栏溢出按钮。 |

**文档溢出按钮：默认状态**

![默认文档溢出按钮](../../extensibility/ux-guidelines/media/0303-084_overflow.png "0303-084_Overflow")<br />默认文档溢出按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DocWellOverflowButtonBackground` |
| 前景（标志符号） | `Environment.DocWellOverflowButtonGlyph` |
| 边框 | 空值 |

**文档溢出按钮：悬停状态**

![悬停时的文档溢出按钮](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303-085_OverflowHover")<br />悬停时的文档溢出按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DocWellOverflowButtonMouseOverBackground` |
| 前景（标志符号） | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| 边框 | `Environment.DocWellOverflowButtonMouseOverBorder` |

**文档溢出按钮：按下状态**

![按下的文档溢出按钮](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303-086_OverflowPressed")<br />按下的文档溢出按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.DocWellOverflowButtonMouseDownBackground` |
| 前景（标志符号） | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| 边框 | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>标记
Visual Studio 支持标记，这使用户可以声明可搜索的关键字以用于跟踪。 例如，项目经理和开发人员可以使用 Team Foundation Server (TFS) 对工作项进行标记。 下表为标记本身以及在悬停和已选定状态下出现的“关闭图标”标志符号提供颜色名称。

![在 Visual Studio 中标记 (红线) ](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303-176_TaggingRedline")<br />在 Visual Studio 中标记 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...适用于支持标记的 UI。 | ...适用于任何其他类型的 UI。 |

#### <a name="tags"></a>Tags

**标记：默认状态**

![默认标记](../../extensibility/ux-guidelines/media/0303-177_tag.png "0303-177_Tag")<br />默认标记

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.Background` |
| 前景（文本） | `Tag.Background` |

**标记：悬停状态**

![悬停时的标记](../../extensibility/ux-guidelines/media/0303-178_taghover.png "0303-178_TagHover")<br />悬停时的标记

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.HoverBackground` |
| 前景（文本） | `Tag.HoverBackgroundText` |

**标记：按下状态**

![按下标记](../../extensibility/ux-guidelines/media/0303-179_tagpressed.png "0303-179_TagPressed")<br />按下标记

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.PressedBackground` |
| 前景（文本） | `Tag.PressedBackgroundText` |

**标记：已选择状态**

![选定标记](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303-180_TagSelected")<br />选定标记

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.SelectedBackground` |
| 前景（文本） | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>关闭 (&times;) 标记标志符号

**关闭 (&times;) 标记字形：默认状态**

![&times;) 标记标志符号的默认关闭 (](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303-181_TagGlyph")<br />&times;) 标记标志符号的默认关闭 (

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（标志符号） | `Tag.TagHoverGlyph` |

**关闭 (&times;) 标记字形：悬停状态**

![关闭 (&times; 悬停时) 标记标志符号](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303-182_TagGlyphHover")<br />关闭 (&times; 悬停时) 标记标志符号

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagHoverGlyphHoverBackground` |
| 前景（标志符号） | `Tag.TagHoverGlyphHover` |
| 边框 | `Tag.TagHoverGlyphHoverBorder` |

**关闭 (&times;) 标记字形：按下状态**

![按下的关闭 (&times;) 标记标志符号](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303-183_TagGlyphPressed")<br />按下的关闭 (&times;) 标记标志符号

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagHoverGlyphPressedBackground` |
| 前景（标志符号） | `Tag.TagHoverGlyphPressed` |
| 边框 | `Tag.TagHoverGlyphPressedBorder` |

**具有 Close (&times;) 标志符号的选定标记：默认状态**

![默认选定标记 (&times;) 标志符号关闭](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303-184_TagSelected")<br />默认选定标记 (&times;) 标志符号关闭

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（标志符号） | `Tag.TagSelectedGlyph` |

**选定标记 (&times;) 标志符号关闭）：悬停状态**

![&times;悬停时 () 标志符号的选定标记](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303-185_TagSelectedHover")<br />&times;悬停时 () 标志符号的选定标记

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagSelectedGlyphHoverBackground` |
| 前景（标志符号） | `Tag.TagSelectedGlyphHover` |
| 边框 | `Tag.TagSelectedGlyphHoverBorder` |

**选定标记 (&times;) 标志符号：按下状态**

![按下的选定标记 (&times;) 标志符号](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303-186_TagSelectedPressed")<br />按下的选定标记 (&times;) 标志符号

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagSelectedGlyphPressedBackground` |
| 前景（标志符号） | `Tag.TagSelectedGlyphPressed` |
| 边框 | `Tag.TagSelectedGlyphPressedBorder` |

## <a name="tool-windows"></a>工具窗口
无需复制工具窗口，因为它们由 Visual Studio 环境提供。 但是，你可能会决定要利用工具窗口中使用的颜色，以便你的 UI 显示方式始终与这部分 Visual Studio 环境一致。

![工具窗口 (红线) ](../../extensibility/ux-guidelines/media/0303-087_toolwindowredline.png "0303-087_ToolWindowRedline")<br />工具窗口 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建要与工具窗口匹配的 UI 的任何位置。 | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

### <a name="tool-window-frame"></a>工具窗口框架
Visual Studio 中的工具窗口用于许多不同的任务，可以采用多个不同状态中的一个状态存在。 如果工具窗口处于打开状态，则它可以分配到文档区域四边的任何一边。 工具窗口还可以在 IDE 外部浮动，从而使它们可以在用户屏幕中的任何位置重新定位。 浮动窗口始终位于 IDE 顶部。 最后，工具窗口可以作为文档窗口停靠，并显示为文档井中的选项卡。 作为文档窗口停靠的工具窗口会使用文档窗口标记名称进行部分着色。

![工具窗口框架 (红线) ](../../extensibility/ux-guidelines/media/0303-088_toolwindowframeredline.png "0303-088_ToolWindowFrameRedline")<br />工具窗口框架 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ... 在其中创建要与工具窗口匹配的 UI 的任何位置。 | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**停靠工具窗口**

![停靠工具窗口](../../extensibility/ux-guidelines/media/0303-089_toolwindowdocked.png "0303-089_ToolWindowDocked")<br />停靠工具窗口

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowBackground` |
| 边框 | `Environment.ToolWindowBorder` |

**浮动、聚焦的工具窗口**

![浮动、聚焦的工具窗口](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303-090_ToolWindowFocused")<br />浮动、聚焦的工具窗口

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowBackground` |
| 边框 | `Environment.MainWindowActiveDefaultBorder` |

**浮动，失去焦点工具窗口**

![浮动，失去焦点工具窗口](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303-091_ToolWindowUnfocused")<br />浮动，失去焦点工具窗口

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowBackground` |
| 边框 | `Environment.MainWindowInactiveBorder` |

### <a name="toolbox-like-windows"></a>类似工具箱的窗口
工具箱是 Visual Studio 中最常使用的常见工具窗口之一。 它实质上是应用了特殊主题和样式的树控件。

![类似工具箱的窗口 (红线) ](../../extensibility/ux-guidelines/media/0303-189_toolboxredline.png "0303-189_ToolboxRedline")<br />类似工具箱的窗口 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在设计希望始终与 shell 工具箱保持一致的工具窗口时。 | ...对于不类似于工具箱 UI 的任何内容，或者如果不确定 UI 在 shell 工具箱颜色更改时是否会出现问题。 |

**工具箱节点：默认状态**

![默认工具箱父节点](../../extensibility/ux-guidelines/media/0303-190_toolboxparentnode.png "0303-190_ToolboxParentNode")<br />默认工具箱父节点

![默认工具箱子节点](../../extensibility/ux-guidelines/media/0303-191_toolboxchildnode.png "0303-191_ToolboxChildNode")<br />默认工具箱子节点

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolboxContent`<br /> (标题)  |
| 背景 | `Environment.ToolWindowBackground`<br /> (单个项，或整个窗口（如果没有可用控件）)  |
| 边框 | 无 |
| 前景（标志符号） | `Environment.ToolboxContent` |
| 前景（文本） | `Environment.ToolboxContent` |

**工具箱子节点：悬停状态**

![悬停时的工具箱子节点](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br />悬停时的工具箱子节点

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolboxContentMouseOver`<br />仅 (单个项)  |
| 边框 | 无 |
| 前景（文本） | `Environment.ToolboxContentMouseOver`<br />仅 (单个项)  |

**选定的工具箱节点：焦点状态**

![重点，选定的工具箱父节点](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br />重点，选定的工具箱父节点

![重点，选定的工具箱子节点](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br />重点，选定的工具箱子节点

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 边框 | `TreeView.FocusVisualBorder`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 前景（标志符号） | `TreeView.SelectedItemActive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 前景（文本） | `TreeView.SelectedItemActive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |

**选定的工具箱节点：失去焦点状态**

![已选择，失去焦点工具箱父节点](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br />已选择，失去焦点工具箱父节点

![已选择，失去焦点工具箱子节点](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br />已选择，失去焦点工具箱子节点

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 边框 | 无 |
| 前景（标志符号） | `TreeView.SelectedItemInactive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 前景（文本） | `TreeView.SelectedItemInactive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |

### <a name="tool-window-title-bar"></a>工具窗口标题栏
标题栏边框不是真实边框，而是标题栏顶部的粗线。 它的失去焦点状态没有标记名称。

![工具窗口标题栏 (红线) ](../../extensibility/ux-guidelines/media/0303-092_toolwindowtitlebarredline.png "0303-092_ToolWindowTitleBarRedline")<br />工具窗口标题栏 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建要与工具窗口匹配的 UI 的任何位置。 | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**已设定焦点的标题栏**

![已设定焦点的标题栏](../../extensibility/ux-guidelines/media/0303-093_titlebarfocused.png "0303-093_TitleBarFocused")<br />已设定焦点的标题栏

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.TitleBarActiveGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.TitleBarActiveText` |
| 边框 | `Environment.TitleBarActiveBorder`<br /> (设置为与背景相同的颜色 )  |
| 拖拽句柄 | `Environment.TitleBarDragHandleActive` |

**失去焦点的标题栏**

![失去焦点的标题栏](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303-094_TitleBarUnfocused")<br />失去焦点的标题栏

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.TitleBarInactiveGradientBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.TitleBarInactiveText` |
| 边框 | 空值 |
| 拖拽句柄 | `Environment.TitleBarDragHandle` |

#### <a name="tool-window-title-bar-buttons"></a>工具窗口标题栏按钮
![标题栏按钮 (红线) ](../../extensibility/ux-guidelines/media/0303-095_titlebarbuttonredline.png "0303-095_TitleBarButtonRedline")<br />标题栏按钮 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...对于在 UI 中显示的按钮，这些按钮使用工具窗口标题栏中的颜色标记。 | ...对于在其他位置出现的按钮。 |
| | ...在除指定之外的任何背景/前景组合中。 |

**聚焦标题栏按钮：默认状态**

![默认值，重点标题栏按钮](../../extensibility/ux-guidelines/media/0303-096_titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br />默认值，重点标题栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（标志符号） | `Environment.ToolWindowButtonActiveGlyph` |
| 边框 | 空值 |

**失去焦点标题栏按钮：默认状态**

![默认值，失去焦点标题栏按钮](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br />默认值，失去焦点标题栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | 空值 |
| 前景（标志符号） | `Environment.ToolWindowButtonInactiveGlyph` |
| 边框 | 空值 |

**聚焦标题栏按钮：悬停状态**

![悬停时的聚焦标题栏按钮](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br />悬停时的聚焦标题栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonHoverActive` |
| 前景（标志符号） | `Environment.ToolWindowButtonHoverActiveGlyph` |
| 边框 | `Environment.ToolWindowButtonHoverActiveBorder` |

**失去焦点标题栏按钮：悬停状态**

![悬停时的失去焦点标题栏按钮](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br />悬停时的失去焦点标题栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonHoverInactive` |
| 前景（标志符号） | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| 边框 | `Environment.ToolWindowButtonHoverInactiveBorder` |

**聚焦标题栏按钮：按下状态**

![按下的聚焦标题栏按钮](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br />按下的聚焦标题栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonDown` |
| 前景（标志符号） | `Environment.ToolWindowButtonDownActiveGlyph` |
| 边框 | `Environment.ToolWindowButtonDownBorder` |

**失去焦点标题栏按钮：按下状态**

![按下的失去焦点标题栏按钮](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br />按下的失去焦点标题栏按钮

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonDown` |
| 前景（标志符号） | `Environment.ToolWindowButtonDownInactiveGlyph` |
| 边框 | `Environment.ToolWindowButtonDownBorder` |

### <a name="tool-window-tabs"></a>工具窗口选项卡
![工具窗口选项卡 (红线) ](../../extensibility/ux-guidelines/media/0303-102_toolwindowtabredline.png "0303-102_ToolWindowTabRedline")<br />工具窗口选项卡 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建要与工具窗口匹配的 UI 的任何位置。 | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**已选定、已设定焦点的工具窗口选项卡**

![已选定、已设定焦点的工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-103_toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br />已选定、已设定焦点的工具窗口选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabSelectedTab` |
| 前景（文本） | `Environment.ToolWindowTabSelectedActiveText` |
| 边框 | `Environment.ToolWindowTabSelectedBorder`<br /> (设置为与背景相同的颜色 )  |

**已选定、失去焦点的工具窗口选项卡**

![已选定、失去焦点的工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br />已选定、失去焦点的工具窗口选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabSelectedTab` |
| 前景（文本） | `Environment.ToolWindowTabSelectedText` |
| 边框 | `Environment.ToolWindowTabSelectedBorder`<br /> (设置为与背景相同的颜色 )  |

**背景工具窗口选项卡：默认状态**

![默认背景工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br />默认背景工具窗口选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br /> (在 Visual Studio 2013 中设置为相同颜色值的梯度停止点。 )  |
| 前景（文本） | `Environment.ToolWindowTabText` |
| 边框 | `Environment.ToolWindowTabBorder` |

**背景工具窗口选项卡：悬停状态**

![悬停时的背景工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br />悬停时的背景工具窗口选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br /> (在 Visual Studio 2013 中设置为相同颜色值的梯度停止点。 )  |
| 前景（文本） | `Environment.ToolWindowTabMouseOverText` |
| 边框 | `Environment.ToolWindowTabMouseOverBorder`<br /> (设置为与背景相同的颜色 )  |

### <a name="auto-hide-tabs"></a>自动隐藏选项卡

![自动隐藏选项卡 (红线) ](../../extensibility/ux-guidelines/media/0303-107_autohideredline.png "0303-107_AutoHideRedline")自动隐藏选项卡 (红线) 

| 使用 .。。 | 请勿使用 .。。 |
| --- | --- |
| ...在其中创建要与自动隐藏工具窗口选项卡匹配的 UI 的任何位置。 | ...对于不希望在 shell 具有主题更新时自动更改的任何 UI。 |

**自动隐藏选项卡：默认状态**

![默认自动隐藏选项卡](../../extensibility/ux-guidelines/media/0303-108_autohidetab.png "0303-108_AutoHideTab")<br />默认自动隐藏选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.AutoHideTabBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.AutoHideTabText` |
| 边框 | `Environment.AutoHideTabBorder` |

**自动隐藏选项卡：悬停状态**

![悬停时的“自动隐藏”选项卡](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303-109_AutoHideTabHover")<br />悬停时的“自动隐藏”选项卡

| 元素 | 标记名称：Category.color |
| --- | --- |
| 背景 | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />未在主题 UI 中使用此标记 (梯度停止点 )  |
| 前景（文本） | `Environment.AutoHideTabMouseOverText` |
| 边框 | `Environment.AutoHideTabMouseOverBorder` |
