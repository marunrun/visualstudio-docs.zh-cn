---
title: 用于 Visual Studio 共享颜色 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b36b7c123f4da9ca3ab7a6f33a972345cdf70e6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310780"
---
# <a name="shared-colors-for-visual-studio"></a>Visual Studio 的共享的颜色
当您正在设计使用公共 Visual Studio shell 元素的 UI 或希望界面元素将与类似功能一致时，使用包定义文件中现有的标记名称来选择和分配颜色。 这可确保 UI 与整体 Visual Studio 环境保持一致，并确保它在添加或更新主题时自动更新。

本文介绍公共 UI 元素以及它们使用的标记名称（可以在构建类似 UI 时引用这些名称）。 有关如何访问这些颜色标记的特定信息，请参见 [The VSColor Service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。

请确保正确使用标记名称：

- **使用基于功能，不是颜色本身的标记名称。** 公共共享颜色与特定界面元素关联，仅用于相同或类似功能。 例如，不要仅仅因为你喜欢某个已按下组合框的颜色，便将该颜色重复用于旋转进度动画。 组合框和动画的函数不同，以及如果组合框中更改与关联的颜色，则可能不再是合适于动画元素的颜色。 以一致方法使用颜色可帮助使用户适应，防止产生混乱。

- **采用正确组合使用背景和文本颜色。** 要用于文本的背景色具有关联文本颜色。 不要使用为该背景指定的颜色之外的文本颜色。 如果没有关联的文本颜色，不要将该背景色用于期望显示文本的任何图面。 文本和背景色的其他组合可能会导致不可读的界面。

- **使用适合于其位置的控件颜色。** 在某些状态，某些 Visual Studio 控件没有单独的边框和背景色。 而是从它们之后的图面选取这些颜色。 请确保始终使用适合于要在其中放置控件的位置的标记名称。

> [!IMPORTANT]
> 不要使用"起始页"或"Cider。"类别中找到的标记

## <a name="common-shared-controls"></a>公共共享控件

当在功能中使用标准的 Visual Studio 命令栏时，您将有权样式的 shell 控件。 不应重新创建模板这些公共控件。 但是，如果需要构建自定义命令栏，则可能还需要构建自定义控件。 在这种情况下，请确保对以下每个控件使用正常标记名称，以便 UI 与 Visual Studio 的其余部分保持一致。

### <a name="button-controls"></a>按钮控件

![按钮控件红线](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303年 155_ButtonControlRedline")

| 使用... | 请勿使用... |
| --- | --- |
| ...对于您要集成的 Visual Studio 主题 （浅色、 深色、 蓝色或系统高对比度主题） 的文档井中的按钮。 | ...对于将针对不属于 Visual Studio 主题自定义背景显示的按钮。 |

**按钮： 标准状态**

![标准按钮](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03.Button.Standard")<br />标准按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Button | `CommonControls.Button` |
| 按钮边框 | `CommonControls.ButtonBorder` |

**按钮： 默认状态**

![默认按钮](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03.Button.Default")<br />默认按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonDefault` |
| 按钮边框 | `CommonControls.ButtonBorderDefault` |

**按钮： 已禁用的状态**

![禁用的按钮](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03.Button.Disabled")<br />禁用的按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonDisabled` |
| 按钮边框 | `CommonControls.ButtonBorderDisabled` |

**按钮： 悬停状态**

![悬停时的按钮](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03.Button.hover")<br />悬停时的按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonHover` |
| 按钮边框 | `CommonControls.ButtonBorderHover` |

**按钮： 按下的状态**

![按下的按钮](../../extensibility/ux-guidelines/media/03.03.Button.Pressed.png "03.03.Button.Pressed")<br />按下的按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonPressed` |
| 按钮边框 | `CommonControls.ButtonBorderPressed` |

**已设定焦点状态按钮：**

![已设定焦点的按钮](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03.Button.Focused")<br />已设定焦点的按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Button | `CommonControls.ButtonFocused` |
| 按钮边框 | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>复选框控件
![复选框 （红线）](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303年 161_CheckboxRedline")<br />复选框 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...为也包含在文档中的复选框控件。 | ...对于不是复选框控件的任何 UI。 |

**复选框： 这是默认状态**

![Check box](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303-162_Checkbox")<br />默认复选框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackground` |
| Border | `CommonControls.CheckBoxBorder` |
| Text | `CommonControls.CheckBoxText` |
| 标志符号 | `CommonControls.CheckBoxGlyph` |

**复选框： 已禁用状态**

![已禁用的复选框](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303年 163_CheckboxDisabled")<br />已禁用的复选框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundDisabled` |
| Border | `CommonControls.CheckBoxBorderDisabled` |
| Text | `CommonControls.CheckBoxTextDisabled` |
| 标志符号 | `CommonControls.CheckBoxGlyphDisabled` |

**复选框： 将鼠标悬停状态**

 ![悬停时的复选框](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303年 164_CheckboxHover")<br />悬停时的复选框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundHover` |
| Border | `CommonControls.CheckBoxBorderHover` |
| Text | `CommonControls.CheckBoxTextHover` |
| 标志符号 | `CommonControls.CheckBoxGlyphHover` |

**复选框： 按下状态**

![已按下的复选框](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303年 165_CheckboxPressed")<br />已按下的复选框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundPressed` |
| Border | `CommonControls.CheckBoxBorderPressed` |
| Text | `CommonControls.CheckBoxTextPressed` |
| 标志符号 | `CommonControls.CheckBoxGlyphPressed` |

**复选框： 已设定焦点状态**

![已设定焦点的复选框](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303年 166_CheckboxFocused")<br />已设定焦点的复选框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundFocused` |
| Border | `CommonControls.CheckBoxBorderFocused` |
| Text | `CommonControls.CheckBoxTextFocused` |
| 标志符号 | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>下拉列表和组合框
![Drop-down/combo box (redline)](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")<br />下拉/组合框 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...的下拉列表和组合框在文档中良好。 | ...对于不是在下拉列表或组合框中的任何 UI。 |
| | ...的命令栏[下拉列表](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)或[组合框](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)。 |

**下拉列表和组合框： 这是默认状态**

![Default drop-down/combo box](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303-168_DropDownComboBox")<br />默认下拉/组合框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackground` |
| Border | `CommonControls.ComboBoxBorder` |
| Text | `CommonControls.ComboBoxText` |
| Separator | `CommonControls.ComboBoxSeparator` |
| 标志符号 | `CommonControls.ComboBoxGlyph` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackground` |

**下拉列表和组合框： 已禁用状态**

![Disabled drop-down/combo box](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")<br />已禁用的下拉/组合框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundDisabled` |
| Border | `CommonControls.ComboBoxBorderDisabled` |
| Text | `CommonControls.ComboBoxTextDisabled` |
| Separator | `CommonControls.ComboBoxSeparatorDisabled` |
| 标志符号 | `CommonControls.ComboBoxGlyphDisabled` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**下拉列表和组合框： 将鼠标悬停状态**

![悬停时的下拉/组合框](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")<br />悬停时的下拉/组合框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundHover` |
| Border | `CommonControls.ComboBoxBorderHover` |
| Text | `CommonControls.ComboBoxTextHover` |
| Separator | `CommonControls.ComboBoxSeparatorHover` |
| 标志符号 | `CommonControls.ComboBoxGlyphHover` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundHover` |

**下拉列表和组合框： 按下状态**

![Pressed drop-down/combo box](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")<br />按下的下拉/组合框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundPressed` |
| Border | `CommonControls.ComboBoxBorderPressed` |
| Text | `CommonControls.ComboBoxTextPressed` |
| Separator | `CommonControls.ComboBoxSeparatorPressed` |
| 标志符号 | `CommonControls.ComboBoxGlyphPressed` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**下拉列表和组合框列表项视图： 按下状态**

 ![按下的列表项视图中的下拉/组合框](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")<br />按下的列表项视图中的下拉/组合框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| Border | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| 项文本 | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| 背景阴影 | `CommonControls.ComboBoxListBackgroundShadow` |

**下拉列表和组合框： 已设定焦点状态**

![下拉/组合框的焦点](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")<br />具有焦点的下拉/组合框

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.ComboBoxBackgroundFocused` |
| Border | `CommonControls.ComboBoxBorderFocused` |
| Text | `CommonControls.ComboBoxTextFocused` |
| Separator | `CommonControls.ComboBoxSeparatorFocused` |
| 标志符号 | `CommonControls.ComboBoxGlyphFocused` |
| 标志符号背景 | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**下拉列表和组合框： 文本输入所选内容**

![下拉/组合框文本输入所选内容](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303年 173_DropDownComboBoxTextInput")<br />下拉/组合框文本输入的选择

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 突出显示 | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>表格数据（网格）控件
表格数据控件（也称为网格控件）是可以用于在多列中呈现大量数据的 Visual Studio 公共控件。 可以在 Visual Studio 中的多个位置中找到标准表格数据控件：错误列表工具窗口、IntelliTrace 报告和内存堆视图及其他位置。 始终使用提供的标准表格数据控件。 在某些极少数情况下，你可能无法访问标准表格数据控件。 在这些情况下，请使用以下标记名称以确保 UI 与 Visual Studio 中的其他表格数据控件保持一致。

![表格的数据网格控件 （红线）](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303年 197_TabularDataGridControlRedline")<br />表格的数据网格控件 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...的表格或网格控件。 | ...对于不是表格或网格控件的任何 UI。 |

#### <a name="column-headers"></a>列标题
列标题由背景、边框、标题文本和可选标志符号（通常在网格按该列进行排序时使用）组成。

**列标题： 这是默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Header.Default` |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（标志符号） | `Header.Glyph` |
| Border | `Header.SeparatorLine` |

**列标题： 将鼠标悬停状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Header.MouseOver` |
| 前景（文本） | `Environment.CommandBarTextHover` |
| 前景（标志符号） | `Header.MouseOverGlyph` |
| Border | `Header.SeparatorLine` |

**列标题： 按下状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `CommonControls.CheckBoxBackgroundPressed` |
| 前景（文本） | `CommonControls.CheckBoxBorderPressed` |
| 前景（标志符号） | `CommonControls.CheckBoxTextPressed` |
| Border | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>列表视图项
 列表视图项由背景和内容组成。 内容可以是文本、图标或两者。

**列表视图项： 这是默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 透明 |
| 前景（文本） | `Environment.CommandBarTextActive` |
| Border | None |

**列表视图项： 活动状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive` |
| 前景（文本） | `TreeView.SelectedItemActiveText` |
| Border | None |

**列表视图项： 非活动状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive` |
| 前景（文本） | `TreeView.SelectedItemInactiveText` |
| Border | None |

### <a name="ui-text"></a>UI 文本

#### <a name="instructional-text"></a>说明文本
说明文本提供了要执行的操作的对话框或文档页面中的突出主要说明。

![默认的说明文本](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />默认的说明文本

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>辅助说明文本
在具有大量文本和控件的文档页，某些说明文本使用不同的颜色值。 这有助于传达哪些信息是最重要并降低总体密度的 UI 元素。 (另请参阅下面有关提示文本的部分。)

![辅助说明文本](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />辅助说明文本

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>提示文本
在下一个控件，或向用户显示下一步操作的空文档图面上的空控件将显示提示文本。 您可以使用窗口或控件的背景提示文本。

**默认提示文本**

![默认提示文本](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />默认提示文本

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Environment.ControlEditHintText` |

**所需的提示文本**

![所需的提示文本](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />所需的提示文本

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Environment.ControlRequiredHintText` |
| 背景 | `Environment.ControlRequiredBackground` |

**搜索框控件文本**

> 请参阅[搜索框](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes)的搜索控件与其他颜色标记。

![搜索框控件文本](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />搜索框控件文本

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>超链接
超链接是一个没有前景/背景对的控件。 在所有情况下，使用的超链接前景色，这会在黑色、 灰色，和白色背景上正确显示。 如果在未使用的颜色标记进行超链接控件，您将看到的默认系统颜色"按下"，这将以红色闪烁。 这是控件不使用正确的环境颜色标记的信号。

![Hyperlink (redline)](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303-133_HyperlinkRedline")<br />超链接 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当你需要创建自定义超链接。 | ...的任何内容，不是一个超链接。 |

**超链接： 默认状态**

![默认超链接](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303年 134_Hyperlink")<br />默认超链接

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlink` |

**超链接： 悬停状态**

![悬停时的超链接](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303年 135_HyperlinkHover")<br />悬停时的超链接

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlinkHover` |

**超链接： 按下的状态**

![按下的超链接](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303年 136_HyperlinkPressed")<br />按下的超链接

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlinkPressed` |

**超链接： 已禁用的状态**

![已禁用的超链接](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303年 137_HyperlinkDisabled")<br />已禁用的超链接

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>信息栏
信息栏用于提供有关给定上下文的详细信息，始终出现在文档窗口或工具窗口顶部。

![Infobar (redline)](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303-138_InfobarRedline")<br />信息栏 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...时创建自定义信息栏。 | ...的不是类似于一个信息栏的 UI 元素。 |

**信息栏： 默认状态**

![默认信息栏](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303年 139_Infobar")<br />默认信息栏

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.InfoBarBackground` |
| 前景（文本） | `InfoBar.InfoBar` |
| Border | `InfoBar.InfoBarBorder` |

**信息栏关闭 (&times;) 按钮： 这是默认状态**

![默认关闭信息栏 (&times;) 按钮](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />默认关闭信息栏 (&times;) 按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.CloseButton` |
| Border | `InfoBar.CloseButtonBorder` |
| 标志符号 | `InfoBar.CloseButtonGlyph` |

**信息栏关闭 (&times;) 按钮： 将鼠标悬停状态**

![信息栏关闭 (&times;) 按钮上悬停](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />信息栏关闭 (&times;) 悬停按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.CloseButtonHover` |
| Border | `InfoBar.CloseButtonHoverBorder` |
| 标志符号 | `InfoBar.CloseButtonHoverGlyph` |

**信息栏关闭 (&times;) 按钮： 按下状态**

![按下关闭信息栏 (&times;) 按钮](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />按下关闭信息栏 (&times;) 按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.CloseButtonDown` |
| Border | `InfoBar.CloseButtonDownBorder` |
| 标志符号 | `InfoBar.CloseButtonDownGlyph` |

**信息栏超链接按钮： 这是默认状态**

![默认信息栏超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />默认信息栏超链接按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `InfoBar.Hyperlink` |

**信息栏超链接按钮： 将鼠标悬停状态**

![悬停时的信息栏超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />悬停时的信息栏超链接按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Infobar.HyperlinkMouseOver`<br />（使用下划线） |

**信息栏超链接按钮： 按下状态**

![按下的信息栏超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />按下的信息栏超链接按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Infobar.HyperlinkMouseDown`<br />（使用下划线） |

**信息栏内联超链接 （在一个句子）： 这是默认状态**

![默认内联信息栏超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />默认内联信息栏超链接按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `InfoBar.Hyperlink` |

**（在一个句子） 信息栏内联超链接： 将鼠标悬停状态**

![悬停时的信息栏内联超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />悬停时的信息栏内联超链接按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Infobar.HyperlinkMouseOver`<br />（使用下划线） |

**信息栏内联超链接 （在一个句子）： 按下状态**

![按下的信息栏内联超链接按钮](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />按下的信息栏内联超链接按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景 （文本） | `Infobar.HyperlinkMouseDown`<br />（使用下划线） |

**信息栏按钮： 这是默认状态**

![默认信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />默认信息栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.Button` |
| 前景 （文本） | `InfoBar.Button` |
| Border | `InfoBar.ButtonBorder` |

**信息栏按钮： 将鼠标悬停状态**

![悬停时的信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />悬停时的信息栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonMouseOver` |
| 前景 （文本） | `InfoBar.ButtonMouseOver` |
| Border | `InfoBar.ButtonMouseOverBorder` |

**信息栏按钮： 按下状态**

![按下的信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />按下的信息栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonMouseDown` |
| 前景 （文本） | `InfoBar.ButtonMouseDown` |
| Border | `InfoBar.ButtonMouseDownBorder` |

**信息栏按钮： 已禁用状态**

![已禁用信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />已禁用信息栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonDisabled` |
| 前景 （文本） | `InfoBar.ButtonDisabled` |
| Border | `InfoBar.ButtonDisabledBorder` |

**信息栏按钮： 已设定焦点状态**

![已设定焦点的信息栏按钮](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />已设定焦点的信息栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `InfoBar.ButtonFocus` |
| 前景 （文本） | `InfoBar.ButtonFocus` |
| Border | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>滚动条
滚动条样式由 Visual Studio 环境中，且无需主题化。 但是，你可能决定你想要利用滚动条中使用，因此，UI 显示方式始终与这部分 Visual Studio 环境一致的颜色。

![滚动条 （红线）](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303年 140_ScrollbarRedline")<br />滚动条 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当你要创建 UI，您希望匹配 Visual Studio 滚动条。 | ...的任何内容不想要始终匹配滚动条 UI。 |

**滚动条： 这是默认状态**

![默认滚动条](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303年 141_Scrollbar")<br />默认滚动条

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 滚动条 | `Environment.ScrollBarBackground` |
| 前景（缩略） | `Environment.ScrollBarThumbBackground` |

**滚动条： 将鼠标悬停状态**

![悬停时的滚动条](../../extensibility/ux-guidelines/media/0303-143_scrollbarhover.png "0303年 143_ScrollbarHover")<br />悬停时的滚动条

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 滚动条 | `Environment.ScrollBarBackground` |
| 前景（缩略） | `Environment.ScrollBarThumbMouseOverBackground` |

*滚动条： 按下状态**

![按下的滚动条](../../extensibility/ux-guidelines/media/0303-145_scrollbarpressed.png "0303年 145_ScrollbarPressed")<br />按下的滚动条

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 滚动条 | `Environment.ScrollBarBackground` |
| 前景（缩略） | `Environment.ScrollBarThumbPressedBackground` |

**滚动条箭头： 这是默认状态**

![默认滚动条箭头](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303年 142_ScrollbarArrow")<br />默认滚动条箭头

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ScrollBarArrowBackground`<br />（设置为与滚动条相同的颜色。） |
| 前景（标志符号） | `Environment.ScrollBarArrowGlyph` |

**滚动条箭头： 将鼠标悬停状态**

![滚动条箭头上悬停](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303年 144_ScrollbarArrowHover")<br />悬停时的滚动条箭头

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ScrollBarArrowMouseOverBackground`<br />（设置为与滚动条相同的颜色。） |
| 前景（标志符号） | `Environment.ScrollBarArrowGlyphMouseOver` |

**滚动条箭头： 按下状态**

![按下的滚动条箭头](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303年 146_ScrollbarArrowPressed")<br />按下的滚动条箭头

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ScrollBarArrowPressedBackground`<br />（设置为与滚动条相同的颜色。） |
| 前景（标志符号） | `Environment.ScrollBarArrowGlyphPressed` |

### <a name="BKMK_SearchBoxes"></a>搜索框
只要可能，便使用 Visual Studio 环境提供的公共搜索控件。 搜索框颜色位于 **ShellColors.pkgdef** 文件中“SearchControl”类别中，该文件包含输入字段、操作按钮、下拉按钮和下拉菜单中的标记名称。

搜索框可以具有多种状态之一，其中一些状态互相排斥：

- “已设定焦点”或“失去焦点”是指光标是否处于文本框中。

- “活动”或“非活动”是指用户是否在文本框中输入了搜索查询。

- “悬停”表示用户将鼠标指针置于搜索框上方（此状态优先于所有其他状态）。

- “已禁用”表示为当前上下文关闭了搜索功能。

![搜索框 （红线）](../../extensibility/ux-guidelines/media/0303-110_searchboxredline.png "0303年 110_SearchBoxRedline")<br />搜索框 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当你设计一个自定义搜索框。 | ...的不是搜索框中的任何内容。 |
| | ...的任何不想要始终与搜索匹配的内容框 UI。 |

**已设定焦点的搜索输入的字段**

![已设定焦点的搜索输入的字段](../../extensibility/ux-guidelines/media/0303-111_searchinputfieldfocused.png "0303年 111_SearchInputFieldFocused")<br />已设定焦点的搜索输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.FocusedBackground` |
| 前景（文本） | `SearchControl.FocusedBackground` |
| Border | `SearchControl.FocusedBorder` |
| Separator | `SearchControl.FocusedDropDownSeparator` |

**失去焦点，处于活动状态的搜索输入的字段**

![失去焦点的搜索输入的字段](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303年 114_SearchInputFieldUnfocused")<br />失去焦点，处于活动状态的搜索输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.SearchActiveBackground` |
| 前景（文本） | `SearchControl.SearchActiveBackground` |
| Border | `SearchControl.UnfocusedBorder` |
| Separator | `SearchControl.DropDownSeparator` |

**失去焦点的非活动搜索输入的字段**

![失去焦点的非活动搜索输入的字段](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303年 114 1_SearchInputFieldUnfocusedInactive")<br />失去焦点的非活动搜索输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.Unfocused` |
| 前景（文本） | `SearchControl.Unfocused` |
| Border | `SearchControl.UnfocusedBorder` |
| Separator | `SearchControl.DropDownSeparator` |

**突出显示的搜索输入的字段 （纯文本）**

![突出显示的搜索输入的字段](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303年 120_SearchInputFieldHighlight")<br />突出显示的搜索输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.Selection` |
| 前景（文本） | `SearchControl.FocusedBackground` |
| Border | None |
| Separator | `SearchControl.FocusedDropDownSeparator` |

**已禁用的搜索输入的字段**

![禁用搜索输入的字段](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303年 121_SearchInputFieldDisabled")<br />已禁用的搜索输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.Disabled` |
| 前景（文本） | `SearchControl.Disabled` |
| Border | `SearchControl.DisabledBorder` |
| Separator | `SearchControl.DropDownSeparator` |

**已设定焦点的搜索操作按钮**

![已设定焦点的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303年 112_SearchActionButtonFocused")<br />已设定焦点的搜索操作按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（搜索标志符号） | `SearchControl.SearchGlyph` |
| 前景（停止标志符号） | `SearchControl.StopGlyph` |
| 前景（清除标志符号） | `SearchControl.ClearGlyph` |
| Border | 不适用 |

**失去焦点的搜索操作按钮**

![失去焦点的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303年 115_SearchActionButtonUnfocused")<br />失去焦点的搜索操作按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（搜索标志符号） | `SearchControl.SearchGlyph` |
| 前景（停止标志符号） | `SearchControl.StopGlyph` |
| 前景（清除标志符号） | `SearchControl.ClearGlyph` |
| Border | 不适用 |

**按下的搜索操作按钮**

![按下的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303年 116 1_SearchActionButtonPressed")<br />按下的搜索操作按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.ActionButtonMouseDown` |
| 前景（标志符号） | `SearchControl.ActionButtonMouseDownGlyph` |
| Border | `SearchControl.ActionButtonMouseDownBorder` |

**已禁用的搜索操作按钮**

![禁用的搜索操作按钮](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303年 122_SearchActionButtonDisabled")<br />已禁用的搜索操作按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（标志符号） | `SearchControl.ActionButtonDisabledGlyph` |
| Border | None |

**已设定焦点的搜索下拉按钮**

![已设定焦点的搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303年 113_SearchDropdownButtonFocused")<br />已设定焦点的搜索下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.FocusedDropDownButton` |
| 前景（标志符号） | `SearchControl.FocusedDropDownButtonGlyph` |
| Border | `SearchControl.FocusedDropDownButtonBorder` |

**失去焦点的搜索下拉按钮**

![失去焦点的搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303年 116_SearchDropdownButtonUnfocused")<br />失去焦点的搜索下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.UnfocusedDropDownButton` |
| 前景（标志符号） | `SearchControl.UnfocusedDropDownButtonGlyph` |
| Border | `SearchControl.UnfocusedDropDownButtonBorder` |

**按下的搜索下拉按钮**

![按下的搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303年 116 2_SearchDropdownButtonPressed")<br />按下的搜索下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.MouseDownDropDownButton` |
| 前景（标志符号） | `SearchControl.MouseDownDropDownButtonGlyph` |
| Border | `SearchControl.MouseDownDropDownButtonBorder` |

**已禁用的搜索下拉按钮**

![禁用搜索下拉按钮](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303年 123_SearchDropdownButtonDisabled")<br />已禁用的搜索下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（标志符号） | `SearchControl.DisabledDownButtonGlyph` |
| Border | None |

#### <a name="search-drop-down-lists"></a>搜索下拉列表
搜索框下拉菜单中有可能要比在 Visual Studio 中其他下拉菜单稍微复杂。 "建议的搜索"和"搜索选项"部分可以显示单独或一起使用的菜单中，并且每个分别进行着色。 当这两个部分一起出现时，还会有一条线分隔它们，并且有一个边框环绕整个下拉菜单。

![搜索下拉列表 （红线）](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303年 124_SearchDropdownRedline")<br />搜索下拉列表 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当创建自定义搜索下拉列表。 | ...为显示在其他上下文中的下拉列表。 |
| ...的正确列表组件的正确标记名称。 | ...在未指定任何背景/前景组合。 |

**搜索下拉列表元素**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| Border | `SearchControl.PopupBorder` |
| Separator | `SearchControl.PopupSectionHeaderSeparator` |
| 阴影 | `Environment.DropShadowBackground` |

**建议的搜索： 这是默认状态**

![默认建议的搜索](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303年 125_SearchSuggested")<br />默认建议的搜索

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `SearchControl.PopupItemText` |

**建议的搜索： 将鼠标悬停状态**

![建议的搜索悬停](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303年 128_SearchSuggestedHover")<br />悬停时的建议的搜索

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `SearchControl.PopupMouseOverItemText` |
| Border | `SearchControl.PopupControlMouseOverBorder` |

**搜索选项： 这是默认状态**

![搜索复选框](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303年 126_SearchCheckbox")<br />默认搜索选项 （复选框）

![搜索选项](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303年 127_SearchOptions")<br />默认搜索选项 （链接）

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupSectionBackgroundGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（复选框文本） | `SearchControl.PopupCheckboxText` |
| 前景（链接文本） | `SearchControl.PopupButtonText` |
| 标题背景 | `SearchControl.PopupSectionHeaderGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（标题文本） | `SearchControl.PopupSectionHeaderText` |

**搜索选项： 将鼠标悬停状态**

![悬停时的搜索选项 （复选框）](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303年 129_SearchCheckboxHover")<br />悬停时的搜索选项 （复选框）

![悬停时的搜索选项 （链接）](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303年 130_SearchOptionsHover")<br />悬停时的搜索选项 （链接）

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（复选框文本） | `SearchControl.PopupCheckboxMouseDownText` |
| 前景（链接文本） | `SearchControl.PopupButtonMouseDownText` |
| Border | `SearchControl.PopupControlMouseOverBorder` |

**搜索选项： 按下状态**

![按下的搜索选项 （复选框）](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303年 131_SearchSuggestedPressed")<br />按下的搜索选项 （复选框）

![按下的搜索选项 （链接）](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303年 132_SearchOptionsPressed")<br />按下的搜索选项 （链接）

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 复选框背景 | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（复选框文本） | `SearchControl.PopupCheckboxMouseDownText` |
| 链接背景 | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（链接文本） | `SearchControl.PopupButtonMouseDownText` |

### <a name="BKMK_TreeView"></a> 树视图
多个工具窗口，其中包括解决方案资源管理器、 服务器资源管理器和类视图实现其颜色控制中的颜色名称的分层组织方案`TreeView`类别。 树视图中的所有项都具有背景和文本颜色。 具有嵌套子元素的项还具有指示该项是展开还是折叠的标志符号。

![树视图 （红线）](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303年 147_TreeViewRedline")<br />树视图 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...您需要实现分层组织视图的任何位置。 | ...对于不类似于树视图的任何内容。 |
| | ...在未指定任何背景/前景组合。 |

**树视图项： 这是默认状态**

![默认树视图项](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303年 148_TreeView")<br />默认树视图项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.Background` |
| 前景（文本） | `TreeView.Background` |
| 前景（标志符号） | `TreeView.Glyph` |
| Border | None |

**树视图项： 将鼠标悬停状态**

![悬停时的树视图项](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303年 149_TreeViewHover")<br />悬停时的树视图项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.Background` |
| 前景（文本） | `TreeView.Background` |
| 前景（标志符号） | `TreeView.GlyphMouseOver` |
| Border | None |

**树视图项： 拖动状态**

![通过树视图项上拖动](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303年 150_TreeViewDragOver")<br />在树视图项拖动到

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.DragOverItem` |
| 前景（文本） | `TreeView.DragOverItem` |
| 前景（标志符号） | `TreeView.DragOverItemGlyph` |
| Border | None |

**树视图项： 选择、 已设定焦点状态**

![选择和已设定焦点的树视图项](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303年 151_TreeViewFocused")<br />所选已设定焦点的树视图项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive` |
| 前景（文本） | `TreeView.SelectedItemActive` |
| 前景（标志符号） | `TreeView.SelectedItemActiveGlyph` |
| Border | `TreeView.FocusVisualBorder` |

**树视图项： 已选定、 失去焦点的状态**

![所选和失去焦点的树视图项](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303年 152_TreeViewUnfocused")<br />所选和失去焦点的树视图项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive` |
| 前景（文本） | `TreeView.SelectedItemInactive` |
| 前景（标志符号） | `TreeView.SelectedItemInactiveGlyph` |
| Border | None |

**树视图项： 悬停，则选择，并已设定焦点状态**

![选择和树视图项侧重于悬停](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303年 153_TreeViewFocusedHover")<br />悬停时的所选且其焦点位于树视图项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive` |
| 前景（文本） | `TreeView.SelectedItemActive` |
| 前景（标志符号） | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Border | `TreeView.FocusVisualBorder` |

**树视图项： 悬停、 选定，和失去焦点状态**

![悬停时的所选和失去焦点的树视图项](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303年 154_TreeViewUnfocusedHover")<br />悬停时的所选和失去焦点的树视图项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive` |
| 前景（文本） | `TreeView.SelectedItemInactive` |
| 前景（标志符号） | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Border | None |

## <a name="shell-appearance"></a>Shell 外观

### <a name="background"></a>背景
环境背景由两层组成。 下层是覆盖整个 IDE 的纯色。 上层位于命令架下，以及 IDE 左边缘和右边缘上的工具窗口自动隐藏通道之间。 顶部和底部背景图层设置为浅色和深色主题中的相同颜色。

![Visual Studio shell 背景 （红线）](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303年 187_ShellBackgroundRedline")<br />Visual Studio shell 背景 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...为你想要与 Visual Studio 环境背景匹配的位置。 | ...为不是背景图面的位置的填充。 |
| | ...作为背景上放置前景元素。 |

**底部层 shell 外观**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.EnvironmentBackground` |

**上面的图层 shell 外观**

> 在 Visual Studio 2013 浅色和深色主题中设置为相同颜色值的梯度停止点。

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |

### <a name="command-shelf"></a>命令架
有两组标记名称用于命令架背景：一组用于菜单栏所在的位置，另一组用于命令栏所在的位置。 单个命令栏组具有自己的背景色值（在“命令栏”部分中进行更详细的讨论）。 菜单栏和命令栏文本分别在菜单和命令栏部分中进行了讨论。

![Visual Studio 命令架 （红线）](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303年 188_CommandShelfRedline")<br />Visual Studio 命令架 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...的放置菜单或工具栏的区域。 | ...的不是类似于命令架的区域。 |
|...与正确的背景/前景标记名称组合。 | |

**命令架菜单栏**

> 在 Visual Studio 2013 浅色和深色主题中设置为相同颜色值的梯度停止点。

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

**命令架命令栏**

> 在 Visual Studio 2013 浅色和深色主题中设置为相同颜色值的梯度停止点。

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>清单设计器
清单设计器旨在作为可用于更加轻松地在 Windows 8 和 Windows Phone 8 项目中编辑清单文件的方法。 虽然没有可供使用的共享框架，不过匹配方向/导航选项卡和整体结构的设计布局和颜色是合适的。 有关布局详细信息的更多信息，请参见 [Layout for Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md)。

![清单设计器 （红线）](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303年 175_ManifestDesignerRedline")<br />清单设计器 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...的设计器的类似于清单设计器。 | ...如果有多个六个选项卡。 |
| ...来代替使用公共选项卡控件在文档中的编辑器顶部嗯。 | ...对于不结构类似于清单设计器的任何 UI。 |

**清单设计器选择的选项卡： 这是默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.TabActive` |
| Border | None |

**清单设计器所选的说明窗格： 这是默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.DescriptionPane` |

**清单设计器所选内容页： 默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.Background` |
| 对话框帮助程序文本 | `ManifestDesigner.WatermarkText`<br />（此标记名称不匹配其功能。） |

**清单设计器选项卡： 未选中状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.Tab.Inactive` |

**清单设计器选项卡： 将鼠标悬停状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>命令结构

### <a name="BKMK_CommandMenus"></a> 菜单
菜单可以出现在 Visual Studio 的多个位置上： 主菜单栏、 嵌入在文档或工具窗口或整个 IDE 的各个位置右键单击。 与其他 UI 元素关联的菜单的实现在针对相应元素的部分中进行讨论。 应始终使用由 Visual Studio 环境提供的标准菜单实现。 但是，在某些极少数情况下，你可能无法访问标准 Visual Studio 菜单。 在这些情况下，请使用以下标记名称以确保 UI 与 Visual Studio 中的其他菜单保持一致。

![Visual Studio 菜单 （红线）](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303年 000_MenuRedline")<br />Visual Studio 菜单 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当你需要创建自定义菜单。| ...单独的背景色。 始终使用指定的背景/前景组合。 |
| ...当具有你想要与 Visual Studio 菜单匹配的新 UI 组件。| |

#### <a name="menu-titles"></a>菜单标题
菜单标题由背景、边框和标题文本以及可选的标志符号（通常是在菜单位于命令栏中使用）组成。

![菜单标题 （红线）](../../extensibility/ux-guidelines/media/0303-001_menutitleredline.png "0303年 001_MenuTitleRedline")<br />菜单标题 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...每当你要创建自定义菜单标题。 | ...对于不想要始终与菜单标题匹配的任何内容。 |
| | ...在未指定任何背景/前景组合。 |

**菜单标题： 这是默认状态**

![默认的菜单标题](../../extensibility/ux-guidelines/media/0303-002_menutitledefault.png "0303年 002_MenuTitleDefault")<br />默认的菜单标题

![默认的具有字形的菜单标题](../../extensibility/ux-guidelines/media/0303-003_menutitlewithglyphdefault.png "0303年 003_MenuTitleWithGlyphDefault")<br />默认的具有字形的菜单标题

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景 （文本） | `Environment.CommandBarTextActive` |
| 前景 （标志符号） | `Environment.CommandBarMenuGlyph` |
| Border | None |

**菜单标题： 将鼠标悬停状态**

![悬停时的菜单标题](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303年 004_MenuTitleHover")<br />悬停时的菜单标题

![菜单标题的具有字形的悬停](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303年 005_MenuTitleWithGlyphHover")<br />悬停时的具有字形的菜单标题

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景 （文本） | `Environment.CommandBarTextHover` |
| 前景 （标志符号） | `Environment.CommandBarMenuMouseOverGlyph` |
| Border | `Environment.CommandBarBorder` |

**菜单标题： 按下状态**

![按下的菜单标题](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303年 006_MenuTitlePressed")<br />按下的菜单标题

![按下的具有字形的菜单标题](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303年 007_MenuTitleWithGlyphPressed")<br />按下的具有字形的菜单标题

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（标志符号） | `Environment.CommandBarMenuMouseDownGlyph` |
| Border | `Environment.CommandBarMenuBorder`<br />（仅限左侧、 顶部和左右两边。） |

**菜单标题： 已禁用状态**

![禁用的具有字形的菜单标题](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303年 008_MenuTitleWithGlyphDisabled")<br />已禁用的菜单标题与标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（文本） | `Environment.CommandBarTextInactive` |
| 前景（标志符号） | `Environment.CommandBarTextInactive` |
| Border | None |

#### <a name="menu-items"></a>菜单项
各个菜单项由菜单文本和可选的图标、复选框或子菜单标志符号组成。 其背景和文本颜色会在鼠标悬停在上方时更改。 此颜色标记是前景/背景对。

![菜单项红线](../../extensibility/ux-guidelines/media/0303-009_menuitemredline.png "0303年 009_MenuItemRedline")

| 使用... | 请勿使用... |
|---|---|
| ...的任何下拉列表，从启动菜单栏或命令栏。 | ...的另一个上下文中的任何下拉列表。 |
| | ...在未指定任何背景/前景组合。 |

**菜单项： 这是默认状态**

![默认菜单项](../../extensibility/ux-guidelines/media/0303-010_menudefault.png "0303年 010_MenuDefault")<br />默认菜单项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMenuBackgroundGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（子菜单标志符号） | `Environment.CommandBarMenuSubmenuGlyph` |
| Border | `Environment.CommandBarMenuBorder` |
| 图标通道背景 | `Environment.CommandBarMenuIconBackground` |
| Separator | `Environment.CommandBarMenuSeparator` |
| 阴影 | `Environment.DropShadowBackground` |

**菜单项： 选中和选定状态**

![选中的菜单](../../extensibility/ux-guidelines/media/0303-011_menuchecked.png "0303年 011_MenuChecked")<br />选中的菜单项

![选定的菜单](../../extensibility/ux-guidelines/media/0303-012_menuselected.png "0303年 012_MenuSelected")<br />所选的菜单项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 选中标记 | `Environment.CommandBarCheckBox` |
| 复选标记背景 | `Environment.CommandBarSelectedIcon` |
| 图标背景 | `Environment.CommandBarSelected` |
| 图标边框 | `Environment.CommandBarSelectedBorder` |

**菜单项： 将鼠标悬停状态**

![Menu hover](../../extensibility/ux-guidelines/media/0303-013_menuhover.png "0303-013_MenuHover")<br />悬停时的菜单项

![选中的菜单悬停](../../extensibility/ux-guidelines/media/0303-014_menuhoverchecked.png "0303年 014_MenuHoverChecked")<br />检查悬停时的菜单项

![选定的菜单悬停](../../extensibility/ux-guidelines/media/0303-015_menuhoverselected.png "0303年 015_MenuHoverSelected")<br />悬停时的选定的菜单项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMenuItemMouseOver` |
| 前景（文本） | `Environment.CommandBarMenuItemMouseOver` |
| 前景（子菜单标志符号） | `Environment.CommandBarMenuMouseOverSubmenuGlyph` |
| 选中标记 | `Environment.CommandBarCheckBoxMouseOver` |
| 复选标记背景 | `Environment.CommandBarHoverOverSelectedIcon` |
| 图标背景 | `Environment.CommandBarHoverOverSelected` |
| 图标边框 | `Environment.CommandBarHoverOverSelectedIconBorder` |

**菜单项： 已禁用状态**

![禁用的菜单](../../extensibility/ux-guidelines/media/0303-016_menudisabled.png "0303年 016_MenuDisabled")<br />已禁用的菜单项

![选中的禁用的菜单](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303年 017_MenuDisabledChecked")<br />带有复选标记的已禁用的菜单项

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 前景（文本） | `Environment.CommandBarTextInactive` |
| 前景（子菜单标志符号） | `Environment.CommandBarMenuSubmenuGlyph` |
| 选中标记 | `Environment.CommandBarCheckBoxDisabled` |
| 复选标记背景 | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>命令栏
命令栏可以出现在多个位置中 Visual Studio IDE 中，最值得注意的是命令架以及嵌入在工具或文档窗口。

一般而言，需始终使用由 Visual Studio 环境提供的标准命令栏实现。 使用标准机制可确保所有视觉细节都正确显示，并且交互元素的行为与其他 Visual Studio 命令栏控件一致。 但是，如果你需要构建自己的命令栏，请确保使用以下标记名称正确设计其样式。

![命令栏红线](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303年 018_CommandBarRedline")<br />命令栏 （红线）

![溢出按钮红线](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303年 019_OverflowButtonRedline")<br />溢出按钮 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...在需要嵌入式的命令栏的位置，但不能使用标准 Visual Studio 命令栏实现。 | ...的不是类似于命令栏的 UI 元素。 |
| | ...的命令栏组件不是在为其指定的标记名称。 |

#### <a name="command-bar-groups"></a>命令栏组
命令栏组由一组相关命令栏控件组成，可能包含任何数量的按钮、拆分按钮、下拉菜单、组合框或菜单。 这些控件的颜色通过单独的标记名称进行控制，在本指南中的其他位置单独进行了讨论。 分隔线用于将命令栏组划分为相关子组。

![命令栏组红线](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303年 020_CommandBarGroupRedline")<br />命令栏组 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...在需要嵌入式的命令栏的位置，但不能使用标准 Visual Studio 命令栏实现。 | ...的不是类似于命令栏的 UI 元素。 |
| | ...的命令栏组件不是在为其指定的标记名称。 |

**命令栏组： 这是默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| Border | `Environment.CommandBarToolBarBorder` |
| 拖动句柄 | `Environment.CommandBarDragHandle` |
| Separator | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>命令图标
![命令图标红线](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303年 021_CommandIconRedline1")<br />命令图标 （红线）

![使用文本命令图标红线](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303年 022_CommandIconRedline2")<br />使用文本命令图标 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...的任何按钮并将其放置在命令栏上。 | ...的控件的具有其自己的标记名称。 |
| | ...在未指定任何背景/前景组合。 |

**命令图标： 这是默认状态**

![命令图标默认值](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303年 023_CommandIconDefault")<br />默认命令图标

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用（从命令栏背景继承） |
| 前景（文本） | `Environment.CommandBarTextActive` |
| Border | 不适用 |

**命令图标： 默认选择的状态**

![默认情况下，所选的命令图标](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303年 024_CommandIconDefaultSelected")<br />默认情况下，所选的命令图标

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarSelected` |
| 前景（文本） | `Environment.CommandBarTextSelected` |
| Border | `Environment.CommandBarSelectedBorder` |

**命令图标： 悬停或焦点状态**

![命令图标上悬停或焦点](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303年 025_CommandIconHover")<br />悬停或焦点上的命令图标

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.CommandBarTextHover` |
| Border | `Environment.CommandBarBorder` |

**命令图标： 悬停或焦点状态，选择**

![选择命令图标上悬停或焦点](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303年 026_CommandIconHoverSelected")<br />所选的命令图标上悬停或焦点

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarHoverOverSelected` |
| 前景（文本） | `Environment.CommandBarTextHoverOverSelected` |
| Border | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **命令图标： 按下状态**

![按下命令图标](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303年 027_CommandIconPressed")<br />已按下命令图标

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseDownBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.CommandBarTextMouseDown` |
| Border | `Environment.CommandBarBorder` |

**命令图标： 已禁用状态**

![已禁用的命令图标](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303年 028_CommandIconDisabled")<br />已禁用命令图标

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用（从命令栏背景继承） |
| 前景（文本） | `Environment.CommandBarTextInactive` |
| Border | 不适用 |

#### <a name="BKMK_CommandComboBox"></a> 命令栏组合框

> [!IMPORTANT]
> 组合框类似于下拉列表，但包含一个可编辑文本区域。 如果下拉列表不包含可编辑文本区域，使用的颜色标记[命令栏下拉列表确定](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)。

![命令栏组合框红线](../../extensibility/ux-guidelines/media/0303-029_comboboxredline.png "0303年 029_ComboBoxRedline")<br />命令栏组合框 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...生成自定义组合框时。 | ...的任何内容不想始终匹配命令栏用户界面。 |
| ...时创建类似于组合框的命令栏控件。 | ...当您有权访问样式的组合框。 |

**命令栏组合框输入的字段： 这是默认状态**

![命令栏组合框输入的字段](../../extensibility/ux-guidelines/media/0303-030_comboboxinputfield.png "0303年 030_ComboBoxInputField")<br />命令栏组合框输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxBackground` |
| 前景（文本） | `Environment.ComboBoxText` |
| Border | `Environment.ComboBoxBorder` |
| Separator | 无分隔符 |

**命令栏下拉列表按钮： 这是默认状态**

![组合框下拉&#45;向下按钮](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303年 031_ComboBoxDropdownButton")<br />命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用（从命令栏背景继承） |
| 前景（标志符号） | `Environment.ComboBoxGlyph` |

**命令栏下拉列表： 这是默认状态**

![命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303年 032_ComboBoxDropdownList")<br />命令栏下拉列表

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxPopupBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.ComboBoxItemText` |
| Border | `Environment.ComboBoxPopupBorder` |

**命令栏组合框输入的字段： 将鼠标悬停状态**

![命令栏的组合框输入的字段的悬停](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303年 033_ComboBoxInputFieldHover")<br />命令栏的组合框输入的字段的悬停

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.ComboBoxMouseOverText` |
| Border | `Environment.ComboBoxMouseOverBorder` |
| Separator | `Environment.ComboBoxMouseOverSeparator` |

 **命令栏下拉列表按钮： 将鼠标悬停状态**

![悬停时的命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303年 034_ComboBoxDropdownButtonHover")<br />悬停时的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxButtonMouseOverBackground` |
| 前景（标志符号） | `Environment.ComboBoxMouseOverGlyph` |

**命令栏下拉列表： 将鼠标悬停状态**

 ![悬停时的命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-035_comboboxdropdownlisthover.png "0303年 035_ComboBoxDropdownListHover")<br />悬停时的命令栏下拉列表

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景（菜单项） | `Environment.ComboBoxItemMouseOverBackground` |
| 前景（文本） | `Environment.ComboBoxItemMouseOverText` |
| 边框（菜单项） | `Environment.ComboBoxItemMouseOverBorder` |

 **命令栏组合框输入的字段： 已设定焦点状态**

![命令栏的组合框输入字段已设定焦点](../../extensibility/ux-guidelines/media/0303-036_comboboxinputfieldfocused.png "0303年 036_ComboBoxInputFieldFocused")<br />已设定焦点的命令栏组合框输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxFocusedBackground` |
| 前景（文本） | `Environment.ComboBoxFocusedText` |
| Border | `Environment.ComboBoxFocusedBorder` |
| Separator | `Environment.ComboBoxFocusedButtonSeparator` |

**命令栏下拉列表按钮： 已设定焦点状态**

![已设定焦点的命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303年 037_ComboBoxDropdownButtonFocused")<br />已设定焦点的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxFocusedButtonBackground` |
| 前景（标志符号） | `Environment.ComboBoxFocusedGlyph` |

 **命令栏组合框输入的字段： 按下状态**

![按下命令的组合框输入字段条形](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303年 038_ComboBoxInputFieldPressed")<br />按下的命令栏组合框输入的字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxMouseDownBackground` |
| 前景（文本） | `Environment.ComboBoxMouseDownText` |
| Border | `Environment.ComboBoxMouseDownBorder` |
| Separator | `Environment.ComboBoxMouseDownSeparator` |

**命令栏下拉列表按钮： 按下状态**

![按下的命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303年 039_ComboBoxDropdownButtonPressed")<br />按下的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxButtonMouseDownBackground` |
| 前景（标志符号） | `Environment.ComboBoxMouseDownGlyph` |

**命令栏组合框输入的字段： 已禁用状态**

![禁用命令栏的组合框输入字段](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303年 041_ComboBoxInputFieldDisabled")<br />已禁用的命令栏的组合框输入字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ComboBoxDisabledBackground` |
| 前景（文本） | `Environment.ComboBoxDisabledText` |
| Border | `Environment.ComboBoxDisabledBorder` |
| Separator | 无分隔符 |

**命令栏下拉列表按钮： 已禁用状态**

![禁用命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303年 040_ComboBoxDropdownButtonDisabled")<br />已禁用的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（标志符号） | `Environment.ComboBoxDisabledGlyph` |

#### <a name="BKMK_CommandDropDown"></a> 命令栏下拉列表

> [!IMPORTANT]
> 下拉列表类似于组合框，但缺少可编辑文本区域。 如果下拉列表包含可编辑文本区域，使用的颜色标记[命令栏组合框](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)。

![命令栏下拉 （红线）](../../extensibility/ux-guidelines/media/0303-042_dropdownredline.png "0303年 042_DropdownRedline")<br />命令栏下拉 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当创建自定义下拉列表控件。 | ...对于不类似于下拉列表的任何内容。 |
| | ...对于组合框或拆分按钮。 |

**命令栏下拉选择字段： 这是默认状态**

![默认命令栏下拉选择字段](../../extensibility/ux-guidelines/media/0303-043_dropdownselectionfield.png "0303年 043_DropdownSelectionField")<br />默认命令栏下拉选择字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownBackground` |
| 前景（文本） | `DropDownText` |
| Border | `DropDownBorder` |
| Separator | 无分隔符 |

**命令栏下拉列表按钮： 这是默认状态**

![默认命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303年 044_DropdownButton")<br />默认的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（标志符号） | `Environment.DropDownGlyph` |

**命令栏下拉列表： 这是默认状态**

![默认命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303年 045_DropdownList")<br />默认命令栏下拉列表

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownPopupBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.ComboBoxItemText` |
| Border | `Environment.DropDownPopupBorder` |
| 阴影 | `Environment.DropShadowBackground` |

**命令栏下拉选择字段： 将鼠标悬停状态**

![悬停时的命令栏下拉选择字段](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303年 046_DropdownSelectionFieldHover")<br />悬停时的命令栏下拉选择字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.DropDownMouseOverText` |
| Border | `Environment.DropDownMouseOverBorder` |
| Separator | `Environment.DropDownButtonMouseOverSeparator` |

**命令栏下拉列表按钮： 将鼠标悬停状态**

![悬停时的命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303年 047_DropdownButtonHover")<br />悬停时的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownButtonMouseOverBackground` |
| 前景（标志符号） | `Environment.DropDownMouseOverGlyph` |

**命令栏下拉列表： 将鼠标悬停状态**

![悬停时的命令栏下拉列表](../../extensibility/ux-guidelines/media/0303-048_dropdownlisthover.png "0303年 048_DropdownListHover")<br />悬停时的命令栏下拉列表

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景（菜单项） | `Environment.ComboBoxItemMouseOverBackground` |
| 前景（文本） | `Environment.ComboBoxItemMouseOverText` |
| 边框（菜单项） | `Environment.ComboBoxItemMouseOverBorder` |

 **命令栏下拉选择字段： 按下状态**

![删除&#45;下按下的选择字段](../../extensibility/ux-guidelines/media/0303-049_dropdownselectionfieldpressed.png "0303年 049_DropdownSelectionFieldPressed")<br />按命令下条形下拉选择字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownMouseDownBackground` |
| 前景（文本） | `Environment.DropDownMouseDownText` |
| Border | `Environment.DropDownMouseDownBorder` |
| Separator | `Environment.DropDownButtonMouseDownSeparator` |

**命令栏下拉列表按钮： 按下状态**

![按下的命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303年 050_DropdownButtonPressed")<br />按下的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownButtonMouseDownBackground` |
| 前景（标志符号） | `Environment.DropDownMouseDownGlyph` |

**命令栏下拉选择字段： 已禁用状态**

![禁用命令栏下拉选择字段](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303年 051_DropdownSelectionFieldDisabled")<br />已禁用的命令栏下拉选择字段

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DropDownDisabledBackground` |
| 前景（文本） | `Environment.DropDownDisabledText` |
| Border | `Environment.DropDownDisabledBorder` |
| Separator | 无分隔符 |

**命令栏下拉列表按钮： 已禁用状态**

![禁用命令栏下拉列表按钮](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303年 052_DropdownButtonDisabled")<br />已禁用的命令栏下拉按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（标志符号） | `Environment.DropDownDisabledGlyph` |

#### <a name="command-bar-split-buttons"></a>命令栏拆分按钮
拆分按钮与其他命令栏控件（如按钮、菜单和命令栏文本）共享许多令牌名称。 为方便起见，在此处重复了所有必要的操作和下拉按钮令牌名称。 拆分按钮下拉列表是实现[命令栏菜单](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)。

![拆分按钮红线](../../extensibility/ux-guidelines/media/0303-053_splitbuttonredline.png "0303年 053_SplitButtonRedline")<br />命令栏中的拆分按钮 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当你要创建的自定义拆分按钮。 | ...为其他类型的按钮。 |
| | ...在未指定任何背景/前景组合。 |

**命令栏中的拆分按钮： 这是默认状态**

![默认命令栏的拆分按钮](../../extensibility/ux-guidelines/media/0303-054_splitbutton.png "0303年 054_SplitButton")<br />默认命令栏的拆分按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | None |
| 前景（文本） | `Environment.CommandBarTextActive` |
| 前景（标志符号） | `Environment.CommandBarSplitButtonGlyph` |
| Border | 不适用 |
| Separator | 不适用 |

**命令栏中的拆分按钮： 将鼠标悬停状态**

![命令栏中的拆分按钮上悬停](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303年 055_SplitButtonHover")<br />命令栏中的拆分按钮上悬停

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.CommandBarTextHover` |
| 前景（标志符号） | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| Border | `Environment.CommandBarBorder` |
| Separator | `Environment.CommandBarSplitButtonSeparator` |

**命令栏中的拆分按钮： 按下状态**

![按下的命令栏的拆分按钮](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303年 056_SplitButtonPressed")<br />按下的命令栏中的拆分按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarMouseDownBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.CommandBarTextMouseDown` |
| 前景（标志符号） | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| Border | `Environment.CommandBarBorder` |
| Separator | 不适用 |

**命令栏中的拆分按钮： 已禁用状态**

![禁用命令栏的拆分按钮](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303年 057_SplitButtonDisabled")<br />已禁用的命令栏的拆分按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（文本） | `Environment.ComboBoxItemTextInactive` |
| 前景（标志符号） | `Environment.CommandBarTextInactive` |
| Border | 不适用 |
| Separator | 不适用 |

#### <a name="command-bar-more-options-and-overflow-buttons"></a>命令栏更多选项和溢出按钮
通过添加或删除相关命令栏按钮来自定义命令栏组时，可使用“更多选项”按钮。 命令栏由于水平空间不足而被截断，以及在单击操作中显示包含无法显示的命令栏按钮的菜单时，会出现“溢出”按钮。 这两个按钮的颜色通过一组相同的标记名称进行控制。

![命令栏更多选项按钮 （红线）](../../extensibility/ux-guidelines/media/0303-058_moreoptionsredline.png "0303年 058_MoreOptionsRedline")<br />命令栏更多选项按钮 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...的自定义更多选项或者溢出按钮。 | ...对于没有与更多选项或溢出按钮类似的功能的按钮。 |

**命令栏更多选项和溢出按钮： 这是默认状态**

![默认命令栏更多选项按钮](../../extensibility/ux-guidelines/media/0303-059_moreoptions.png "0303年 059_MoreOptions")<br />默认命令栏更多选项按钮

![默认命令栏溢出按钮](../../extensibility/ux-guidelines/media/0303-060_overflow.png "0303年 060_Overflow")<br />默认命令栏溢出按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarOptionsBackground` |
| 前景（标志符号） | `Environment.CommandBarOptionsGlyph` |

**命令栏更多选项和溢出按钮： 将鼠标悬停状态**

![命令栏更多选项按钮上悬停](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303年 061_MoreOptionsHover")<br />命令栏上悬停时的更多选项按钮

![悬停时的命令栏溢出按钮](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303年 062_OverflowOptions")<br />悬停时的命令栏溢出按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（标志符号） | `Environment.CommandBarOptionsMouseDownGlyph` |

**命令栏更多选项和溢出按钮： 按下状态**

![按下的命令栏更多选项按钮](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303年 063_MoreOptionsPressed")<br />按下的命令栏更多选项按钮

![按下的溢出](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303年 064_OverflowPressed")<br />按下的命令栏溢出按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（标志符号） | `Environment.CommandBarOptionsMouseDownGlyph` |

## <a name="document-windows"></a>文档窗口
没有无需复制文档窗口，因为它们由 Visual Studio 环境提供。 但是，你可能会决定要利用文档窗口中使用的颜色，以便你的 UI 显示方式始终与这部分 Visual Studio 环境一致。

在使用文档窗口颜色标记时，务必仅用于类似元素，并且始终成对使用它们。 如果不这样做，您可能会在 UI 中得到意外的结果。

### <a name="document-window-frames"></a>文档窗口框架
文档窗口可以在 IDE 中停靠或作为单独窗口浮动。 当在 IDE 外部浮动文档窗口时，它仍然位于文档井中，并且具有背景、 边框、 文本和 IDE 的一部分时将与相同的选项卡颜色。 但是，文档位于具有自己的背景、边框和文本颜色的框架中。 当工具窗口停靠在文档井中时，它们会从文档窗口标记名称继承其选项卡的行为和颜色。

![停靠的文档窗口 （红线）](../../extensibility/ux-guidelines/media/0303-065_dockeddocumentwindowredline.png "0303年 065_DockedDocumentWindowRedline")<br />停靠的文档窗口 （红线）

![浮动文档窗口 （红线）](../../extensibility/ux-guidelines/media/0303-066_floatingdocumentwindowredline.png "0303年 066_FloatingDocumentWindowRedline")<br />浮动文档窗口 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建 UI，您希望匹配的文档窗口的任意位置。 | ...对于您不想自动更改如果任何 UI 在 shell 具有主题更新。 |

**停靠或浮动文档窗口： 这是默认状态**

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 取决于文档类型 |
| 前景（文本） | 取决于文档类型 |
| Border | `Environment.ToolWindowBorder` |

**已设定焦点，浮动文档窗口框架： 这是默认状态**

![默认值为主要目标，浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303年 067_FrameFocused")<br />默认值为主要目标，浮动文档窗口框架

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowFloatingFrame` |
| 前景（文本） | `Environment.ToolWindowFloatingFrame` |
| 前景（标志符号） | `Environment.RaftedWindowButtonActiveGlyph` |
| Border | `Environment.MainWindowActiveDefaultBorder` |
| 边框（标志符号） | `Environment.RaftedWindowButtonActiveBorder`<br />（设置为透明） |

**失去焦点的浮动文档窗口框架： 这是默认状态**

![默认失去焦点的浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303年 068_FrameUnfocused")<br />默认失去焦点的浮动文档窗口框架

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowFloatingFrameInactive` |
| 前景（文本） | `Environment.ToolWindowFloatingFrameInactive` |
| 前景（标志符号） | `Environment.RaftedWindowButtonInactiveGlyph` |
| Border | `Environment.MainWindowInactiveBorder` |
| 边框（标志符号） | `Environment.RaftedWindowButtonInactiveBorder`<br />（设置为透明） |

**已设定焦点，浮动文档窗口框架： 将鼠标悬停状态**

![已设定焦点，浮动文档窗口框架的悬停](../../extensibility/ux-guidelines/media/0303-069_framefocusedhover.png "0303年 069_FrameFocusedHover")<br />已设定焦点，悬停时的浮动文档窗口框架

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景（标志符号） | `Environment.RaftedWindowButtonHoverActive` |
| 前景（标志符号） | `Environment.RaftedWindowButtonHoverActiveGlyph` |
| 边框（标志符号） | `Environment.RaftedWindowButtonHoverActiveBorder` |

**失去焦点的浮动文档窗口框架： 将鼠标悬停状态**

![悬停时的失去焦点的浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-070_frameunfocusedhover.png "0303年 070_FrameUnfocusedHover")<br />悬停时的失去焦点的浮动文档窗口框架

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景（标志符号） | `EnvironmentRaftedWindowButtonHoverInactive` |
| 前景（标志符号） | `Environment.RaftedWindowButtonHoverInactiveGlyph` |
| 边框（标志符号） | `Environment.RaftedWindowButtonHoverInactiveBorder` |

**已设定焦点，浮动文档窗口框架： 按下状态**

![已设定焦点，按下时浮动文档窗口框架](../../extensibility/ux-guidelines/media/0303-071_framefocusedpressed.png "0303年 071_FrameFocusedPressed")<br />已设定焦点，按下时浮动文档窗口框架

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景（标志符号） | `Environment.RaftedWindowButtonDown` |
| 前景（标志符号） | `Environment.RaftedWindowButtonDownGlyph` |
| 边框（标志符号） | `Environment.RaftedWindowButtonDownBorder` |

### <a name="document-tabs"></a>文档选项卡
文档选项卡位于选项卡通道中，以指示当前打开的文档，以及当前选择或活动的文档。 如果用户将工具窗口置于文档选项卡通道中，则这些窗口也可以在其中停靠。 在此情况下，它们使用与文档窗口相同的选项卡颜色。 如果你在创建要始终与文档窗口颜色匹配的 UI（包括主题更新，或如果安装新主题），则引用这些颜色标记。

![文档选项卡 （红线）](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303年 072_DocumentTabRedline")<br />文档选项卡 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建想要与文档选项卡匹配并自动选取主题更新或新的主题颜色的 UI 的任何位置。 | ...对于不想要在 shell 具有主题更新时自动更改的任何 UI。 |

#### <a name="open-document-tabs"></a>打开文档选项卡
每个打开的文档都在文档选项卡通道中具有显示其名称的选项卡。 文档可以处于已选定状态，或在后台打开，其选项卡会反映这些状态：

- 已选定选项卡表示当前显示在文档井中的文档。 已选定选项卡具有沿文档井上边缘扩展的文档边框。

- 背景选项卡为不是当前已选定选项卡的任何文档选项卡。单击之后，它们会成为已选定选项卡，并从这些标记名称获取所有背景、边框和文本颜色。

![打开的文档选项卡 （红线）](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303年 073_OpenDocumentTabRedline")<br />打开的文档选项卡 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当创建自定义文档选项卡。 | ...的临时 （预览） 选项卡。 |
| | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

**所选的、 已设定焦点的文档选项卡**

![选择、 已设定焦点的文档选项卡](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303年 074_SelectedTabFocused")<br />所选的、 已设定焦点的文档选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabSelectedGradientTop`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.FileTabSelectedText` |
| Border | `Environment.FileTabSelectedBorder`<br />（设置为与背景颜色相同。） |
| 文档边框 | `Environment.FileTabDocumentBorderBackground` |

**已选定、 失去焦点的文档选项卡**

![已选定、 失去焦点的文档选项卡](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303年 075_SelectedTabUnfocused")<br />已选定、 失去焦点的文档选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabInactiveGradientTop`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.FileTabInactiveText` |
| Border | `Environment.FileTabInactiveBorder`<br />（设置为与背景颜色相同。） |
| 文档边框 | `Environment.FileTabInactiveDocumentBorderBackground` |

**背景文档选项卡： 这是默认状态**

![默认背景文档选项卡](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303年 076_BackgroundTab")<br />默认背景文档选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabBackground` |
| 前景（文本） | `Environment.FileTabText` |
| Border | `Environment.FileTabBorder`<br />（设置为与背景颜色相同。） |

**背景文档选项卡： 将鼠标悬停状态**

![悬停时的背景文档选项卡](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303年 077_BackgroundTabHover")<br />悬停时的背景文档选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabHotGradientTop`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.FileTabHotText` |
| Border | `Environment.FileTabHotBorder`<br />（设置为与背景颜色相同。） |

#### <a name="preview-tab"></a>预览选项卡
也称为"临时"选项卡。当用户在解决方案资源管理器工具窗口中单击某个项时，预览选项卡会出现在文档选项卡通道右侧。 它充当文档的预览，还为用户提供用于使文档在文档选项卡通道左侧保持打开状态的选项。 一次只能打开一个预览选项卡。 预览选项卡具有背景和选定状态（与打开的选项卡一样），可以在其活动状态下具有焦点或失去焦点。

![预览选项卡 （红线）](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303年 078_PreviewTabRedline")<br />预览选项卡 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...任何位置创建临时预览，并且希望一些元素以匹配当前的预览选项卡颜色。 | ...的任何类型的文档或选项卡不是临时 （预览）。 |
| | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

**已设定焦点的选定预览选项卡**

![已设定焦点的选定预览选项卡](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303年 079_PreviewTabFocused")<br />已设定焦点的选定预览选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalSelectedActive` |
| 前景（文本） | `Environment.FileTabProvisionalSelectedActiveForeground` |
| Border | `Environment.FileTabProvisionalSelectedActiveBorder`<br />（设置为与背景颜色相同。） |
| 文档边框 | `Environment.FileTabProvisionalSelectedActiveBorder` |

**失去焦点的选定预览选项卡**

![失去焦点的选定预览选项卡](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303年 080_PreviewTabUnfocused")<br />失去焦点的选定预览选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalSelectedInactive` |
| 前景（文本） | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| Border | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| 文档边框 | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**背景预览选项卡： 这是默认状态**

![默认背景预览选项卡](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303年 081_PreviewBackgroundTab")<br />默认背景预览选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalInactive` |
| 前景（文本） | `Environment.FileTabProvisionalInactiveForeground` |
| Border | `Environment.FileTabProvisionalInactiveBorder`<br />（设置为与背景颜色相同。） |

**背景预览选项卡： 将鼠标悬停状态**

![背景预览选项卡上悬停](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303年 082_PreviewBackgroundTabHover")<br />悬停时的背景预览选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.FileTabProvisionalHover` |
| 前景（文本） | `Environment.FileTabProvisionalHoverForeground` |
| Border | `Environment.FileTabProvisionalHoverBorder`<br />（设置为与背景颜色相同。） |

#### <a name="document-overflow-button"></a>文档溢出按钮
如果有一个或多个文档打开，则无论当前配置中是否有垂直空间可容纳所有文档选项卡，都会提供文档溢出按钮。 文档溢出下拉菜单中，通过控制[命令栏菜单](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)颜色，显示的所有打开的文档，可见或隐藏，具体取决于是否所有打开的文档溢出标志符号更改的列表显示在选项卡通道中。

![文档溢出按钮 （红线）](../../extensibility/ux-guidelines/media/0303-083_overflowredline.png "0303年 083_OverflowRedline")<br />文档溢出按钮 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当创建自定义文档溢出按钮。 | ...对于不类似于溢出按钮的 UI。 |
| | ...的命令栏溢出按钮。 |

**文档溢出按钮： 这是默认状态**

![默认文档溢出按钮](../../extensibility/ux-guidelines/media/0303-084_overflow.png "0303年 084_Overflow")<br />默认文档溢出按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DocWellOverflowButtonBackground` |
| 前景（标志符号） | `Environment.DocWellOverflowButtonGlyph` |
| Border | 不适用 |

**文档溢出按钮： 将鼠标悬停状态**

![悬停时的文档溢出按钮](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303年 085_OverflowHover")<br />悬停时的文档溢出按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DocWellOverflowButtonMouseOverBackground` |
| 前景（标志符号） | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| Border | `Environment.DocWellOverflowButtonMouseOverBorder` |

**文档溢出按钮： 按下状态**

![在按下文档溢出按钮](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303年 086_OverflowPressed")<br />在按下文档溢出按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.DocWellOverflowButtonMouseDownBackground` |
| 前景（标志符号） | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| Border | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>标记
Visual Studio 支持标记，这使用户可以声明可搜索的关键字以用于跟踪。 例如，项目经理和开发人员可以使用 Team Foundation Server (TFS) 对工作项进行标记。 下表为标记本身以及在悬停和已选定状态下出现的“关闭图标”标志符号提供颜色名称。

![在 Visual Studio 中标记 （红线）](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303年 176_TaggingRedline")<br />在 Visual Studio 中标记 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...为支持标记的 UI。 | ...的任何其他类型的 UI。 |

#### <a name="tags"></a>Tags

**标记： 默认状态**

![默认标记](../../extensibility/ux-guidelines/media/0303-177_tag.png "0303年 177_Tag")<br />默认标记

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.Background` |
| 前景（文本） | `Tag.Background` |

**标记： 悬停状态**

![悬停时的标记](../../extensibility/ux-guidelines/media/0303-178_taghover.png "0303年 178_TagHover")<br />悬停时的标记

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.HoverBackground` |
| 前景（文本） | `Tag.HoverBackgroundText` |

**标记： 按下状态**

![按下标记](../../extensibility/ux-guidelines/media/0303-179_tagpressed.png "0303年 179_TagPressed")<br />按下的标记

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.PressedBackground` |
| 前景（文本） | `Tag.PressedBackgroundText` |

**标记： 所选的状态**

![选择标记](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303年 180_TagSelected")<br />所选的标记

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.SelectedBackground` |
| 前景（文本） | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>关闭 (&times;) 标记标志符号

**关闭 (&times;) 标记标志符号： 这是默认状态**

![默认关闭 (&times;) 标记标志符号](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303年 181_TagGlyph")<br />默认关闭 (&times;) 标记标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（标志符号） | `Tag.TagHoverGlyph` |

**关闭 (&times;) 标记标志符号： 将鼠标悬停状态**

![关闭 (&times;) 标记标志符号的悬停](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303年 182_TagGlyphHover")<br />关闭 (&times;) 悬停时的标记标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagHoverGlyphHoverBackground` |
| 前景（标志符号） | `Tag.TagHoverGlyphHover` |
| Border | `Tag.TagHoverGlyphHoverBorder` |

**关闭 (&times;) 标记标志符号： 按下状态**

![按下关闭 (&times;) 标记标志符号](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303年 183_TagGlyphPressed")<br />按下关闭 (&times;) 标记标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagHoverGlyphPressedBackground` |
| 前景（标志符号） | `Tag.TagHoverGlyphPressed` |
| Border | `Tag.TagHoverGlyphPressedBorder` |

**选择与关闭标记 (&times;) 标志符号： 这是默认状态**

![默认关闭与所选的标记 (&times;) 标志符号](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303年 184_TagSelected")<br />默认关闭与所选的标记 (&times;) 标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（标志符号） | `Tag.TagSelectedGlyph` |

**选择与关闭标记 (&times;) 标志符号： 将鼠标悬停状态**

![选择与关闭标记 (&times;) 上悬停标志符号](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303年 185_TagSelectedHover")<br />选择与关闭标记 (&times;) 上悬停标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagSelectedGlyphHoverBackground` |
| 前景（标志符号） | `Tag.TagSelectedGlyphHover` |
| Border | `Tag.TagSelectedGlyphHoverBorder` |

**选择与关闭标记 (&times;) 标志符号： 按下状态**

![选择，按下关闭的标记 (&times;) 标志符号](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303年 186_TagSelectedPressed")<br />选择，按下关闭的标记 (&times;) 标志符号

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Tag.TagSelectedGlyphPressedBackground` |
| 前景（标志符号） | `Tag.TagSelectedGlyphPressed` |
| Border | `Tag.TagSelectedGlyphPressedBorder` |

## <a name="tool-windows"></a>工具窗口
没有无需复制工具窗口，因为它们由 Visual Studio 环境提供。 但是，你可能会决定要利用工具窗口中使用的颜色，以便你的 UI 显示方式始终与这部分 Visual Studio 环境一致。

![工具窗口 （红线）](../../extensibility/ux-guidelines/media/0303-087_toolwindowredline.png "0303年 087_ToolWindowRedline")<br />工具窗口 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建想要与工具窗口匹配的 UI 的任何位置。 | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

### <a name="tool-window-frame"></a>工具窗口框架
Visual Studio 中的工具窗口用于许多不同的任务，可以采用多个不同状态中的一个状态存在。 如果工具窗口处于打开状态，则它可以分配到文档区域四边的任何一边。 工具窗口还可以在 IDE 外部浮动，从而使它们可以在用户屏幕中的任何位置重新定位。 浮动窗口始终位于 IDE 顶部。 最后，工具窗口可以作为文档窗口停靠，并显示为文档井中的选项卡。 作为文档窗口停靠的工具窗口会使用文档窗口标记名称进行部分着色。

![工具窗口框架 （红线）](../../extensibility/ux-guidelines/media/0303-088_toolwindowframeredline.png "0303年 088_ToolWindowFrameRedline")<br />工具窗口框架 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建想要与工具窗口匹配的 UI 的任何位置。 | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

**停靠的工具窗口**

![停靠的工具窗口](../../extensibility/ux-guidelines/media/0303-089_toolwindowdocked.png "0303年 089_ToolWindowDocked")<br />停靠的工具窗口

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowBackground` |
| Border | `Environment.ToolWindowBorder` |

**浮动、 已设定焦点的工具窗口**

![浮动、 已设定焦点的工具窗口](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303年 090_ToolWindowFocused")<br />浮动、 已设定焦点的工具窗口

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowBackground` |
| Border | `Environment.MainWindowActiveDefaultBorder` |

**浮动、 失去焦点的工具窗口**

![浮动、 失去焦点的工具窗口](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303年 091_ToolWindowUnfocused")<br />浮动、 失去焦点的工具窗口

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowBackground` |
| Border | `Environment.MainWindowInactiveBorder` |

### <a name="toolbox-like-windows"></a>类似于工具箱的 windows
工具箱是 Visual Studio 中的使用频率最高公共工具窗口之一。 它是实质上是具有特殊主题和应用的样式的树控件。

![Toolbox-like window (redline)](../../extensibility/ux-guidelines/media/0303-189_toolboxredline.png "0303-189_ToolboxRedline")<br />类似于工具箱的窗口 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...当你设计一个工具窗口，你想要始终与 shell 工具箱保持一致。 | ...的任何内容不是类似于工具箱 UI，或如果不确定是否在 shell 工具箱颜色更改中移动时 UI 有问题。 |

**工具箱节点： 这是默认状态**

![默认的工具箱父节点](../../extensibility/ux-guidelines/media/0303-190_toolboxparentnode.png "0303年 190_ToolboxParentNode")<br />默认的工具箱父节点

![默认的工具箱子节点](../../extensibility/ux-guidelines/media/0303-191_toolboxchildnode.png "0303年 191_ToolboxChildNode")<br />默认的工具箱子节点

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolboxContent`<br />（标题） |
| 背景 | `Environment.ToolWindowBackground`<br />（各项或如果没有可用控件的整个窗口） |
| Border | None |
| 前景（标志符号） | `Environment.ToolboxContent` |
| 前景（文本） | `Environment.ToolboxContent` |

**工具箱子节点： 将鼠标悬停状态**

![悬停时的工具箱子节点](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303年 192_ToolboxChildNodeHover")<br />悬停时的工具箱子节点

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolboxContentMouseOver`<br />（仅限单个项） |
| Border | None |
| 前景（文本） | `Environment.ToolboxContentMouseOver`<br />（仅限单个项） |

**所选工具箱节点： 已设定焦点状态**

![集中的所选工具箱父节点](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303年 193_ToolboxParentNodeFocused")<br />集中的所选工具箱父节点

![集中的所选的工具箱子节点](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303年 194_ToolboxChildNodeFocused")<br />集中的所选的工具箱子节点

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemActive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| Border | `TreeView.FocusVisualBorder`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 前景（标志符号） | `TreeView.SelectedItemActive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 前景（文本） | `TreeView.SelectedItemActive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |

**所选工具箱节点： 失去焦点的状态**

![已选定、 失去焦点的工具箱父节点](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303年 195_ToolboxParentNodeUnfocused")<br />已选定、 失去焦点的工具箱父节点

![已选定、 失去焦点的工具箱子节点](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303年 196_ToolboxChildNodeUnfocused")<br />已选定、 失去焦点的工具箱子节点

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `TreeView.SelectedItemInactive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| Border | None |
| 前景（标志符号） | `TreeView.SelectedItemInactive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |
| 前景（文本） | `TreeView.SelectedItemInactive`<br />来自 [Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) 类别 |

### <a name="tool-window-title-bar"></a>工具窗口标题栏
标题栏边框不是真实边框，它是标题栏顶部的粗线。 它没有其失去焦点状态的令牌名称。

![工具窗口标题栏 （红线）](../../extensibility/ux-guidelines/media/0303-092_toolwindowtitlebarredline.png "0303年 092_ToolWindowTitleBarRedline")<br />工具窗口标题栏 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建想要与工具窗口匹配的 UI 的任何位置。 | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

**已设定焦点的标题栏**

![已设定焦点的标题栏](../../extensibility/ux-guidelines/media/0303-093_titlebarfocused.png "0303年 093_TitleBarFocused")<br />已设定焦点的标题栏

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.TitleBarActiveGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.TitleBarActiveText` |
| Border | `Environment.TitleBarActiveBorder`<br />（设置为与背景颜色相同。） |
| 拖动句柄 | `Environment.TitleBarDragHandleActive` |

**失去焦点的标题栏**

![失去焦点的标题栏](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303年 094_TitleBarUnfocused")<br />失去焦点的标题栏

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.TitleBarInactiveGradientBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.TitleBarInactiveText` |
| Border | 不适用 |
| 拖动句柄 | `Environment.TitleBarDragHandle` |

#### <a name="tool-window-title-bar-buttons"></a>工具窗口标题栏按钮
![标题栏按钮 （红线）](../../extensibility/ux-guidelines/media/0303-095_titlebarbuttonredline.png "0303年 095_TitleBarButtonRedline")<br />标题栏按钮 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...对于在使用来自工具窗口标题栏的颜色标记的 UI 中显示的按钮。 | ...对于在其他位置出现的按钮。 |
| | ...在未指定任何背景/前景组合。 |

**已设定焦点的标题栏按钮： 这是默认状态**

![默认情况下，已设定焦点的标题栏按钮](../../extensibility/ux-guidelines/media/0303-096_titlebarbuttonfocused.png "0303年 096_TitleBarButtonFocused")<br />默认情况下，已设定焦点的标题栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（标志符号） | `Environment.ToolWindowButtonActiveGlyph` |
| Border | 不适用 |

**失去焦点的标题栏按钮： 这是默认状态**

![默认情况下失去焦点的标题栏按钮](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303年 097_TitleBarButtonUnfocused")<br />默认情况下失去焦点的标题栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | 不适用 |
| 前景（标志符号） | `Environment.ToolWindowButtonInactiveGlyph` |
| Border | 不适用 |

**已设定焦点的标题栏按钮： 将鼠标悬停状态**

![标题栏按钮侧重于悬停](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303年 098_TitleBarButtonFocusedHover")<br />悬停时的已设定焦点的标题栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonHoverActive` |
| 前景（标志符号） | `Environment.ToolWindowButtonHoverActiveGlyph` |
| Border | `Environment.ToolWindowButtonHoverActiveBorder` |

**失去焦点的标题栏按钮： 将鼠标悬停状态**

![悬停时的失去焦点的标题栏按钮](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303年 099_TitleBarButtonUnfocusedHover")<br />悬停时的失去焦点的标题栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonHoverInactive` |
| 前景（标志符号） | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| Border | `Environment.ToolWindowButtonHoverInactiveBorder` |

**已设定焦点的标题栏按钮： 按下状态**

![标题栏按钮侧重于按](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303年 100_TitleBarButtonFocusedPressed")<br />按下时的已设定焦点的标题栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonDown` |
| 前景（标志符号） | `Environment.ToolWindowButtonDownActiveGlyph` |
| Border | `Environment.ToolWindowButtonDownBorder` |

**失去焦点的标题栏按钮： 按下状态**

![按下时的失去焦点的标题栏按钮](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303年 101_TitleBarButtonUnfocusedPressed")<br />按下时的失去焦点的标题栏按钮

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowButtonDown` |
| 前景（标志符号） | `Environment.ToolWindowButtonDownInactiveGlyph` |
| Border | `Environment.ToolWindowButtonDownBorder` |

### <a name="tool-window-tabs"></a>工具窗口选项卡
![工具窗口选项卡 （红线）](../../extensibility/ux-guidelines/media/0303-102_toolwindowtabredline.png "0303年 102_ToolWindowTabRedline")<br />工具窗口选项卡 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建想要与工具窗口匹配的 UI 的任何位置。 | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

**已选定、 已设定焦点的工具窗口选项卡**

![选择、 已设定焦点的工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-103_toolwindowtabfocused.png "0303年 103_ToolWindowTabFocused")<br />已选定、已设定焦点的工具窗口选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabSelectedTab` |
| 前景（文本） | `Environment.ToolWindowTabSelectedActiveText` |
| Border | `Environment.ToolWindowTabSelectedBorder`<br />（设置为与背景颜色相同。） |

**已选定、 失去焦点的工具窗口选项卡**

![已选定、 失去焦点的工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303年 104_ToolWindowTabUnfocused")<br />已选定、失去焦点的工具窗口选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabSelectedTab` |
| 前景（文本） | `Environment.ToolWindowTabSelectedText` |
| Border | `Environment.ToolWindowTabSelectedBorder`<br />（设置为与背景颜色相同。） |

**背景工具窗口选项卡： 这是默认状态**

![默认背景工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303年 105_ToolWindowBackgroundTab")<br />默认背景工具窗口选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br />（梯度停止点设置为 Visual Studio 2013 中相同的颜色值。） |
| 前景（文本） | `Environment.ToolWindowTabText` |
| Border | `Environment.ToolWindowTabBorder` |

**背景工具窗口选项卡： 将鼠标悬停状态**

![悬停时的背景工具窗口选项卡](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303年 106_ToolWindowBackgroundTabHover")<br />悬停时的背景工具窗口选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br />（梯度停止点设置为 Visual Studio 2013 中相同的颜色值。） |
| 前景（文本） | `Environment.ToolWindowTabMouseOverText` |
| Border | `Environment.ToolWindowTabMouseOverBorder`<br />（设置为与背景颜色相同。） |

### <a name="auto-hide-tabs"></a>自动隐藏选项卡

![自动隐藏选项卡 （红线）](../../extensibility/ux-guidelines/media/0303-107_autohideredline.png "0303年 107_AutoHideRedline")自动隐藏选项卡 （红线）

| 使用... | 请勿使用... |
| --- | --- |
| ...要创建想要与自动隐藏工具窗口选项卡匹配的 UI 的任何位置。 | ...对于不想要时自动更改的任何 UI 在 shell 具有主题更新。 |

**自动隐藏选项卡： 这是默认状态**

![默认自动隐藏选项卡](../../extensibility/ux-guidelines/media/0303-108_autohidetab.png "0303年 108_AutoHideTab")<br />默认自动隐藏选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.AutoHideTabBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.AutoHideTabText` |
| Border | `Environment.AutoHideTabBorder` |

**自动隐藏选项卡： 将鼠标悬停状态**

![悬停时自动隐藏选项卡](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303年 109_AutoHideTabHover")<br />悬停时的“自动隐藏”选项卡

| 元素 | 令牌名称：Category.color |
| --- | --- |
| 背景 | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />（梯度停止点不在主题 UI 中使用此令牌。） |
| 前景（文本） | `Environment.AutoHideTabMouseOverText` |
| Border | `Environment.AutoHideTabMouseOverBorder` |
