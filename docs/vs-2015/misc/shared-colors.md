---
title: 共享颜色 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 9d3186f3-07d2-441f-b33e-435e95d8a0b8
caps.latest.revision: 11
ms.author: brgeorge
ms.openlocfilehash: 421ff85831bb611b655de2bc35f01423b61921a2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436575"
---
# <a name="shared-colors"></a>共享颜色
在此处插入介绍。  
  
## <a name="shared-colors"></a>共享颜色  
 在设计使用公共 Visual Studio shell 元素的 UI，或者希望界面元素与类似功能一致时，可使用包定义文件中的现有标记名称来选择和分配颜色。 这可确保 UI 与整体 Visual Studio 环境保持一致，并确保它在添加或更新主题时自动更新。  
  
 本文介绍公共 UI 元素以及它们使用的标记名称（可以在构建类似 UI 时引用这些名称）。 有关如何访问这些颜色标记的特定信息，请参见 [The VSColor Service](../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。  
  
 请确保正确使用标记名称：  
  
- **使用基于功能，不是颜色本身的标记名称。** 公共共享颜色与特定界面元素关联，仅用于相同或类似功能。 例如，不要仅仅因为你喜欢某个已按下组合框的颜色，便将该颜色重复用于旋转进度动画。 组合框和动画的功能不同，如果与组合框关联的颜色更改，则它可能不再是适合于动画元素的颜色。 以一致方法使用颜色可帮助使用户适应，防止产生混乱。  
  
- **采用正确组合使用背景和文本颜色。** 要用于文本的背景色具有关联文本颜色。 不要使用为该背景指定的颜色之外的文本颜色。 如果没有关联文本颜色，请勿将该背景色用于期望在其上显示文本的任何图面。 文本和背景色的其他组合可能会导致不可读的界面。  
  
- **使用适合于其位置的控件颜色。** 在特定状态下，某些 Visual Studio 控件没有单独的边框和背景色。 而是从它们之后的图面选取这些颜色。 请确保始终使用适合于要在其中放置控件的位置的标记名称。  
  
> [!IMPORTANT]
> 请勿使用在“起始页”或“Cider”类别中找到的标记！  
  
### <a name="command-structures"></a>命令结构  
  
#### <a name="BKMK_CommandMenus"></a> 菜单  
 菜单在 Visual Studio 2013 中可以出现在多个位置处：主菜单栏、嵌入在文档或工具窗口中或是在整个 IDE 的各个位置右键单击时。 与其他 UI 元素关联的菜单的实现在针对相应元素的部分中进行讨论。 应始终使用由 Visual Studio 环境提供的标准菜单实现。 但是，在某些极少数情况下，你可能无法访问标准 Visual Studio 菜单。 在这些情况下，请使用以下标记名称以确保 UI 与 Visual Studio 中的其他菜单保持一致。  
  
 ![菜单红线](../extensibility/ux-guidelines/media/0303-000-menuredline.png "0303年 000_MenuRedline")  
  
使用...  
- 每当需要创建自定义菜单时。  
  
- 如果具有要与 Visual Studio 菜单匹配的新 UI 组件时。  
  
请勿使用...  
单独的背景色。 始终使用指定的背景/前景组合。  
  
##### <a name="menu-title"></a>菜单标题  
 菜单标题由背景、边框和标题文本以及可选的标志符号（通常是在菜单位于命令栏中使用）组成。  
  
 ![菜单标题红线](../extensibility/ux-guidelines/media/0303-001-menutitleredline.png "0303年 001_MenuTitleRedline")  
  
使用...  
每当创建自定义菜单标题时。  
  
请勿使用...  
- 对于并非希望始终与菜单标题匹配的任何内容。  
  
- 在指定组合之外的任何背景/前景组合中。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![菜单标题默认值](../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303年 002_MenuTitleDefault")<br /><br /> **菜单标题**|背景|None|  
|![菜单标题默认值](../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303年 002_MenuTitleDefault")<br /><br /> **菜单标题**|前景（文本）|`Environment.CommandBarTextActive`|  
|![具有默认值标志符号的菜单标题](../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303年 003_MenuTitleWithGlyphDefault")<br /><br /> **具有字形的菜单标题**|前景（标志符号）|`Environment.CommandBarMenuGlyph`|  
|![具有默认值标志符号的菜单标题](../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303年 003_MenuTitleWithGlyphDefault")<br /><br /> **具有字形的菜单标题**|Border|None|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的菜单标题](../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303年 004_MenuTitleHover")<br /><br /> **菜单标题**|背景|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停时的菜单标题](../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303年 004_MenuTitleHover")<br /><br /> **菜单标题**|前景（文本）|`Environment.CommandBarTextHover`|  
|![菜单标题的具有字形的悬停](../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303年 005_MenuTitleWithGlyphHover")<br /><br /> **具有字形的菜单标题**|前景（标志符号）|`Environment.CommandBarMenuMouseOverGlyph`|  
|![菜单标题的具有字形的悬停](../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303年 005_MenuTitleWithGlyphHover")<br /><br /> **具有字形的菜单标题**|Border|`Environment.CommandBarBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下的菜单标题](../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303年 006_MenuTitlePressed")<br /><br /> **菜单标题**|背景|`Environment.CommandBarMenuBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![按下的菜单标题](../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303年 006_MenuTitlePressed")<br /><br /> **菜单标题**|前景（文本）|`Environment.CommandBarTextActive`|  
|![具有标志符号按下的菜单标题](../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303年 007_MenuTitleWithGlyphPressed")<br /><br /> **具有字形的菜单标题**|前景（标志符号）|`Environment.CommandBarMenuMouseDownGlyph`|  
|![具有标志符号按下的菜单标题](../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303年 007_MenuTitleWithGlyphPressed")<br /><br /> **具有字形的菜单标题**|Border|`Environment.CommandBarMenuBorder`<br /><br /> 仅限左侧、顶端和右侧。|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![禁用的具有字形的菜单标题](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303年 008_MenuTitleWithGlyphDisabled")<br /><br /> **具有字形的菜单标题**|背景|None|  
|![禁用的具有字形的菜单标题](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303年 008_MenuTitleWithGlyphDisabled")<br /><br /> **具有字形的菜单标题**|前景（文本）|`Environment.CommandBarTextInactive`|  
|![禁用的具有字形的菜单标题](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303年 008_MenuTitleWithGlyphDisabled")<br /><br /> **具有字形的菜单标题**|前景（标志符号）|`Environment.CommandBarTextInactive`|  
|![禁用的具有字形的菜单标题](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303年 008_MenuTitleWithGlyphDisabled")<br /><br /> **具有字形的菜单标题**|Border|None|  
  
##### <a name="menu"></a>菜单  
 各个菜单项由菜单文本和可选的图标、复选框或子菜单标志符号组成。 其背景和文本颜色会在鼠标悬停在上方时更改。 此颜色标记是前景/背景对。  
  
 ![菜单项红线](../extensibility/ux-guidelines/media/0303-009-menuitemredline.png "0303年 009_MenuItemRedline")  
  
 使用...  
 对于从菜单栏或命令栏启动的任何下拉列表。  
  
请勿使用...  
- 对于在另一个上下文中出现的任何下拉列表。  

- 在指定组合之外的任何背景/前景组合中。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|背景|`Environment.CommandBarMenuBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|前景（文本）|`Environment.CommandBarTextActive`|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|前景（子菜单标志符号）|`Environment.CommandBarMenuSubmenuGlyph`|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|Border|`Environment.CommandBarMenuBorder`|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|图标通道背景|`Environment.CommandBarMenuIconBackground`|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|Separator|`Environment.CommandBarMenuSeparator`|  
|![菜单默认值](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303年 010_MenuDefault")<br /><br /> **菜单**|阴影|`Environment.DropShadowBackground`|  
|![选中的菜单](../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303年 011_MenuChecked")<br /><br /> **已选中**|选中标记|`Environment.CommandBarCheckBox`|  
|![选中的菜单](../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303年 011_MenuChecked")<br /><br /> **已选中**|复选标记背景|`Environment.CommandBarSelectedIcon`|  
|![选定的菜单](../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303年 012_MenuSelected")<br /><br /> **选择**|图标背景|`Environment.CommandBarSelected`|  
|![选定的菜单](../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303年 012_MenuSelected")<br /><br /> **选择**|图标边框|`Environment.CommandBarSelectedBorder`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Menu hover](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **菜单项**|背景|`Environment.CommandBarMenuItemMouseOver`|  
|![Menu hover](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **菜单项**|前景（文本）|`Environment.CommandBarMenuItemMouseOver`|  
|![Menu hover](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **菜单项**|前景（子菜单标志符号）|`Environment.CommandBarMenuMouseOverSubmenuGlyph`|  
|![选中的菜单悬停](../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303年 014_MenuHoverChecked")<br /><br /> **已选中**|选中标记|`Environment.CommandBarCheckBoxMouseOver`|  
|![选中的菜单悬停](../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303年 014_MenuHoverChecked")<br /><br /> **已选中**|复选标记背景|`Environment.CommandBarHoverOverSelectedIcon`|  
|![选定的菜单悬停](../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303年 015_MenuHoverSelected")<br /><br /> **选择**|图标背景|`Environment.CommandBarHoverOverSelected`|  
|![选定的菜单悬停](../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303年 015_MenuHoverSelected")<br /><br /> **选择**|图标边框|`Environment.CommandBarHoverOverSelectedIconBorder`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![禁用的菜单](../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303年 016_MenuDisabled")<br /><br /> Menu item|前景（文本）|`Environment.CommandBarTextInactive`|  
|![禁用的菜单](../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303年 016_MenuDisabled")<br /><br /> Menu item|前景（子菜单标志符号）|`Environment.CommandBarMenuSubmenuGlyph`|  
|![选中的禁用的菜单](../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303年 017_MenuDisabledChecked")<br /><br /> 已选中|选中标记|`Environment.CommandBarCheckBoxDisabled`|  
|![选中的禁用的菜单](../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303年 017_MenuDisabledChecked")<br /><br /> 已选中|复选标记背景|`Environment.CommandBarSelectedIconDisabled`|  
  
#### <a name="command-bar"></a>命令栏  
 命令栏在 Visual Studio IDE 中可以出现在多个位置处，最值得注意的是命令架以及嵌入在工具或文档窗口中。  
  
 一般而言，需始终使用由 Visual Studio 环境提供的标准命令栏实现。 使用标准机制可确保所有视觉细节都正确显示，并且交互元素的行为与其他 Visual Studio 命令栏控件一致。 但是，如果你需要构建自己的命令栏，请确保使用以下标记名称正确设计其样式。  
  
 ![命令栏红线](../extensibility/ux-guidelines/media/0303-018-commandbarredline.png "0303年 018_CommandBarRedline")  
  
 ![溢出按钮红线](../extensibility/ux-guidelines/media/0303-019-overflowbuttonredline.png "0303年 019_OverflowButtonRedline")  
  
 使用...  
 在需要嵌入式命令栏，但无法使用标准 Visual Studio 命令栏实现的位置处。  
  
请勿使用...  
- 对于与命令栏不相似的 UI 元素。  

- 对于指定了其标记名称的命令栏组件之外的命令栏组件。  
  
##### <a name="command-bar-group"></a>命令栏组  
 命令栏组由一组相关命令栏控件组成，可能包含任何数量的按钮、拆分按钮、下拉菜单、组合框或菜单。 这些控件的颜色通过单独的标记名称进行控制，在本指南中的其他位置单独进行了讨论。 分隔线用于将命令栏组划分为相关子组。  
  
 ![命令栏组红线](../extensibility/ux-guidelines/media/0303-020-commandbargroupredline.png "0303年 020_CommandBarGroupRedline")  
  
 使用...  
 在需要嵌入式命令栏，但无法使用标准 Visual Studio 命令栏实现的位置处。  
  
请勿使用...  
- 对于与命令栏不相似的 UI 元素。  

- 对于指定了其标记名称的命令栏组件之外的命令栏组件。  
  
  **默认值** （无任何其他状态）  
  
|元素|令牌名称：Category.color|  
|-------------|--------------------------------|  
|背景|`Environment.CommandBarGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|Border|`Environment.CommandBarToolBarBorder`|  
|拖动句柄|`Environment.CommandBarDragHandle`|  
|Separator|`Environment.CommandBarToolBarSeparator`<br /><br /> `Environment.CommandBarToolBarSeparatorHighlight`|  
  
##### <a name="command-icons"></a>命令图标  
 ![命令图标红线](../extensibility/ux-guidelines/media/0303-021-commandiconredline1.png "0303年 021_CommandIconRedline1")  
  
 ![命令图标红线](../extensibility/ux-guidelines/media/0303-022-commandiconredline2.png "0303年 022_CommandIconRedline2")  
  
 使用...  
 对于将放置在命令栏上的任何按钮。  
  
请勿使用...  
- 对于具有自己的标记名称的控件。  

- 在指定组合之外的任何背景/前景组合中。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![命令图标默认值](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303年 023_CommandIconDefault")<br /><br /> **默认**|背景|不适用（从命令栏背景继承）|  
|![命令图标默认值](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303年 023_CommandIconDefault")<br /><br /> **默认**|前景（文本）|`Environment.CommandBarTextActive`|  
|![命令图标默认值](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303年 023_CommandIconDefault")<br /><br /> **默认**|Border|不适用|  
|![命令图标默认选定](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303年 024_CommandIconDefaultSelected")<br /><br /> **选择**|背景|`Environment.CommandBarSelected`|  
|![命令图标默认选定](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303年 024_CommandIconDefaultSelected")<br /><br /> **选择**|前景（文本）|`Environment.CommandBarTextSelected`|  
|![命令图标默认选定](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303年 024_CommandIconDefaultSelected")<br /><br /> **选择**|Border|`Environment.CommandBarSelectedBorder`|  
  
 **悬停和键盘已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![命令图标悬停](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303年 025_CommandIconHover")<br /><br /> **悬停时的标准**|背景|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![命令图标悬停](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303年 025_CommandIconHover")<br /><br /> **悬停时的标准**|前景（文本）|`Environment.CommandBarTextHover`|  
|![命令图标悬停](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303年 025_CommandIconHover")<br /><br /> **悬停时的标准**|Border|`Environment.CommandBarBorder`|  
|![命令选择图标悬停](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303年 026_CommandIconHoverSelected")<br /><br /> **悬停时的选择**|背景|`Environment.CommandBarHoverOverSelected`|  
|![命令选择图标悬停](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303年 026_CommandIconHoverSelected")<br /><br /> **悬停时的选择**|前景（文本）|`Environment.CommandBarTextHoverOverSelected`|  
|![命令选择图标悬停](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303年 026_CommandIconHoverSelected")<br /><br /> **悬停时的选择**|Border|`Environment.CommandBarHoverOverSelectedIconBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下命令图标](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303年 027_CommandIconPressed")<br /><br /> **已按下的命令图标**|背景|`Environment.CommandBarMouseDownBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![按下命令图标](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303年 027_CommandIconPressed")<br /><br /> **已按下的命令图标**|前景（文本）|`Environment.CommandBarTextMouseDown`|  
|![按下命令图标](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303年 027_CommandIconPressed")<br /><br /> **已按下的命令图标**|Border|`Environment.CommandBarBorder`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![禁用命令图标](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303年 028_CommandIconDisabled")<br /><br /> **已禁用的命令图标**|背景|不适用（从命令栏背景继承）|  
|![禁用命令图标](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303年 028_CommandIconDisabled")<br /><br /> **已禁用的命令图标**|前景（文本）|`Environment.CommandBarTextInactive`|  
|![禁用命令图标](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303年 028_CommandIconDisabled")<br /><br /> **已禁用的命令图标**|Border|不适用|  
  
##### <a name="BKMK_CommandComboBox"></a> 组合框  
  
> [!IMPORTANT]
> 组合框类似于下拉列表，但包含一个可编辑文本区域。 如果下拉列表不包含可编辑文本区域，请使用位于 [Drop-down](../misc/shared-colors.md#BKMK_CommandDropDown)下的颜色标记。  
  
 ![Combo box redline](../extensibility/ux-guidelines/media/0303-029-comboboxredline.png "0303-029_ComboBoxRedline")  
  
使用...  
- 当构建自定义组合框时。  

- 当创建类似于组合框的命令栏控件时。  

请勿使用...  
- 对于并非希望始终与命令栏 UI 匹配的任何内容。  

- 当你可以访问设置了样式的组合框时。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![组合框输入的字段](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303年 030_ComboBoxInputField")<br /><br /> **输入的字段**|背景|`Environment.ComboBoxBackground`|  
|![组合框输入的字段](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303年 030_ComboBoxInputField")<br /><br /> **输入的字段**|前景（文本）|`Environment.ComboBoxText`|  
|![组合框输入的字段](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303年 030_ComboBoxInputField")<br /><br /> **输入的字段**|Border|`Environment.ComboBoxBorder`|  
|![组合框输入的字段](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303年 030_ComboBoxInputField")<br /><br /> **输入的字段**|Separator|无分隔符|  
|![组合框下拉&#45;向下按钮](../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303年 031_ComboBoxDropdownButton")<br /><br /> **下拉按钮**|背景|不适用（继承）|  
|![组合框下拉&#45;向下按钮](../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303年 031_ComboBoxDropdownButton")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.ComboBoxGlyph`|  
|![组合框&#47;删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303年 032_ComboBoxDropdownList")<br /><br /> **下拉列表**|背景|`Environment.ComboBoxPopupBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![组合框&#47;删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303年 032_ComboBoxDropdownList")<br /><br /> **下拉列表**|前景（文本）|`Environment.ComboBoxItemText`|  
|![组合框&#47;删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303年 032_ComboBoxDropdownList")<br /><br /> **下拉列表**|Border|`Environment.ComboBoxPopupBorder`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的组合框输入的字段](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303年 033_ComboBoxInputFieldHover")<br /><br /> **输入的字段**|背景|`Environment.ComboBoxMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停时的组合框输入的字段](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303年 033_ComboBoxInputFieldHover")<br /><br /> **输入的字段**|前景（文本）|`Environment.ComboBoxMouseOverText`|  
|![悬停时的组合框输入的字段](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303年 033_ComboBoxInputFieldHover")<br /><br /> **输入的字段**|Border|`Environment.ComboBoxMouseOverBorder`|  
|![悬停时的组合框输入的字段](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303年 033_ComboBoxInputFieldHover")<br /><br /> **输入的字段**|Separator|`Environment.ComboBoxMouseOverSeparator`|  
|![组合框&#47;删除&#45;向下按钮上悬停](../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303年 034_ComboBoxDropdownButtonHover")<br /><br /> **下拉按钮**|背景|`Environment.ComboBoxButtonMouseOverBackground`|  
|![组合框&#47;删除&#45;向下按钮上悬停](../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303年 034_ComboBoxDropdownButtonHover")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.ComboBoxMouseOverGlyph`|  
|![组合框&#47;删除&#45;下拉列表的悬停](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303年 035_ComboBoxDropdownListHover")<br /><br /> **下拉列表**|背景（菜单项）|`Environment.ComboBoxItemMouseOverBackground`|  
|![组合框&#47;删除&#45;下拉列表的悬停](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303年 035_ComboBoxDropdownListHover")<br /><br /> **下拉列表**|前景（文本）|`Environment.ComboBoxItemMouseOverText`|  
|![组合框&#47;删除&#45;下拉列表的悬停](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303年 035_ComboBoxDropdownListHover")<br /><br /> **下拉列表**|边框（菜单项）|`Environment.ComboBoxItemMouseOverBorder`|  
  
 **已设定焦点**  
  
|组件|元素|令牌名称：Color.category|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的组合框输入的字段](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303年 036_ComboBoxInputFieldFocused")<br /><br /> **输入的字段**|背景|`Environment.ComboBoxFocusedBackground`|  
|![已设定焦点的组合框输入的字段](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303年 036_ComboBoxInputFieldFocused")<br /><br /> **输入的字段**|前景（文本）|`Environment.ComboBoxFocusedText`|  
|![已设定焦点的组合框输入的字段](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303年 036_ComboBoxInputFieldFocused")<br /><br /> **输入的字段**|Border|`Environment.ComboBoxFocusedBorder`|  
|![已设定焦点的组合框输入的字段](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303年 036_ComboBoxInputFieldFocused")<br /><br /> **输入的字段**|Separator|`Environment.ComboBoxFocusedButtonSeparator`|  
|![组合框&#47;删除&#45;向下按钮已设定焦点](../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303年 037_ComboBoxDropdownButtonFocused")<br /><br /> **下拉按钮**|背景|`Environment.ComboBoxFocusedButtonBackground`|  
|![组合框&#47;删除&#45;向下按钮已设定焦点](../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303年 037_ComboBoxDropdownButtonFocused")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.ComboBoxFocusedGlyph`|  
  
 **按下**  
  
|组件|元素|令牌名称：Color.category|  
|---------------|-------------|--------------------------------|  
|![组合框输入的字段按下](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303年 038_ComboBoxInputFieldPressed")<br /><br /> **输入的字段**|背景|`Environment.ComboBoxMouseDownBackground`|  
|![组合框输入的字段按下](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303年 038_ComboBoxInputFieldPressed")<br /><br /> **输入的字段**|前景（文本）|`Environment.ComboBoxMouseDownText`|  
|![组合框输入的字段按下](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303年 038_ComboBoxInputFieldPressed")<br /><br /> **输入的字段**|Border|`Environment.ComboBoxMouseDownBorder`|  
|![组合框输入的字段按下](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303年 038_ComboBoxInputFieldPressed")<br /><br /> **输入的字段**|Separator|`Environment.ComboBoxMouseDownSeparator`|  
|![组合框&#47;删除&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303年 039_ComboBoxDropdownButtonPressed")<br /><br /> **下拉按钮**|背景|`Environment.ComboBoxButtonMouseDownBackground`|  
|![组合框&#47;删除&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303年 039_ComboBoxDropdownButtonPressed")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.ComboBoxMouseDownGlyph`|  
  
 已禁用  
  
|组件|元素|令牌名称：Color.category|  
|---------------|-------------|--------------------------------|  
|![组合框输入的字段已禁用](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303年 041_ComboBoxInputFieldDisabled")<br /><br /> **输入的字段**|背景|`Environment.ComboBoxDisabledBackground`|  
|![组合框输入的字段已禁用](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303年 041_ComboBoxInputFieldDisabled")<br /><br /> **输入的字段**|前景（文本）|`Environment.ComboBoxDisabledText`|  
|![组合框输入的字段已禁用](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303年 041_ComboBoxInputFieldDisabled")<br /><br /> **输入的字段**|Border|`Environment.ComboBoxDisabledBorder`|  
|![组合框输入的字段已禁用](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303年 041_ComboBoxInputFieldDisabled")<br /><br /> **输入的字段**|Separator|无分隔符|  
|![组合框&#47;删除&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303年 040_ComboBoxDropdownButtonDisabled")<br /><br /> **下拉按钮**|背景|None|  
|![组合框&#47;删除&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303年 040_ComboBoxDropdownButtonDisabled")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.ComboBoxDisabledGlyph`|  
  
##### <a name="BKMK_CommandDropDown"></a> 下拉列表  
  
> [!IMPORTANT]
> 下拉列表类似于组合框，但缺少可编辑文本区域。 如果下拉列表包含可编辑文本区域，请使用位于 [Combo box](../misc/shared-colors.md#BKMK_CommandComboBox)下的颜色标记。  
  
 ![删除&#45;向下红线](../extensibility/ux-guidelines/media/0303-042-dropdownredline.png "0303年 042_DropdownRedline")  
  
 使用...  
 当创建自定义下拉列表控件时。  
  
请勿使用...  
- 对于不类似于下拉列表的任何内容。  

- 对于组合框或拆分按钮。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;下选择字段](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303年 043_DropdownSelectionField")<br /><br /> **选择字段**|背景|`Environment.DropDownBackground`|  
|![删除&#45;下选择字段](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303年 043_DropdownSelectionField")<br /><br /> **选择字段**|前景（文本）|`DropDownText`|  
|![删除&#45;下选择字段](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303年 043_DropdownSelectionField")<br /><br /> **选择字段**|Border|`DropDownBorder`|  
|![删除&#45;下选择字段](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303年 043_DropdownSelectionField")<br /><br /> **选择字段**|Separator|无分隔符|  
|![删除&#45;向下按钮](../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303年 044_DropdownButton")<br /><br /> **下拉按钮**|背景|None|  
|![删除&#45;向下按钮](../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303年 044_DropdownButton")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.DropDownGlyph`|  
|![删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303年 045_DropdownList")<br /><br /> **下拉列表**|背景|`Environment.DropDownPopupBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303年 045_DropdownList")<br /><br /> **下拉列表**|前景（文本）|`Environment.ComboBoxItemText`|  
|![删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303年 045_DropdownList")<br /><br /> **下拉列表**|Border|`Environment.DropDownPopupBorder`|  
|![删除&#45;列表中向下](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303年 045_DropdownList")<br /><br /> **下拉列表**|阴影|`Environment.DropShadowBackground`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;下选择字段的悬停](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303年 046_DropdownSelectionFieldHover")<br /><br /> **选择字段**|背景|`Environment.DropDownMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![删除&#45;下选择字段的悬停](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303年 046_DropdownSelectionFieldHover")<br /><br /> **选择字段**|前景（文本）|`Environment.DropDownMouseOverText`|  
|![删除&#45;下选择字段的悬停](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303年 046_DropdownSelectionFieldHover")<br /><br /> **选择字段**|Border|`Environment.DropDownMouseOverBorder`|  
|![删除&#45;下选择字段的悬停](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303年 046_DropdownSelectionFieldHover")<br /><br /> **选择字段**|Separator|`Environment.DropDownButtonMouseOverSeparator`|  
|![删除&#45;向下按钮上悬停](../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303年 047_DropdownButtonHover")<br /><br /> **下拉按钮**|背景|`Environment.DropDownButtonMouseOverBackground`|  
|![删除&#45;向下按钮上悬停](../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303年 047_DropdownButtonHover")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.DropDownMouseOverGlyph`|  
|![删除&#45;悬停时的列表中向下](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303年 048_DropdownListHover")<br /><br /> **下拉列表**|背景（菜单项）|`Environment.ComboBoxItemMouseOverBackground`|  
|![删除&#45;悬停时的列表中向下](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303年 048_DropdownListHover")<br /><br /> **下拉列表**|前景（文本）|`Environment.ComboBoxItemMouseOverText`|  
|![删除&#45;悬停时的列表中向下](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303年 048_DropdownListHover")<br /><br /> **下拉列表**|边框（菜单项）|`Environment.ComboBoxItemMouseOverBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;下按下的选择字段](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303年 049_DropdownSelectionFieldPressed")<br /><br /> **选择字段**|背景|`Environment.DropDownMouseDownBackground`|  
|![删除&#45;下按下的选择字段](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303年 049_DropdownSelectionFieldPressed")<br /><br /> **选择字段**|前景（文本）|`Environment.DropDownMouseDownText`|  
|![删除&#45;下按下的选择字段](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303年 049_DropdownSelectionFieldPressed")<br /><br /> **选择字段**|Border|`Environment.DropDownMouseDownBorder`|  
|![删除&#45;下按下的选择字段](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303年 049_DropdownSelectionFieldPressed")<br /><br /> **选择字段**|Separator|`Environment.DropDownButtonMouseDownSeparator`|  
|![删除&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303年 050_DropdownButtonPressed")<br /><br /> **下拉按钮**|背景|`Environment.DropDownButtonMouseDownBackground`|  
|![删除&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303年 050_DropdownButtonPressed")<br /><br /> **下拉按钮**|前景（标志符号）|`Environment.DropDownMouseDownGlyph`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;下选择字段已禁用](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303年 051_DropdownSelectionFieldDisabled")|背景|`Environment.DropDownDisabledBackground`|  
|![删除&#45;下选择字段已禁用](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303年 051_DropdownSelectionFieldDisabled")|前景（文本）|`Environment.DropDownDisabledText`|  
|![删除&#45;下选择字段已禁用](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303年 051_DropdownSelectionFieldDisabled")|Border|`Environment.DropDownDisabledBorder`|  
|![删除&#45;下选择字段已禁用](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303年 051_DropdownSelectionFieldDisabled")|Separator|无分隔符|  
|![删除&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303年 052_DropdownButtonDisabled")|背景|不适用|  
|![删除&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303年 052_DropdownButtonDisabled")|前景（标志符号）|`Environment.DropDownDisabledGlyph`|  
  
##### <a name="split-button"></a>“拆分”按钮  
 拆分按钮与其他命令栏控件（如按钮、菜单和命令栏文本）共享许多令牌名称。 为方便起见，在此处重复了所有必要的操作和下拉按钮令牌名称。 拆分按钮下拉列表是命令栏 [Menus](../misc/shared-colors.md#BKMK_CommandMenus)的实现。  
  
 ![拆分按钮红线](../extensibility/ux-guidelines/media/0303-053-splitbuttonredline.png "0303年 053_SplitButtonRedline")  
  
 使用...  
 当构建自定义拆分按钮时。  
  
请勿使用...  
- 对于其他类型的按钮。  

- 在指定组合之外的任何背景/前景组合中。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![拆分按钮](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303年 054_SplitButton")<br /><br /> **拆分按钮 （默认值）**|背景|None|  
|![拆分按钮](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303年 054_SplitButton")<br /><br /> **拆分按钮 （默认值）**|前景（文本）|`Environment.CommandBarTextActive`|  
|![拆分按钮](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303年 054_SplitButton")<br /><br /> **拆分按钮 （默认值）**|前景（标志符号）|`Environment.CommandBarSplitButtonGlyph`|  
|![拆分按钮](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303年 054_SplitButton")<br /><br /> **拆分按钮 （默认值）**|Border|不适用|  
|![拆分按钮](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303年 054_SplitButton")<br /><br /> **拆分按钮 （默认值）**|Separator|不适用|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![拆分按钮上悬停](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303年 055_SplitButtonHover")<br /><br /> **拆分按钮 （悬停）**|背景|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![拆分按钮上悬停](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303年 055_SplitButtonHover")<br /><br /> **拆分按钮 （悬停）**|前景（文本）|`Environment.CommandBarTextHover`|  
|![拆分按钮上悬停](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303年 055_SplitButtonHover")<br /><br /> **拆分按钮 （悬停）**|前景（标志符号）|`Environment.CommandBarSplitButtonMouseOverGlyph`|  
|![拆分按钮上悬停](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303年 055_SplitButtonHover")<br /><br /> **拆分按钮 （悬停）**|Border|`Environment.CommandBarBorder`|  
|![拆分按钮上悬停](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303年 055_SplitButtonHover")<br /><br /> **拆分按钮 （悬停）**|Separator|`Environment.CommandBarSplitButtonSeparator`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![拆分按钮按下](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303年 056_SplitButtonPressed")<br /><br /> **拆分按钮 （按下）**|背景|`Environment.CommandBarMouseDownBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![拆分按钮按下](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303年 056_SplitButtonPressed")<br /><br /> **拆分按钮 （按下）**|前景（文本）|`Environment.CommandBarTextMouseDown`|  
|![拆分按钮按下](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303年 056_SplitButtonPressed")<br /><br /> **拆分按钮 （按下）**|前景（标志符号）|`Environment.CommandBarSplitButtonMouseDownGlyph`|  
|![拆分按钮按下](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303年 056_SplitButtonPressed")<br /><br /> **拆分按钮 （按下）**|Border|`Environment.CommandBarBorder`|  
|![拆分按钮按下](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303年 056_SplitButtonPressed")<br /><br /> **拆分按钮 （按下）**|Separator|不适用|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![拆分按钮禁用](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303年 057_SplitButtonDisabled")<br /><br /> **拆分按钮 （禁用）**|背景|不适用|  
|![拆分按钮禁用](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303年 057_SplitButtonDisabled")<br /><br /> **拆分按钮 （禁用）**|前景（文本）|`Environment.ComboBoxItemTextInactive`|  
|![拆分按钮禁用](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303年 057_SplitButtonDisabled")<br /><br /> **拆分按钮 （禁用）**|前景（标志符号）|`Environment.CommandBarTextInactive`|  
|![拆分按钮禁用](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303年 057_SplitButtonDisabled")<br /><br /> **拆分按钮 （禁用）**|Border|不适用|  
|![拆分按钮禁用](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303年 057_SplitButtonDisabled")<br /><br /> **拆分按钮 （禁用）**|Separator|不适用|  
  
##### <a name="more-options-and-overflow-buttons"></a>“更多选项”和“溢出”按钮  
 通过添加或删除相关命令栏按钮来自定义命令栏组时，可使用“更多选项”按钮。 命令栏由于水平空间不足而被截断，以及在单击操作中显示包含无法显示的命令栏按钮的菜单时，会出现“溢出”按钮。 这两个按钮的颜色通过一组相同的标记名称进行控制。  
  
 ![更多选项红线](../extensibility/ux-guidelines/media/0303-058-moreoptionsredline.png "0303年 058_MoreOptionsRedline")  
  
 使用...  
 对于自定义“更多选项”或“溢出”按钮。  
  
 请勿使用...  
 对于功能不与“更多选项”或“溢出”按钮类似的按钮。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![更多选项](../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303年 059_MoreOptions")<br /><br /> **更多选项**|背景|`Environment.CommandBarOptionsBackground`|  
|![更多选项](../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303年 059_MoreOptions")<br /><br /> **更多选项**|前景（标志符号）|`Environment.CommandBarOptionsGlyph`|  
|![溢出按钮](../extensibility/ux-guidelines/media/0303-060-overflow.png "0303年 060_Overflow")<br /><br /> **Overflow**|背景|`Environment.CommandBarOptionsBackground`|  
|![溢出按钮](../extensibility/ux-guidelines/media/0303-060-overflow.png "0303年 060_Overflow")<br /><br /> **Overflow**|前景（标志符号）|`Environment.CommandBarOptionsGlyph`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的更多选项](../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303年 061_MoreOptionsHover")<br /><br /> **更多选项**|背景|`Environment.CommandBarOptionsMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停时的更多选项](../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303年 061_MoreOptionsHover")<br /><br /> **更多选项**|前景（标志符号）|`Environment.CommandBarOptionsMouseDownGlyph`|  
|![悬停时的溢出](../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303年 062_OverflowOptions")<br /><br /> **Overflow**|背景|`Environment.CommandBarOptionsMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停时的溢出](../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303年 062_OverflowOptions")<br /><br /> **Overflow**|前景（标志符号）|`Environment.CommandBarOptionsMouseDownGlyph`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![更多选项按下](../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303年 063_MoreOptionsPressed")<br /><br /> **更多选项**|背景|`Environment.CommandBarOptionsMouseDownBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![更多选项按下](../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303年 063_MoreOptionsPressed")<br /><br /> **更多选项**|前景（标志符号）|`Environment.CommandBarOptionsMouseDownGlyph`|  
|![按下的溢出](../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303年 064_OverflowPressed")<br /><br /> **Overflow**|背景|`Environment.CommandBarOptionsMouseDownBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![按下的溢出](../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303年 064_OverflowPressed")<br /><br /> **Overflow**|前景（标志符号）|`Environment.CommandBarOptionsMouseDownGlyph`|  
  
### <a name="document-windows"></a>文档窗口  
 无需复制文档窗口，因为它们由 Visual Studio 环境提供。 但是，你可能会决定要利用文档窗口中使用的颜色，以便你的 UI 显示方式始终与这部分 Visual Studio 环境一致。  
  
 使用文档窗口颜色标记时，必须小心地仅将它们用于类似元素，并且始终成对使用。 如果不这样做，则会在 UI 中遇到意外结果。  
  
#### <a name="document-window-frame"></a>文档窗口框架  
 文档窗口可以在 IDE 中停靠或作为单独窗口浮动。 文档窗口在 IDE 外部浮动时，它仍然位于文档井中，具有与作为 IDE 一部分时相同的背景、边框、文本和选项卡颜色。 但是，文档位于具有自己的背景、边框和文本颜色的框架中。 当工具窗口停靠在文档井中时，它们会从文档窗口标记名称继承其选项卡的行为和颜色。  
  
 ![停靠的文档窗口红线](../extensibility/ux-guidelines/media/0303-065-dockeddocumentwindowredline.png "0303年 065_DockedDocumentWindowRedline")  
  
 **停靠的文档窗口**  
  
 ![浮动文档窗口红线](../extensibility/ux-guidelines/media/0303-066-floatingdocumentwindowredline.png "0303年 066_FloatingDocumentWindowRedline")  
  
 **浮动文档窗口**  
  
 使用...  
 在其中创建要与文档窗口匹配的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|文档：停靠或浮动|背景|取决于文档类型|  
|文档：停靠或浮动|前景（文本）|取决于文档类型|  
|文档：停靠或浮动|Border|`Environment.ToolWindowBorder`|  
|![已设定焦点的框架](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303年 067_FrameFocused")<br /><br /> **框架： 浮动、 已设定焦点**|背景|`Environment.ToolWindowFloatingFrame`|  
|![已设定焦点的框架](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303年 067_FrameFocused")<br /><br /> **框架： 浮动、 已设定焦点**|前景（文本）|`Environment.ToolWindowFloatingFrame`|  
|![已设定焦点的框架](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303年 067_FrameFocused")<br /><br /> **框架： 浮动、 已设定焦点**|前景（标志符号）|`Environment.RaftedWindowButtonActiveGlyph`|  
|![已设定焦点的框架](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303年 067_FrameFocused")<br /><br /> **框架： 浮动、 已设定焦点**|Border|`Environment.MainWindowActiveDefaultBorder`|  
|![已设定焦点的框架](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303年 067_FrameFocused")<br /><br /> **框架： 浮动、 已设定焦点**|边框（标志符号）|`Environment.RaftedWindowButtonActiveBorder`<br /><br /> 设置为透明|  
|![失去焦点的框架](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303年 068_FrameUnfocused")<br /><br /> **框架： 浮动、 失去焦点**|背景|`Environment.ToolWindowFloatingFrameInactive`|  
|![失去焦点的框架](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303年 068_FrameUnfocused")<br /><br /> **框架： 浮动、 失去焦点**|前景（文本）|`Environment.ToolWindowFloatingFrameInactive`|  
|![失去焦点的框架](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303年 068_FrameUnfocused")<br /><br /> **框架： 浮动、 失去焦点**|前景（标志符号）|`Environment.RaftedWindowButtonInactiveGlyph`|  
|![失去焦点的框架](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303年 068_FrameUnfocused")<br /><br /> **框架： 浮动、 失去焦点**|Border|`Environment.MainWindowInactiveBorder`|  
|![失去焦点的框架](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303年 068_FrameUnfocused")<br /><br /> **框架： 浮动、 失去焦点**|边框（标志符号）|`Environment.RaftedWindowButtonInactiveBorder`<br /><br /> 设置为透明|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的设定焦点的框架](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303年 069_FrameFocusedHover")<br /><br /> **框架： 浮动、 已设定焦点**|背景（标志符号）|`Environment.RaftedWindowButtonHoverActive`|  
|![悬停时的设定焦点的框架](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303年 069_FrameFocusedHover")<br /><br /> **框架： 浮动、 已设定焦点**|前景（标志符号）|`Environment.RaftedWindowButtonHoverActiveGlyph`|  
|![悬停时的设定焦点的框架](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303年 069_FrameFocusedHover")<br /><br /> **框架： 浮动、 已设定焦点**|边框（标志符号）|`Environment.RaftedWindowButtonHoverActiveBorder`|  
|![悬停时的失去焦点的框架](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303年 070_FrameUnfocusedHover")<br /><br /> **框架： 浮动、 失去焦点**|背景（标志符号）|`EnvironmentRaftedWindowButtonHoverInactive`|  
|![悬停时的失去焦点的框架](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303年 070_FrameUnfocusedHover")<br /><br /> **框架： 浮动、 失去焦点**|前景（标志符号）|`Environment.RaftedWindowButtonHoverInactiveGlyph`|  
|![悬停时的失去焦点的框架](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303年 070_FrameUnfocusedHover")<br /><br /> **框架： 浮动、 失去焦点**|边框（标志符号）|`Environment.RaftedWindowButtonHoverInactiveBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![设定焦点的框架按下](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303年 071_FrameFocusedPressed")<br /><br /> **框架： 浮动、 已设定焦点**|背景（标志符号）|`Environment.RaftedWindowButtonDown`|  
|![设定焦点的框架按下](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303年 071_FrameFocusedPressed")<br /><br /> **框架： 浮动、 已设定焦点**|前景（标志符号）|`Environment.RaftedWindowButtonDownGlyph`|  
|![设定焦点的框架按下](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303年 071_FrameFocusedPressed")<br /><br /> **框架： 浮动、 已设定焦点**|边框（标志符号）|`Environment.RaftedWindowButtonDownBorder`|  
  
#### <a name="document-tabs"></a>文档选项卡  
 文档选项卡位于选项卡通道中，以指示当前打开的文档，以及当前选择或活动的文档。 如果用户将工具窗口置于文档选项卡通道中，则这些窗口也可以在其中停靠。 在此情况下，它们使用与文档窗口相同的选项卡颜色。 如果你在创建要始终与文档窗口颜色匹配的 UI（包括主题更新，或如果安装新主题），则引用这些颜色标记。  
  
 ![文档选项卡红线](../extensibility/ux-guidelines/media/0303-072-documenttabredline.png "0303年 072_DocumentTabRedline")  
  
 使用...  
 在其中创建要与文档选项卡匹配并自动选取主题更新或新主题颜色的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
##### <a name="open-document-tabs"></a>打开文档选项卡  
 每个打开的文档都在文档选项卡通道中具有显示其名称的选项卡。 文档可以处于已选定状态，或在后台打开，其选项卡会反映这些状态：  
  
- 已选定选项卡表示当前显示在文档井中的文档。 已选定选项卡具有沿文档井上边缘扩展的文档边框。  
  
- 背景选项卡为不是当前已选定选项卡的任何文档选项卡。单击之后，它们会成为已选定选项卡，并从这些标记名称获取所有背景、边框和文本颜色。  
  
  ![打开的文档选项卡红线](../extensibility/ux-guidelines/media/0303-073-opendocumenttabredline.png "0303年 073_OpenDocumentTabRedline")  
  
  使用...  
  当创建自定义文档选项卡时。  
  
  请勿使用...  
  - 对于临时（预览）选项卡。  
  
- 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
##### <a name="selected-tab"></a>已选定选项卡  
 **已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303年 074_SelectedTabFocused")<br /><br /> **已设定焦点的选定的文档选项卡**|背景|`Environment.FileTabSelectedGradientTop`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![已设定焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303年 074_SelectedTabFocused")<br /><br /> **已设定焦点的选定的文档选项卡**|前景（文本）|`Environment.FileTabSelectedText`|  
|![已设定焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303年 074_SelectedTabFocused")<br /><br /> **已设定焦点的选定的文档选项卡**|Border|`Environment.FileTabSelectedBorder`<br /><br /> 设置为与背景相同的颜色。|  
|![已设定焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303年 074_SelectedTabFocused")<br /><br /> **已设定焦点的选定的文档选项卡**|文档边框|`Environment.FileTabDocumentBorderBackground`|  
  
 **失去焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![失去焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303年 075_SelectedTabUnfocused")<br /><br /> **所选的文档选项卡、 失去焦点**|背景|`Environment.FileTabInactiveGradientTop`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![失去焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303年 075_SelectedTabUnfocused")<br /><br /> **所选的文档选项卡、 失去焦点**|前景（文本）|`Environment.FileTabInactiveText`|  
|![失去焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303年 075_SelectedTabUnfocused")<br /><br /> **所选的文档选项卡、 失去焦点**|Border|`Environment.FileTabInactiveBorder`<br /><br /> 设置为与背景相同的颜色。|  
|![失去焦点的选定选项卡](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303年 075_SelectedTabUnfocused")<br /><br /> **所选的文档选项卡、 失去焦点**|文档边框|`Environment.FileTabInactiveDocumentBorderBackground`|  
  
##### <a name="background-tab"></a>“背景”选项卡  
 **默认**  
  
|组件|元素|令牌名称：Color.category|  
|---------------|-------------|--------------------------------|  
|![背景选项卡](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303年 076_BackgroundTab")<br /><br /> **背景选项卡默认值**|背景|`Environment.FileTabBackground`|  
|![背景选项卡](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303年 076_BackgroundTab")<br /><br /> **背景选项卡默认值**|前景（文本）|`Environment.FileTabText`|  
|![背景选项卡](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303年 076_BackgroundTab")<br /><br /> **背景选项卡默认值**|Border|`Environment.FileTabBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
 **Hover**  
  
|组件|元素|令牌名称：Color.category|  
|---------------|-------------|--------------------------------|  
|![悬停背景选项卡](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303年 077_BackgroundTabHover")<br /><br /> **悬停背景选项卡**|背景|`Environment.FileTabHotGradientTop`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停背景选项卡](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303年 077_BackgroundTabHover")<br /><br /> **悬停背景选项卡**|前景（文本）|`Environment.FileTabHotText`|  
|![悬停背景选项卡](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303年 077_BackgroundTabHover")<br /><br /> **悬停背景选项卡**|Border|`Environment.FileTabHotBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
##### <a name="preview-tab"></a>预览选项卡  
 当用户在解决方案资源管理器工具窗口中单击某个项时，预览选项卡会出现在文档选项卡通道右侧。 它充当文档的预览，还为用户提供用于使文档在文档选项卡通道左侧保持打开状态的选项。 一次只能打开一个预览选项卡。 预览选项卡具有背景和选定状态（与打开的选项卡一样），可以在其活动状态下具有焦点或失去焦点。  
  
 ![预览选项卡红线](../extensibility/ux-guidelines/media/0303-078-previewtabredline.png "0303年 078_PreviewTabRedline")  
  
 使用...  
 在其中创建临时预览，并且希望一些元素与当前预览选项卡颜色匹配的临时预览。  
  
请勿使用...  
- 对于不是临时（预览）的任何种类的文档或选项卡。  

- 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
  **已选定的预览选项卡上：已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303年 079_PreviewTabFocused")<br /><br /> **已设定焦点的预览选项卡**|背景|`Environment.FileTabProvisionalSelectedActive`|  
|![已设定焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303年 079_PreviewTabFocused")<br /><br /> **已设定焦点的预览选项卡**|前景（文本）|`Environment.FileTabProvisionalSelectedActiveForeground`|  
|![已设定焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303年 079_PreviewTabFocused")<br /><br /> **已设定焦点的预览选项卡**|Border|`Environment.FileTabProvisionalSelectedActiveBorder`<br /><br /> 设置为与背景相同的颜色。|  
|![已设定焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303年 079_PreviewTabFocused")<br /><br /> **已设定焦点的预览选项卡**|文档边框|`Environment.FileTabProvisionalSelectedActiveBorder`|  
  
 **已选定的预览选项卡上：失去焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![失去焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303年 080_PreviewTabUnfocused")<br /><br /> **失去焦点的预览选项卡**|背景|`Environment.FileTabProvisionalSelectedInactive`|  
|![失去焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303年 080_PreviewTabUnfocused")<br /><br /> **失去焦点的预览选项卡**|前景（文本）|`Environment.FileTabProvisionalSelectedInactiveForeground`|  
|![失去焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303年 080_PreviewTabUnfocused")<br /><br /> **失去焦点的预览选项卡**|Border|`Environment.FileTabProvisionalSelectedInactiveBorder`|  
|![失去焦点的预览选项卡](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303年 080_PreviewTabUnfocused")<br /><br /> **失去焦点的预览选项卡**|文档边框|`Environment.FileTabProvisionalSelectedInactiveBorder`|  
  
 **背景预览选项卡：默认值**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![预览背景选项卡](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303年 081_PreviewBackgroundTab")<br /><br /> **预览选项卡背景选项卡**|背景|`Environment.FileTabProvisionalInactive`|  
|![预览背景选项卡](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303年 081_PreviewBackgroundTab")<br /><br /> **预览选项卡背景选项卡**|前景（文本）|`Environment.FileTabProvisionalInactiveForeground`|  
|![预览背景选项卡](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303年 081_PreviewBackgroundTab")<br /><br /> **预览选项卡背景选项卡**|Border|`Environment.FileTabProvisionalInactiveBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
 **背景预览选项卡：Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的预览背景选项卡](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303年 082_PreviewBackgroundTabHover")<br /><br /> **悬停时的预览选项卡的背景选项卡**|背景|`Environment.FileTabProvisionalHover`|  
|![悬停时的预览背景选项卡](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303年 082_PreviewBackgroundTabHover")<br /><br /> **悬停时的预览选项卡的背景选项卡**|前景（文本）|`Environment.FileTabProvisionalHoverForeground`|  
|![悬停时的预览背景选项卡](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303年 082_PreviewBackgroundTabHover")<br /><br /> **悬停时的预览选项卡的背景选项卡**|Border|`Environment.FileTabProvisionalHoverBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
##### <a name="document-overflow-button"></a>文档溢出按钮  
 如果有一个或多个文档打开，则无论当前配置中是否有垂直空间可容纳所有文档选项卡，都会提供文档溢出按钮。 通过 **CommandBarMenu** 颜色（请参见 [Menus](../misc/shared-colors.md#BKMK_CommandMenus)）控制的文档溢出下拉菜单会显示所有打开的文档（可见或隐藏）的列表，溢出标志符号会根据是否所有打开的文档都显示在选项卡通道中而更改。  
  
 ![溢出红线](../extensibility/ux-guidelines/media/0303-083-overflowredline.png "0303年 083_OverflowRedline")  
  
使用...  
当创建自定义文档溢出按钮时。  

请勿使用...  
- 对于不类似于溢出按钮的 UI。  

- 对于命令栏溢出按钮。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Overflow](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **文档溢出按钮**|背景|`Environment.DocWellOverflowButtonBackground`|  
|![Overflow](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **文档溢出按钮**|前景（标志符号）|`Environment.DocWellOverflowButtonGlyph`|  
|![Overflow](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **文档溢出按钮**|Border|不适用|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的溢出](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303年 085_OverflowHover")<br /><br /> **悬停时的文档溢出按钮**|背景|`Environment.DocWellOverflowButtonMouseOverBackground`|  
|![悬停时的溢出](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303年 085_OverflowHover")<br /><br /> **悬停时的文档溢出按钮**|前景（标志符号）|`Environment.DocWellOverflowButtonMouseOverGlyph`|  
|![悬停时的溢出](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303年 085_OverflowHover")<br /><br /> **悬停时的文档溢出按钮**|Border|`Environment.DocWellOverflowButtonMouseOverBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下的溢出](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303年 086_OverflowPressed")<br /><br /> **按下文档溢出按钮**|背景|`Environment.DocWellOverflowButtonMouseDownBackground`|  
|![按下的溢出](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303年 086_OverflowPressed")<br /><br /> **按下文档溢出按钮**|前景（标志符号）|`Environment.DocWellOverflowButtonMouseDownGlyph`|  
|![按下的溢出](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303年 086_OverflowPressed")<br /><br /> **按下文档溢出按钮**|Border|`Environment.DocWellOverflowButtonMouseDownBorder`|  
  
### <a name="tool-windows"></a>工具窗口  
 无需复制工具窗口，因为它们由 Visual Studio 环境提供。 但是，你可能会决定要利用工具窗口中使用的颜色，以便你的 UI 显示方式始终与这部分 Visual Studio 环境一致。  
  
 ![工具窗口红线](../extensibility/ux-guidelines/media/0303-087-toolwindowredline.png "0303年 087_ToolWindowRedline")  
  
 使用...  
 在其中创建要与工具窗口匹配的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
#### <a name="tool-window-frame"></a>工具窗口框架  
 Visual Studio 中的工具窗口用于许多不同的任务，可以采用多个不同状态中的一个状态存在。 如果工具窗口处于打开状态，则它可以分配到文档区域四边的任何一边。 工具窗口还可以在 IDE 外部浮动，从而使它们可以在用户屏幕中的任何位置重新定位。 浮动窗口始终位于 IDE 顶部。 最后，工具窗口可以作为文档窗口停靠，并显示为文档井中的选项卡。 作为文档窗口停靠的工具窗口会使用文档窗口标记名称进行部分着色。  
  
 ![工具窗口框架红线](../extensibility/ux-guidelines/media/0303-088-toolwindowframeredline.png "0303年 088_ToolWindowFrameRedline")  
  
 使用...  
 在其中创建要与工具窗口匹配的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
 **Docked**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![工具窗口停靠](../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303年 089_ToolWindowDocked")|背景|`Environment.ToolWindowBackground`|  
|![工具窗口停靠](../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303年 089_ToolWindowDocked")|Border|`Environment.ToolWindowBorder`|  
  
 **浮动： 已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的工具窗口](../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303年 090_ToolWindowFocused")|背景|`Environment.ToolWindowBackground`|  
|![已设定焦点的工具窗口](../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303年 090_ToolWindowFocused")|Border|`Environment.MainWindowActiveDefaultBorder`|  
  
 **浮动： 失去焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![工具窗口失去焦点](../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303年 091_ToolWindowUnfocused")|背景|`Environment.ToolWindowBackground`|  
|![工具窗口失去焦点](../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303年 091_ToolWindowUnfocused")|Border|`Environment.MainWindowInactiveBorder`|  
  
#### <a name="tool-window-title-bar"></a>工具窗口标题栏  
 标题栏边框不是真实边框，而是横跨标题栏顶部的粗线。 对于其失去焦点的状态，它没有标记名称。  
  
 ![工具窗口标题栏红线](../extensibility/ux-guidelines/media/0303-092-toolwindowtitlebarredline.png "0303年 092_ToolWindowTitleBarRedline")  
  
 使用...  
 在其中创建要与工具窗口匹配的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
 **已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![标题栏已设定焦点](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303年 093_TitleBarFocused")<br /><br /> **已设定焦点的标题栏**|背景|`Environment.TitleBarActiveGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![标题栏已设定焦点](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303年 093_TitleBarFocused")<br /><br /> **已设定焦点的标题栏**|前景（文本）|`Environment.TitleBarActiveText`|  
|![标题栏已设定焦点](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303年 093_TitleBarFocused")<br /><br /> **已设定焦点的标题栏**|Border|`Environment.TitleBarActiveBorder`<br /><br /> 设置为与背景相同的颜色。|  
|![标题栏已设定焦点](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303年 093_TitleBarFocused")<br /><br /> **已设定焦点的标题栏**|拖动句柄|`Environment.TitleBarDragHandleActive`|  
  
 **失去焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![失去焦点的标题栏](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303年 094_TitleBarUnfocused")<br /><br /> **失去焦点的标题栏**|背景|`Environment.TitleBarInactiveGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![失去焦点的标题栏](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303年 094_TitleBarUnfocused")<br /><br /> **失去焦点的标题栏**|前景（文本）|`Environment.TitleBarInactiveText`|  
|![失去焦点的标题栏](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303年 094_TitleBarUnfocused")<br /><br /> **失去焦点的标题栏**|Border|不适用|  
|![失去焦点的标题栏](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303年 094_TitleBarUnfocused")<br /><br /> **失去焦点的标题栏**|拖动句柄|`Environment.TitleBarDragHandle`|  
  
##### <a name="title-bar-buttons"></a>标题栏按钮  
 ![标题栏按钮红线](../extensibility/ux-guidelines/media/0303-095-titlebarbuttonredline.png "0303年 095_TitleBarButtonRedline")  
  
 使用...  
 对于在使用来自工具窗口标题栏的颜色标记的 UI 中出现的按钮。  
  
请勿使用...  
- 对于在其他位置出现的按钮。  

- 在指定组合之外的任何背景/前景组合中。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![标题栏按钮已设定焦点](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303年 096_TitleBarButtonFocused")<br /><br /> **已设定焦点**|背景|不适用|  
|![标题栏按钮已设定焦点](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303年 096_TitleBarButtonFocused")<br /><br /> **已设定焦点**|前景（标志符号）|`Environment.ToolWindowButtonActiveGlyph`|  
|![标题栏按钮已设定焦点](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303年 096_TitleBarButtonFocused")<br /><br /> **已设定焦点**|Border|不适用|  
|![标题栏失去焦点的按钮](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303年 097_TitleBarButtonUnfocused")<br /><br /> **失去焦点**|背景|不适用|  
|![标题栏失去焦点的按钮](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303年 097_TitleBarButtonUnfocused")<br /><br /> **失去焦点**|前景（标志符号）|`Environment.ToolWindowButtonInactiveGlyph`|  
|![标题栏失去焦点的按钮](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303年 097_TitleBarButtonUnfocused")<br /><br /> **失去焦点**|Border|不适用|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的设定焦点的标题栏按钮](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303年 098_TitleBarButtonFocusedHover")<br /><br /> **已设定焦点**|背景|`Environment.ToolWindowButtonHoverActive`|  
|![悬停时的设定焦点的标题栏按钮](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303年 098_TitleBarButtonFocusedHover")<br /><br /> **已设定焦点**|前景（标志符号）|`Environment.ToolWindowButtonHoverActiveGlyph`|  
|![悬停时的设定焦点的标题栏按钮](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303年 098_TitleBarButtonFocusedHover")<br /><br /> **已设定焦点**|Border|`Environment.ToolWindowButtonHoverActiveBorder`|  
|![标题栏按钮悬停时的失去焦点](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303年 099_TitleBarButtonUnfocusedHover")<br /><br /> **失去焦点**|背景|`Environment.ToolWindowButtonHoverInactive`|  
|![标题栏按钮悬停时的失去焦点](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303年 099_TitleBarButtonUnfocusedHover")<br /><br /> **失去焦点**|前景（标志符号）|`Environment.ToolWindowButtonHoverInactiveGlyph`|  
|![标题栏按钮悬停时的失去焦点](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303年 099_TitleBarButtonUnfocusedHover")<br /><br /> **失去焦点**|Border|`Environment.ToolWindowButtonHoverInactiveBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![标题栏按钮已设定焦点，并按下](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303年 100_TitleBarButtonFocusedPressed")<br /><br /> **已设定焦点**|背景|`Environment.ToolWindowButtonDown`|  
|![标题栏按钮已设定焦点，并按下](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303年 100_TitleBarButtonFocusedPressed")<br /><br /> **已设定焦点**|前景（标志符号）|`Environment.ToolWindowButtonDownActiveGlyph`|  
|![标题栏按钮已设定焦点，并按下](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303年 100_TitleBarButtonFocusedPressed")<br /><br /> **已设定焦点**|Border|`Environment.ToolWindowButtonDownBorder`|  
|![失去焦点或按下状态的标题栏按钮](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303年 101_TitleBarButtonUnfocusedPressed")<br /><br /> **失去焦点**|背景|`Environment.ToolWindowButtonDown`|  
|![失去焦点或按下状态的标题栏按钮](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303年 101_TitleBarButtonUnfocusedPressed")<br /><br /> **失去焦点**|前景（标志符号）|`Environment.ToolWindowButtonDownInactiveGlyph`|  
|![失去焦点或按下状态的标题栏按钮](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303年 101_TitleBarButtonUnfocusedPressed")<br /><br /> **失去焦点**|Border|`Environment.ToolWindowButtonDownBorder`|  
  
#### <a name="tool-window-tabs"></a>工具窗口选项卡  
 ![工具窗口选项卡红线](../extensibility/ux-guidelines/media/0303-102-toolwindowtabredline.png "0303年 102_ToolWindowTabRedline")  
  
 使用...  
 在其中创建要与工具窗口匹配的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
 **选定的选项卡**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![工具窗口选项卡已设定焦点](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303年 103_ToolWindowTabFocused")<br /><br /> **已选定、 已设定焦点的工具窗口选项卡**|背景|`Environment.ToolWindowTabSelectedTab`|  
|![工具窗口选项卡已设定焦点](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303年 103_ToolWindowTabFocused")<br /><br /> **已选定、 已设定焦点的工具窗口选项卡**|前景（文本）|`Environment.ToolWindowTabSelectedActiveText`|  
|![工具窗口选项卡已设定焦点](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303年 103_ToolWindowTabFocused")<br /><br /> **已选定、 已设定焦点的工具窗口选项卡**|Border|`Environment.ToolWindowTabSelectedBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![失去焦点的工具窗口选项卡](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303年 104_ToolWindowTabUnfocused")<br /><br /> **已选定、 失去焦点的工具窗口选项卡**|背景|`Environment.ToolWindowTabSelectedTab`|  
|![失去焦点的工具窗口选项卡](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303年 104_ToolWindowTabUnfocused")<br /><br /> **已选定、 失去焦点的工具窗口选项卡**|前景（文本）|`Environment.ToolWindowTabSelectedText`|  
|![失去焦点的工具窗口选项卡](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303年 104_ToolWindowTabUnfocused")<br /><br /> **已选定、 失去焦点的工具窗口选项卡**|Border|`Environment.ToolWindowTabSelectedBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
 **背景选项卡**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![工具窗口背景选项卡](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303年 105_ToolWindowBackgroundTab")<br /><br /> **背景工具窗口选项卡**|背景|`Environment.ToolWindowTabGradientBegin`<br /><br /> 在 Visual Studio 2013 中设置为相同颜色值的梯度停止点。<br /><br /> `Environment.ToolWindowTabGradientEnd`<br /><br /> 在 Visual Studio 2013 中设置为相同颜色值的梯度停止点。|  
|![工具窗口背景选项卡](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303年 105_ToolWindowBackgroundTab")<br /><br /> **背景工具窗口选项卡**|前景（文本）|`Environment.ToolWindowTabText`|  
|![工具窗口背景选项卡](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303年 105_ToolWindowBackgroundTab")<br /><br /> **背景工具窗口选项卡**|Border|`Environment.ToolWindowTabBorder`|  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的工具窗口背景选项卡](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303年 106_ToolWindowBackgroundTabHover")<br /><br /> **悬停时的背景工具窗口选项卡**|背景|`Environment.ToolWindowTabMouseOverBackgroundBegin`<br /><br /> 在 Visual Studio 2013 中设置为相同颜色值的梯度停止点。<br /><br /> `Environment.ToolWindowTabMouseOverBackgroundEnd`<br /><br /> 在 Visual Studio 2013 中设置为相同颜色值的梯度停止点。|  
|![悬停时的工具窗口背景选项卡](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303年 106_ToolWindowBackgroundTabHover")<br /><br /> **悬停时的背景工具窗口选项卡**|前景（文本）|`Environment.ToolWindowTabMouseOverText`|  
|![悬停时的工具窗口背景选项卡](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303年 106_ToolWindowBackgroundTabHover")<br /><br /> **悬停时的背景工具窗口选项卡**|Border|`Environment.ToolWindowTabMouseOverBorder`<br /><br /> 设置为与背景相同的颜色。|  
  
#### <a name="auto-hide-tabs"></a>自动隐藏选项卡  
 ![自动&#45;隐藏红线](../extensibility/ux-guidelines/media/0303-107-autohideredline.png "0303年 107_AutoHideRedline")  
  
 使用...  
 在其中创建要与自动隐藏工具窗口选项卡匹配的 UI 的任何位置。  
  
 请勿使用...  
 对于不希望在 shell 具有主题更新时自动更改的任何 UI。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![自动&#45;隐藏选项卡](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303年 108_AutoHideTab")<br /><br /> **默认自动隐藏选项卡**|背景|`Environment.AutoHideTabBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![自动&#45;隐藏选项卡](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303年 108_AutoHideTab")<br /><br /> **默认自动隐藏选项卡**|前景（文本）|`Environment.AutoHideTabText`|  
|![自动&#45;隐藏选项卡](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303年 108_AutoHideTab")<br /><br /> **默认自动隐藏选项卡**|Border|`Environment.AutoHideTabBorder`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![自动&#45;隐藏选项卡上悬停](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303年 109_AutoHideTabHover")<br /><br /> **悬停时自动隐藏选项卡**|背景|`Environment.AutoHideTabMouseOverBackgroundBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![自动&#45;隐藏选项卡上悬停](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303年 109_AutoHideTabHover")<br /><br /> **悬停时自动隐藏选项卡**|前景（文本）|`Environment.AutoHideTabMouseOverText`|  
|![自动&#45;隐藏选项卡上悬停](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303年 109_AutoHideTabHover")<br /><br /> **悬停时自动隐藏选项卡**|Border|`Environment.AutoHideTabMouseOverBorder`|  
  
### <a name="common-shared-controls"></a>公共共享控件  
 在功能中使用标准 Visual Studio 命令栏时，你可以访问设置了样式的 shell 控件，不应对这些公共控件重新创建模板。 但是，如果需要构建自定义命令栏，则可能还需要构建自定义控件。 在这种情况下，请确保对以下每个控件使用正常标记名称，以便 UI 与 Visual Studio 的其余部分保持一致。  
  
#### <a name="search-box"></a>搜索框  
 只要可能，便使用 Visual Studio 环境提供的公共搜索控件。 搜索框颜色位于 **ShellColors.pkgdef** 文件中“SearchControl”类别中，该文件包含输入字段、操作按钮、下拉按钮和下拉菜单中的标记名称。  
  
 搜索框可以具有多种状态之一，其中一些状态互相排斥：  
  
- “已设定焦点”或“失去焦点”是指光标是否处于文本框中。  
  
- “活动”或“非活动”是指用户是否在文本框中输入了搜索查询。  
  
- “悬停”表示用户将鼠标指针置于搜索框上方（此状态优先于所有其他状态）。  
  
- “已禁用”表示为当前上下文关闭了搜索功能。  
  
  ![搜索框红线](../extensibility/ux-guidelines/media/0303-110-searchboxredline.png "0303年 110_SearchBoxRedline")  
  
  使用...  
  当在设计自定义搜索框时。  
  
  请勿使用...  
  - 对于不是搜索框的任何内容。  
  
- 对于并非希望始终与搜索框 UI 匹配的任何内容。  
  
  **已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303年 111_SearchInputFieldFocused")<br /><br /> **输入的字段**|背景|`SearchControl.FocusedBackground`|  
|![已设定焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303年 111_SearchInputFieldFocused")<br /><br /> **输入的字段**|前景（文本）|`SearchControl.FocusedBackground`|  
|![已设定焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303年 111_SearchInputFieldFocused")<br /><br /> **输入的字段**|Border|`SearchControl.FocusedBorder`|  
|![已设定焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303年 111_SearchInputFieldFocused")<br /><br /> **输入的字段**|Separator|`SearchControl.FocusedDropDownSeparator`|  
|![已设定焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303年 112_SearchActionButtonFocused")<br /><br /> **操作按钮**|背景|None|  
|![已设定焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303年 112_SearchActionButtonFocused")<br /><br /> **操作按钮**|前景（搜索标志符号）|`SearchControl.SearchGlyph`|  
|![已设定焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303年 112_SearchActionButtonFocused")<br /><br /> **操作按钮**|前景（停止标志符号）|`SearchControl.StopGlyph`|  
|![已设定焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303年 112_SearchActionButtonFocused")<br /><br /> **操作按钮**|前景（清除标志符号）|`SearchControl.ClearGlyph`|  
|![已设定焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303年 112_SearchActionButtonFocused")<br /><br /> **操作按钮**|Border|不适用|  
|![搜索下拉&#45;下已设定焦点的按钮](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303年 113_SearchDropdownButtonFocused")<br /><br /> **下拉按钮**|背景|`SearchControl.FocusedDropDownButton`|  
|![搜索下拉&#45;下已设定焦点的按钮](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303年 113_SearchDropdownButtonFocused")<br /><br /> **下拉按钮**|前景（标志符号）|`SearchControl.FocusedDropDownButtonGlyph`|  
|![搜索下拉&#45;下已设定焦点的按钮](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303年 113_SearchDropdownButtonFocused")<br /><br /> **下拉按钮**|Border|`SearchControl.FocusedDropDownButtonBorder`|  
  
 **失去焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![失去焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303年 114_SearchInputFieldUnfocused")<br /><br /> **活动输入的字段**|背景|`SearchControl.SearchActiveBackground`|  
|![失去焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303年 114_SearchInputFieldUnfocused")<br /><br /> **活动输入的字段**|前景（文本）|`SearchControl.SearchActiveBackground`|  
|![失去焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303年 114_SearchInputFieldUnfocused")<br /><br /> **活动输入的字段**|Border|`SearchControl.UnfocusedBorder`|  
|![失去焦点的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303年 114_SearchInputFieldUnfocused")<br /><br /> **活动输入的字段**|Separator|`SearchControl.DropDownSeparator`|  
|![失去焦点并处于非活动状态的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303年 114 1_SearchInputFieldUnfocusedInactive")<br /><br /> **非活动的输入的字段**|背景|`SearchControl.Unfocused`|  
|![失去焦点并处于非活动状态的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303年 114 1_SearchInputFieldUnfocusedInactive")<br /><br /> **非活动的输入的字段**|前景（文本）|`SearchControl.Unfocused`|  
|![失去焦点并处于非活动状态的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303年 114 1_SearchInputFieldUnfocusedInactive")<br /><br /> **非活动的输入的字段**|Border|`SearchControl.UnfocusedBorder`|  
|![失去焦点并处于非活动状态的搜索输入的字段](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303年 114 1_SearchInputFieldUnfocusedInactive")<br /><br /> **非活动的输入的字段**|Separator|`SearchControl.DropDownSeparator`|  
|![失去焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303年 115_SearchActionButtonUnfocused")<br /><br /> **操作按钮**|背景|不适用|  
|![失去焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303年 115_SearchActionButtonUnfocused")<br /><br /> **操作按钮**|前景（搜索标志符号）|`SearchControl.SearchGlyph`|  
|![失去焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303年 115_SearchActionButtonUnfocused")<br /><br /> **操作按钮**|前景（停止标志符号）|`SearchControl.StopGlyph`|  
|![失去焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303年 115_SearchActionButtonUnfocused")<br /><br /> **操作按钮**|前景（清除标志符号）|`SearchControl.ClearGlyph`|  
|![失去焦点的搜索操作按钮](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303年 115_SearchActionButtonUnfocused")<br /><br /> **操作按钮**|Border|不适用|  
|![搜索下拉&#45;向下按钮失去焦点](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303年 116_SearchDropdownButtonUnfocused")<br /><br /> **下拉按钮**|背景|`SearchControl.UnfocusedDropDownButton`|  
|![搜索下拉&#45;向下按钮失去焦点](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303年 116_SearchDropdownButtonUnfocused")<br /><br /> **下拉按钮**|前景（标志符号）|`SearchControl.UnfocusedDropDownButtonGlyph`|  
|![搜索下拉&#45;向下按钮失去焦点](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303年 116_SearchDropdownButtonUnfocused")<br /><br /> **下拉按钮**|Border|`SearchControl.UnfocusedDropDownButtonBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![搜索操作按钮按下](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303年 116 1_SearchActionButtonPressed")<br /><br /> **操作按钮**|背景|`SearchControl.ActionButtonMouseDown`|  
|![搜索操作按钮按下](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303年 116 1_SearchActionButtonPressed")<br /><br /> **操作按钮**|前景（标志符号）|`SearchControl.ActionButtonMouseDownGlyph`|  
|![搜索操作按钮按下](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303年 116 1_SearchActionButtonPressed")<br /><br /> **操作按钮**|Border|`SearchControl.ActionButtonMouseDownBorder`|  
|![搜索下拉&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303年 116 2_SearchDropdownButtonPressed")<br /><br /> **下拉按钮**|背景|`SearchControl.MouseDownDropDownButton`|  
|![搜索下拉&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303年 116 2_SearchDropdownButtonPressed")<br /><br /> **下拉按钮**|前景（标志符号）|`SearchControl.MouseDownDropDownButtonGlyph`|  
|![搜索下拉&#45;向下按钮按下](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303年 116 2_SearchDropdownButtonPressed")<br /><br /> **下拉按钮**|Border|`SearchControl.MouseDownDropDownButtonBorder`|  
  
 **突出显示 （纯文本）**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![搜索输入的字段突出显示](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303年 120_SearchInputFieldHighlight")<br /><br /> **突出显示文本的输入的字段**|背景|`SearchControl.Selection`|  
|![搜索输入的字段突出显示](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303年 120_SearchInputFieldHighlight")<br /><br /> **突出显示文本的输入的字段**|前景（文本）|`SearchControl.FocusedBackground`|  
|![搜索输入的字段突出显示](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303年 120_SearchInputFieldHighlight")<br /><br /> **突出显示文本的输入的字段**|Border|None|  
|![搜索输入的字段突出显示](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303年 120_SearchInputFieldHighlight")<br /><br /> **突出显示文本的输入的字段**|Separator|`SearchControl.FocusedDropDownSeparator`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![禁用的搜索输入的字段](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303年 121_SearchInputFieldDisabled")<br /><br /> **输入的字段**|背景|`SearchControl.Disabled`|  
|![禁用的搜索输入的字段](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303年 121_SearchInputFieldDisabled")<br /><br /> **输入的字段**|前景（文本）|`SearchControl.Disabled`|  
|![禁用的搜索输入的字段](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303年 121_SearchInputFieldDisabled")<br /><br /> **输入的字段**|Border|`SearchControl.DisabledBorder`|  
|![禁用的搜索输入的字段](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303年 121_SearchInputFieldDisabled")<br /><br /> **输入的字段**|Separator|`SearchControl.DropDownSeparator`|  
|![禁用的搜索操作按钮](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303年 122_SearchActionButtonDisabled")<br /><br /> **操作按钮**|背景|None|  
|![禁用的搜索操作按钮](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303年 122_SearchActionButtonDisabled")<br /><br /> **操作按钮**|前景（标志符号）|`SearchControl.ActionButtonDisabledGlyph`|  
|![禁用的搜索操作按钮](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303年 122_SearchActionButtonDisabled")<br /><br /> **操作按钮**|Border|None|  
|![搜索下拉&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303年 123_SearchDropdownButtonDisabled")<br /><br /> **下拉按钮**|背景|None|  
|![搜索下拉&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303年 123_SearchDropdownButtonDisabled")<br /><br /> **下拉按钮**|前景（标志符号）|`SearchControl.DisabledDownButtonGlyph`|  
|![搜索下拉&#45;向下按钮禁用](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303年 123_SearchDropdownButtonDisabled")<br /><br /> **下拉按钮**|Border|None|  
  
##### <a name="search-drop-down-lists"></a>搜索下拉列表  
 搜索框下拉菜单可能比 Visual Studio 中的其他下拉菜单稍微复杂一些。 “建议的搜索”和“搜索选项”部分可以在菜单中单独或一起出现，各自分别进行着色。 当这两个部分一起出现时，还会有一条线分隔它们，并且有一个边框环绕整个下拉菜单。  
  
 ![搜索下拉&#45;向下红线](../extensibility/ux-guidelines/media/0303-124-searchdropdownredline.png "0303年 124_SearchDropdownRedline")  
  
使用...  
- 当创建自定义搜索下拉列表时。  

- 正确列表组件的正确标记名称。  

请勿使用...  
- 对于在其他上下文中出现的下拉列表。  

- 在指定组合之外的任何背景/前景组合中。  
  
  **默认 （无任何其他状态）**  
  
|元素|令牌名称：Category.color|  
|-------------|--------------------------------|  
|Border|`SearchControl.PopupBorder`|  
|Separator|`SearchControl.PopupSectionHeaderSeparator`|  
|阴影|`Environment.DropShadowBackground`|  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![建议的搜索](../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303年 125_SearchSuggested")<br /><br /> **建议的搜索**|背景|`SearchControl.PopupItemsListBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![建议的搜索](../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303年 125_SearchSuggested")<br /><br /> **建议的搜索**|前景（文本）|`SearchControl.PopupItemText`|  
|![搜索复选框](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303年 126_SearchCheckbox")<br /><br /> **搜索选项 （复选框）**|背景|`SearchControl.PopupSectionBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索选项](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303年 127_SearchOptions")<br /><br /> **搜索选项 （链接）**|背景|`SearchControl.PopupSectionBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索复选框](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303年 126_SearchCheckbox")<br /><br /> **搜索选项 （复选框）**|前景（复选框文本）|`SearchControl.PopupCheckboxText`|  
|![搜索选项](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303年 127_SearchOptions")<br /><br /> **搜索选项 （链接）**|前景（复选框文本）|`SearchControl.PopupCheckboxText`|  
|![搜索复选框](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303年 126_SearchCheckbox")<br /><br /> **搜索选项 （复选框）**|前景（链接文本）|`SearchControl.PopupButtonText`|  
|![搜索选项](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303年 127_SearchOptions")<br /><br /> **搜索选项 （链接）**|前景（链接文本）|`SearchControl.PopupButtonText`|  
|![搜索复选框](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303年 126_SearchCheckbox")<br /><br /> **搜索选项 （复选框）**|标题背景|`SearchControl.PopupSectionHeaderGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索选项](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303年 127_SearchOptions")<br /><br /> **搜索选项 （链接）**|标题背景|`SearchControl.PopupSectionHeaderGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索复选框](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303年 126_SearchCheckbox")<br /><br /> **搜索选项 （复选框）**|前景（标题文本）|`SearchControl.PopupSectionHeaderText`|  
|![搜索选项](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303年 127_SearchOptions")<br /><br /> **搜索选项 （链接）**|前景（标题文本）|`SearchControl.PopupSectionHeaderText`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的建议的搜索](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303年 128_SearchSuggestedHover")<br /><br /> **建议的搜索**|背景|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停时的建议的搜索](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303年 128_SearchSuggestedHover")<br /><br /> **建议的搜索**|前景（文本）|`SearchControl.PopupMouseOverItemText`|  
|![悬停时的建议的搜索](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303年 128_SearchSuggestedHover")<br /><br /> **建议的搜索**|Border|`SearchControl.PopupControlMouseOverBorder`|  
|![悬停时的搜索复选框](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303年 129_SearchCheckboxHover")<br /><br /> **建议的搜索 （复选框）**|背景|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索选项的悬停](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303年 130_SearchOptionsHover")<br /><br /> **搜索选项**|背景|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![悬停时的搜索复选框](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303年 129_SearchCheckboxHover")<br /><br /> **建议的搜索 （复选框）**|前景（复选框文本）|`SearchControl.PopupCheckboxMouseDownText`|  
|![搜索选项的悬停](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303年 130_SearchOptionsHover")<br /><br /> **搜索选项**|前景（复选框文本）|`SearchControl.PopupCheckboxMouseDownText`|  
|![悬停时的搜索复选框](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303年 129_SearchCheckboxHover")<br /><br /> **建议的搜索 （复选框）**|前景（链接文本）|`SearchControl.PopupButtonMouseDownText`|  
|![搜索选项的悬停](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303年 130_SearchOptionsHover")<br /><br /> **搜索选项**|前景（链接文本）|`SearchControl.PopupButtonMouseDownText`|  
|![悬停时的搜索复选框](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303年 129_SearchCheckboxHover")<br /><br /> **建议的搜索 （复选框）**|Border|`SearchControl.PopupControlMouseOverBorder`|  
|![搜索选项的悬停](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303年 130_SearchOptionsHover")<br /><br /> **搜索选项**|Border|`SearchControl.PopupControlMouseOverBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下的搜索建议](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303年 131_SearchSuggestedPressed")<br /><br /> **建议的搜索 （复选框）**|复选框背景|`SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索按下的选项](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303年 132_SearchOptionsPressed")<br /><br /> **搜索选项**|复选框背景|`SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![按下的搜索建议](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303年 131_SearchSuggestedPressed")<br /><br /> **建议的搜索 （复选框）**|复选框背景|`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索按下的选项](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303年 132_SearchOptionsPressed")<br /><br /> **搜索选项**|复选框背景|`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![按下的搜索建议](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303年 131_SearchSuggestedPressed")<br /><br /> **建议的搜索 （复选框）**|前景（复选框文本）|`SearchControl.PopupCheckboxMouseDownText`|  
|![搜索按下的选项](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303年 132_SearchOptionsPressed")<br /><br /> **搜索选项**|前景（复选框文本）|`SearchControl.PopupCheckboxMouseDownText`|  
|![按下的搜索建议](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303年 131_SearchSuggestedPressed")<br /><br /> **建议的搜索 （复选框）**|链接背景|`SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![搜索按下的选项](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303年 132_SearchOptionsPressed")<br /><br /> **搜索选项**|链接背景|`SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br /><br /> 未在现代主题 UI 中使用时，此背景具有梯度停止点和值。|  
|![按下的搜索建议](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303年 131_SearchSuggestedPressed")<br /><br /> **建议的搜索 （复选框）**|前景（链接文本）|`SearchControl.PopupButtonMouseDownText`|  
|![搜索按下的选项](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303年 132_SearchOptionsPressed")<br /><br /> **搜索选项**|前景（链接文本）|`SearchControl.PopupButtonMouseDownText`|  
  
#### <a name="hyperlink"></a>超链接  
 超链接是一个没有前景/背景对的控件。 在所有情况下，都使用超链接前景色，它可在黑色、灰色和白色背景上正确显示。 如果不使用超链接控件的颜色标记，则会看到用于“已按下”的默认系统颜色（以红色闪烁）。 这是控件未使用正确环境颜色标记的信号。  
  
 ![超链接红线](../extensibility/ux-guidelines/media/0303-133-hyperlinkredline.png "0303年 133_HyperlinkRedline")  
  
 使用...  
 当需要创建自定义超链接时。  
  
 请勿使用...  
 对于不是超链接的任何内容。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![超链接默认值](../extensibility/ux-guidelines/media/0303-134-hyperlink.png "0303年 134_Hyperlink")|前景（文本）|`Environment.PanelHyperlink`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的超链接](../extensibility/ux-guidelines/media/0303-135-hyperlinkhover.png "0303年 135_HyperlinkHover")|前景（文本）|`Environment.PanelHyperlinkHover`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下的超链接](../extensibility/ux-guidelines/media/0303-136-hyperlinkpressed.png "0303年 136_HyperlinkPressed")|前景（文本）|`Environment.PanelHyperlinkPressed`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![禁用的超链接](../extensibility/ux-guidelines/media/0303-137-hyperlinkdisabled.png "0303年 137_HyperlinkDisabled")|前景（文本）|`Environment.PanelHyperlinkDisabled`|  
  
#### <a name="infobar"></a>信息栏  
 信息栏用于提供有关给定上下文的详细信息，始终出现在文档窗口或工具窗口顶部。  
  
 ![信息栏红线](../extensibility/ux-guidelines/media/0303-138-infobarredline.png "0303年 138_InfobarRedline")  
  
 使用...  
 当创建自定义信息栏时。  
  
 请勿使用...  
 对于与信息栏不相似的 UI 元素。  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Infobar](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **Infobar**|背景|`Environment.InfoBackground`|  
|![Infobar](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **Infobar**|前景（文本）|`Environment.InfoText`|  
|![Infobar](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **Infobar**|Border|`Environment.ToolWindowBorder`|  
  
#### <a name="scroll-bar"></a>滚动条  
 滚动条由 Visual Studio 环境设置样式，无需具有主题。 但是，你可能决定你想要利用滚动条中使用，因此，UI 显示方式始终与这部分 Visual Studio 环境一致的颜色。  
  
 ![滚动条红线](../extensibility/ux-guidelines/media/0303-140-scrollbarredline.png "0303年 140_ScrollbarRedline")  
  
 使用...  
 当创建要与 Visual Studio 滚动条匹配的 UI 时。  
  
 请勿使用...  
 对于并非希望始终与滚动条 UI 匹配的任何内容。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![滚动条](../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303年 141_Scrollbar")<br /><br /> **Scrollbar**|Scrollbar|`Environment.ScrollBarBackground`|  
|![滚动条](../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303年 141_Scrollbar")<br /><br /> **Scrollbar**|前景（缩略）|`Environment.ScrollBarThumbBackground`|  
|![滚动条箭头](../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303年 142_ScrollbarArrow")<br /><br /> **滚动箭头**|背景|`Environment.ScrollBarArrowBackground`<br /><br /> 设置为与滚动条相同的颜色。|  
|![滚动条箭头](../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303年 142_ScrollbarArrow")<br /><br /> **滚动箭头**|前景（标志符号）|`Environment.ScrollBarArrowGlyph`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的滚动条](../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303年 143_ScrollbarHover")<br /><br /> **Scrollbar**|Scrollbar|`Environment.ScrollBarBackground`|  
|![悬停时的滚动条](../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303年 143_ScrollbarHover")<br /><br /> **Scrollbar**|前景（缩略）|`Environment.ScrollBarThumbMouseOverBackground`|  
|![滚动条箭头上悬停](../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303年 144_ScrollbarArrowHover")<br /><br /> **滚动箭头**|背景|`Environment.ScrollBarArrowMouseOverBackground`<br /><br /> 设置为与滚动条相同的颜色。|  
|![滚动条箭头上悬停](../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303年 144_ScrollbarArrowHover")<br /><br /> **滚动箭头**|前景（标志符号）|`Environment.ScrollBarArrowGlyphMouseOver`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下的滚动条](../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303年 145_ScrollbarPressed")<br /><br /> **Scrollbar**|Scrollbar|`Environment.ScrollBarBackground`|  
|![按下的滚动条](../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303年 145_ScrollbarPressed")<br /><br /> **Scrollbar**|前景（缩略）|`Environment.ScrollBarThumbPressedBackground`|  
|![滚动条箭头按下](../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303年 146_ScrollbarArrowPressed")<br /><br /> **滚动箭头**|背景|`Environment.ScrollBarArrowPressedBackground`<br /><br /> 设置为与滚动条相同的颜色。|  
|![滚动条箭头按下](../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303年 146_ScrollbarArrowPressed")<br /><br /> **滚动箭头**|前景（标志符号）|`Environment.ScrollBarArrowGlyphPressed`|  
  
#### <a name="BKMK_TreeView"></a> 树视图  
 多个工具窗口（包括解决方案资源管理器、服务器资源管理器和类视图）可实现其颜色由树视图类别中的颜色名称控制的分层组织方案。 树视图中的所有项都具有背景和文本颜色。 具有嵌套子元素的项还具有指示该项是展开还是折叠的标志符号。  
  
 ![树视图红线](../extensibility/ux-guidelines/media/0303-147-treeviewredline.png "0303年 147_TreeViewRedline")  
  
 使用...  
 需要在其中实现分层组织视图的任何位置。  
  
请勿使用...  
- 对于不类似于树视图的任何内容。  

- 在指定组合之外的任何背景/前景组合中。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![树视图](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303年 148_TreeView")|背景|`TreeView.Background`|  
|![树视图](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303年 148_TreeView")|前景（文本）|`TreeView.Background`|  
|![树视图](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303年 148_TreeView")|前景（标志符号）|`TreeView.Glyph`|  
|![树视图](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303年 148_TreeView")|Border|None|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![树视图的悬停](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303年 149_TreeViewHover")|背景|`TreeView.Background`|  
|![树视图的悬停](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303年 149_TreeViewHover")|前景（文本）|`TreeView.Background`|  
|![树视图的悬停](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303年 149_TreeViewHover")|前景（标志符号）|`TreeView.GlyphMouseOver`|  
|![树视图的悬停](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303年 149_TreeViewHover")|Border|None|  
  
 **拖动**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![树视图拖动](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303年 150_TreeViewDragOver")|背景|`TreeView.DragOverItem`|  
|![树视图拖动](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303年 150_TreeViewDragOver")|前景（文本）|`TreeView.DragOverItem`|  
|![树视图拖动](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303年 150_TreeViewDragOver")|前景（标志符号）|`TreeView.DragOverItemGlyph`|  
|![树视图拖动](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303年 150_TreeViewDragOver")|Border|None|  
  
 **选择**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![树视图已设定焦点](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303年 151_TreeViewFocused")<br /><br /> **已设定焦点**|背景|`TreeView.SelectedItemActive`|  
|![树视图已设定焦点](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303年 151_TreeViewFocused")<br /><br /> **已设定焦点**|前景（文本）|`TreeView.SelectedItemActive`|  
|![树视图已设定焦点](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303年 151_TreeViewFocused")<br /><br /> **已设定焦点**|前景（标志符号）|`TreeView.SelectedItemActiveGlyph`|  
|![树视图已设定焦点](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303年 151_TreeViewFocused")<br /><br /> **已设定焦点**|Border|`TreeView.FocusVisualBorder`|  
|![树视图已失去焦点](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303年 152_TreeViewUnfocused")<br /><br /> **失去焦点**|背景|`TreeView.SelectedItemInactive`|  
|![树视图已失去焦点](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303年 152_TreeViewUnfocused")<br /><br /> **失去焦点**|前景（文本）|`TreeView.SelectedItemInactive`|  
|![树视图已失去焦点](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303年 152_TreeViewUnfocused")<br /><br /> **失去焦点**|前景（标志符号）|`TreeView.SelectedItemInactiveGlyph`|  
|![树视图已失去焦点](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303年 152_TreeViewUnfocused")<br /><br /> **失去焦点**|Border|None|  
  
 **悬停在选定内容**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![树视图侧重于悬停](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303年 153_TreeViewFocusedHover")<br /><br /> **已设定焦点**|背景|`TreeView.SelectedItemActive`|  
|![树视图侧重于悬停](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303年 153_TreeViewFocusedHover")<br /><br /> **已设定焦点**|前景（文本）|`TreeView.SelectedItemActive`|  
|![树视图侧重于悬停](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303年 153_TreeViewFocusedHover")<br /><br /> **已设定焦点**|前景（标志符号）|`TreeView.SelectedItemActiveGlyphMouseOver`|  
|![树视图侧重于悬停](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303年 153_TreeViewFocusedHover")<br /><br /> **已设定焦点**|Border|无`TreeView.FocusVisualBorder`|  
|![树视图失去焦点的悬停](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303年 154_TreeViewUnfocusedHover")<br /><br /> **失去焦点**|背景|`TreeView.SelectedItemInactive`|  
|![树视图失去焦点的悬停](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303年 154_TreeViewUnfocusedHover")<br /><br /> **失去焦点**|前景（文本）|`TreeView.SelectedItemInactive`|  
|![树视图失去焦点的悬停](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303年 154_TreeViewUnfocusedHover")<br /><br /> **失去焦点**|前景（标志符号）|`TreeView.SelectedItemActiveGlyphMouseOver`|  
|![树视图失去焦点的悬停](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303年 154_TreeViewUnfocusedHover")<br /><br /> **失去焦点**|Border|None|  
  
#### <a name="button-controls"></a>按钮控件  
 ![按钮控件红线](../extensibility/ux-guidelines/media/0303-155-buttoncontrolredline.png "0303年 155_ButtonControlRedline")  
  
 使用...  
 对于要与 Visual Studio 主题（浅色、深色、蓝色或系统高对比度主题）集成的文档井中的按钮。  
  
 请勿使用...  
 对于将针对不属于 Visual Studio 主题一部分的自定义背景显示的按钮。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Button](../extensibility/ux-guidelines/media/0303-156-button.png "0303-156_Button")|Button|`CommonControls.Button`|  
|![Button](../extensibility/ux-guidelines/media/0303-156-button.png "0303-156_Button")|按钮边框|`CommonControls.ButtonBorder`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按钮已禁用](../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303年 157_ButtonDisabled")|Button|`CommonControls.ButtonDisabled`|  
|![按钮已禁用](../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303年 157_ButtonDisabled")|按钮边框|`CommonControls.ButtonBorderDisabled`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的按钮](../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303年 158_ButtonHover")|Button|`CommonControls.ButtonHover`|  
|![悬停时的按钮](../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303年 158_ButtonHover")|按钮边框|`CommonControls.ButtonBorderHover`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下按钮](../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303年 159_ButtonPressed")|Button|`CommonControls.ButtonPressed`|  
|![按下按钮](../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303年 159_ButtonPressed")|按钮边框|`CommonControls.ButtonBorderPressed`|  
  
 **已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的按钮](../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303年 160_ButtonFocused")|Button|`CommonControls.ButtonFocused`|  
|![已设定焦点的按钮](../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303年 160_ButtonFocused")|按钮边框|`CommonControls.ButtonBorderFocused`|  
  
#### <a name="check-box-controls"></a>复选框控件  
 ![复选框红线](../extensibility/ux-guidelines/media/0303-161-checkboxredline.png "0303年 161_CheckboxRedline")  
  
 使用...  
 对于文档井中包含的复选框控件。  
  
 请勿使用...  
 对于不是复选框控件的任何 UI。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Check box](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|背景|`CommonControls.CheckBoxBackground`|  
|![Check box](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Border|`CommonControls.CheckBoxBorder`|  
|![Check box](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Text|`CommonControls.CheckBoxText`|  
|![Check box](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|标志符号|`CommonControls.CheckBoxGlyph`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![禁用的复选框](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303年 163_CheckboxDisabled")|背景|`CommonControls.CheckBoxBackgroundDisabled`|  
|![禁用的复选框](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303年 163_CheckboxDisabled")|Border|`CommonControls.CheckBoxBorderDisabled`|  
|![禁用的复选框](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303年 163_CheckboxDisabled")|Text|`CommonControls.CheckBoxTextDisabled`|  
|![禁用的复选框](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303年 163_CheckboxDisabled")|标志符号|`CommonControls.CheckBoxGlyphDisabled`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的复选框](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303年 164_CheckboxHover")|背景|`CommonControls.CheckBoxBackgroundHover`|  
|![悬停时的复选框](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303年 164_CheckboxHover")|Border|`CommonControls.CheckBoxBorderHover`|  
|![悬停时的复选框](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303年 164_CheckboxHover")|Text|`CommonControls.CheckBoxTextHover`|  
|![悬停时的复选框](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303年 164_CheckboxHover")|标志符号|`CommonControls.CheckBoxGlyphHover`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![按下的复选框](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303年 165_CheckboxPressed")|背景|`CommonControls.CheckBoxBackgroundPressed`|  
|![按下的复选框](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303年 165_CheckboxPressed")|Border|`CommonControls.CheckBoxBorderPressed`|  
|![按下的复选框](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303年 165_CheckboxPressed")|Text|`CommonControls.CheckBoxTextPressed`|  
|![按下的复选框](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303年 165_CheckboxPressed")|标志符号|`CommonControls.CheckBoxGlyphPressed`|  
  
 **已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的复选框](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303年 166_CheckboxFocused")|背景|`CommonControls.CheckBoxBackgroundFocused`|  
|![已设定焦点的复选框](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303年 166_CheckboxFocused")|Border|`CommonControls.CheckBoxBorderFocused`|  
|![已设定焦点的复选框](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303年 166_CheckboxFocused")|Text|`CommonControls.CheckBoxTextFocused`|  
|![已设定焦点的复选框](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303年 166_CheckboxFocused")|标志符号|`CommonControls.CheckBoxGlyphFocused`|  
  
#### <a name="drop-boxcombo-box-controls"></a>下拉框/组合框控件  
 ![删除&#45;关闭&#47;组合框红线](../extensibility/ux-guidelines/media/0303-167-dropdowncomboboxredline.png "0303年 167_DropDownComboBoxRedline")  
  
使用...  
对于属于文档井一部分的下拉框和组合框。  

请勿使用...  
- 对于不是下拉框或组合框的任何 UI。  

- 对于命令栏中的 [Drop-down](../misc/shared-colors.md#BKMK_CommandDropDown) 或 [Combo box](../misc/shared-colors.md#BKMK_CommandComboBox) 。  
  
  **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Drop&#45;down&#47;combo box](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|背景|`CommonControls.ComboBoxBackground`|  
|![Drop&#45;down&#47;combo box](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Border|`CommonControls.ComboBoxBorder`|  
|![Drop&#45;down&#47;combo box](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Text|`CommonControls.ComboBoxText`|  
|![Drop&#45;down&#47;combo box](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Separator|`CommonControls.ComboBoxSeparator`|  
|![Drop&#45;down&#47;combo box](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|标志符号|`CommonControls.ComboBoxGlyph`|  
|![Drop&#45;down&#47;combo box](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|标志符号背景|`CommonControls.ComboBoxGlyphBackground`|  
  
 已禁用  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;关闭&#47;组合框禁用](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303年 169_DropDownComboBoxDisabled")|背景|`CommonControls.ComboBoxBackgroundDisabled`|  
|![删除&#45;关闭&#47;组合框禁用](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303年 169_DropDownComboBoxDisabled")|Border|`CommonControls.ComboBoxBorderDisabled`|  
|![删除&#45;关闭&#47;组合框禁用](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303年 169_DropDownComboBoxDisabled")|Text|`CommonControls.ComboBoxTextDisabled`|  
|![删除&#45;关闭&#47;组合框禁用](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303年 169_DropDownComboBoxDisabled")|Separator|`CommonControls.ComboBoxSeparatorDisabled`|  
|![删除&#45;关闭&#47;组合框禁用](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303年 169_DropDownComboBoxDisabled")|标志符号|`CommonControls.ComboBoxGlyphDisabled`|  
|![删除&#45;关闭&#47;组合框禁用](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303年 169_DropDownComboBoxDisabled")|标志符号背景|`CommonControls.ComboBoxGlyphBackgroundDisabled`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;关闭&#47;组合框上悬停](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")|背景|`CommonControls.ComboBoxBackgroundHover`|  
|![删除&#45;关闭&#47;组合框上悬停](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")|Border|`CommonControls.ComboBoxBorderHover`|  
|![删除&#45;关闭&#47;组合框上悬停](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")|Text|`CommonControls.ComboBoxTextHover`|  
|![删除&#45;关闭&#47;组合框上悬停](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")|Separator|`CommonControls.ComboBoxSeparatorHover`|  
|![删除&#45;关闭&#47;组合框上悬停](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")|标志符号|`CommonControls.ComboBoxGlyphHover`|  
|![删除&#45;关闭&#47;组合框上悬停](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303年 170_DropDownComboBoxHover")|标志符号背景|`CommonControls.ComboBoxGlyphBackgroundHover`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;关闭&#47;按下的组合框](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303年 171_DropDownComboBoxPressed")|背景|`CommonControls.ComboBoxBackgroundPressed`|  
|![删除&#45;关闭&#47;按下的组合框](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303年 171_DropDownComboBoxPressed")|Border|`CommonControls.ComboBoxBorderPressed`|  
|![删除&#45;关闭&#47;按下的组合框](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303年 171_DropDownComboBoxPressed")|Text|`CommonControls.ComboBoxTextPressed`|  
|![删除&#45;关闭&#47;按下的组合框](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303年 171_DropDownComboBoxPressed")|Separator|`CommonControls.ComboBoxSeparatorPressed`|  
|![删除&#45;关闭&#47;按下的组合框](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303年 171_DropDownComboBoxPressed")|标志符号|`CommonControls.ComboBoxGlyphPressed`|  
|![删除&#45;关闭&#47;按下的组合框](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303年 171_DropDownComboBoxPressed")|标志符号背景|`CommonControls.ComboBoxGlyphBackgroundPressed`|  
  
 **已设定焦点**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;关闭&#47;已设定焦点的组合框](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")|背景|`CommonControls.ComboBoxBackgroundFocused`|  
|![删除&#45;关闭&#47;已设定焦点的组合框](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")|Border|`CommonControls.ComboBoxBorderFocused`|  
|![删除&#45;关闭&#47;已设定焦点的组合框](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")|Text|`CommonControls.ComboBoxTextFocused`|  
|![删除&#45;关闭&#47;已设定焦点的组合框](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")|Separator|`CommonControls.ComboBoxSeparatorFocused`|  
|![删除&#45;关闭&#47;已设定焦点的组合框](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")|标志符号|`CommonControls.ComboBoxGlyphFocused`|  
|![删除&#45;关闭&#47;已设定焦点的组合框](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303年 172_DropDownComboBoxFocused")|标志符号背景|`CommonControls.ComboBoxGlyphBackgroundFocused`|  
  
 **文本输入的选择**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![删除&#45;关闭&#47;组合框文本输入](../extensibility/ux-guidelines/media/0303-173-dropdowncomboboxtextinput.png "0303年 173_DropDownComboBoxTextInput")|突出显示|`CommonControls.ComboBoxTextInputSelection`|  
  
 **已按下 – 列表项视图**  
  
|组件|元素|令牌名称：Color.category|  
|---------------|-------------|--------------------------------|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListBackground`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListBackgroundHover`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListItemBackgroundPressed`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListItemBackgroundFocused`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|Border|`CommonControls.ComboBoxListBorder`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|Border|`CommonControls.ComboBoxListBorderHover`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|Border|`CommonControls.ComboBoxListBorderPressed`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|Border|`CommonControls.ComboBoxListBorderFocused`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|项文本|`CommonControls.ComboBoxListItemText`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|项文本|`CommonControls.ComboBoxListItemTextHover`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|项文本|`CommonControls.ComboBoxListItemTextPressed`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|项文本|`CommonControls.ComboBoxListItemTextFocused`|  
|![删除&#45;关闭&#47;组合框列表视图](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303年 174_DropDownComboBoxListView")|背景阴影|`CommonControls.ComboBoxListBackgroundShadow`|  
  
#### <a name="tabular-data-grid-controls"></a>表格数据（网格）控件  
 表格数据控件（也称为网格控件）是可以用于在多列中呈现大量数据的 Visual Studio 公共控件。 可以在 Visual Studio 中的多个位置中找到标准表格数据控件：错误列表工具窗口、IntelliTrace 报告和内存堆视图及其他位置。 始终使用提供的标准表格数据控件。 在某些极少数情况下，你可能无法访问标准表格数据控件。 在这些情况下，请使用以下标记名称以确保 UI 与 Visual Studio 中的其他表格数据控件保持一致。  
  
 ![表格数据&#40;网格控件&#41;红线](../extensibility/ux-guidelines/media/0303-197-tabulardatagridcontrolredline.png "0303年 197_TabularDataGridControlRedline")  
  
 使用...  
 对于表格或网格控件。  
  
 请勿使用...  
 对于不是表格或网格控件的任何 UI。  
  
##### <a name="column-headers"></a>列标题  
 列标题由背景、边框、标题文本和可选标志符号（通常在网格按该列进行排序时使用）组成。  
  
|状态|元素|令牌名称：Category.color|  
|-----------|-------------|--------------------------------|  
|默认|背景|`Header.Default`|  
|默认|前景（文本）|`Environment.CommandBarTextActive`|  
|默认|前景（标志符号）|`Header.Glyph`|  
|默认|Border|`Header.SeparatorLine`|  
|悬停|背景|`Header.MouseOver`|  
|悬停|前景（文本）|`Environment.CommandBarTextHover`|  
|悬停|前景（标志符号）|`Header.MouseOverGlyph`|  
|悬停|Border|`Header.SeparatorLine`|  
|已按下|背景|`CommonControls.CheckBoxBackgroundPressed`|  
|已按下|前景（文本）|`CommonControls.CheckBoxBorderPressed`|  
|已按下|前景（标志符号）|`CommonControls.CheckBoxTextPressed`|  
|已按下|Border|`CommonControls.CheckBoxGlyphPressed`|  
  
##### <a name="list-view-items"></a>列表视图项  
 列表视图项由背景和内容组成。 内容可以是文本、图标或两者。  
  
|状态|元素|令牌名称：Category.color|  
|-----------|-------------|--------------------------------|  
|默认|背景|透明|  
|默认|前景（文本）|`Environment.CommandBarTextActive`|  
|默认|Border|None|  
|已选定（活动）|背景|`TreeView.SelectedItemActive`|  
|已选定（活动）|前景（文本）|`TreeView.SelectedItemActiveText`|  
|已选定（活动）|Border|None|  
|已选定（非活动）|背景|`TreeView.SelectedItemInactive`|  
|已选定（非活动）|前景（文本）|`TreeView.SelectedItemInactiveText`|  
|已选定（非活动）|Border|None|  
  
### <a name="manifest-designer"></a>清单设计器  
 清单设计器旨在作为可用于更加轻松地在 Windows 8 和 Windows Phone 8 项目中编辑清单文件的方法。 虽然没有可供使用的共享框架，不过匹配方向/导航选项卡和整体结构的设计布局和颜色是合适的。 有关布局详细信息的更多信息，请参见 [Layout for Visual Studio](../extensibility/ux-guidelines/layout-for-visual-studio.md)。  
  
 ![清单设计器红线](../extensibility/ux-guidelines/media/0303-175-manifestdesignerredline.png "0303年 175_ManifestDesignerRedline")  
  
使用...  
- 对于类似于清单设计器的设计器。  

- 在文档井中编辑器的顶部代替使用公共选项卡控件。  

请勿使用...  
- 如果你有六个以上的选项卡。  

- 对于结构不类似于清单设计器中的任何 UI。  
  
|状态|组件|元素|令牌名称：Category.color|  
|-----------|---------------|-------------|--------------------------------|  
|默认值（已选定）|Tab|背景|`ManifestDesigner.TabActive`|  
|默认值（已选定）|Tab|Border|None|  
|默认值（已选定）|说明窗格|背景|`ManifestDesigner.DescriptionPane`|  
|默认值（已选定）|内容页|背景|`ManifestDesigner.Background`|  
|默认值（已选定）|内容页|对话框帮助程序文本|`ManifestDesigner.WatermarkText`<br /><br /> 此标记名称与其功能不匹配。|  
|未选定|Tab|背景|`ManifestDesigner.Tab.Inactive`|  
|悬停|Tab|背景|`ManifestDesigner.Tab.Mouseover`|  
  
### <a name="tagging"></a>标记  
 Visual Studio 支持标记，这使用户可以声明可搜索的关键字以用于跟踪。 例如，项目经理和开发人员可以使用 Team Foundation Server (TFS) 对工作项进行标记。 下表为标记本身以及在悬停和已选定状态下出现的“关闭图标”标志符号提供颜色名称。  
  
 ![标记红线](../extensibility/ux-guidelines/media/0303-176-taggingredline.png "0303年 176_TaggingRedline")  
  
 使用...  
 支持标记的 UI。  
  
 请勿使用...  
 对于任何其他类型的 UI。  
  
#### <a name="tag"></a>标记  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Tag](../extensibility/ux-guidelines/media/0303-177-tag.png "0303-177_Tag")<br /><br /> **默认**|背景|`Tag.Background`|  
|![Tag](../extensibility/ux-guidelines/media/0303-177-tag.png "0303-177_Tag")<br /><br /> **默认**|前景（文本）|`Tag.Background`|  
|![悬停时的标记](../extensibility/ux-guidelines/media/0303-178-taghover.png "0303年 178_TagHover")<br /><br /> **Hover**|背景|`Tag.HoverBackground`|  
|![悬停时的标记](../extensibility/ux-guidelines/media/0303-178-taghover.png "0303年 178_TagHover")<br /><br /> **Hover**|前景（文本）|`Tag.HoverBackgroundText`|  
|![按下的标记](../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303年 179_TagPressed")<br /><br /> **按下**|背景|`Tag.PressedBackground`|  
|![按下的标记](../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303年 179_TagPressed")<br /><br /> **按下**|前景（文本）|`Tag.PressedBackgroundText`|  
|![已选定标记](../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303年 180_TagSelected")<br /><br /> **选择**|背景|`Tag.SelectedBackground`|  
|![已选定标记](../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303年 180_TagSelected")<br /><br /> **选择**|前景（文本）|`Tag.SelectedBackgroundText`|  
  
#### <a name="glyph-close-icon"></a>标志符号（关闭图标）  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![Tag &#40;glyph&#41;](../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303-181_TagGlyph")<br /><br /> **默认值 （标记默认值）**|背景|不适用|  
|![Tag &#40;glyph&#41;](../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303-181_TagGlyph")<br /><br /> **默认值 （标记默认值）**|前景（标志符号）|`Tag.TagHoverGlyph`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![标记&#40;标志符号&#41;上悬停](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303年 182_TagGlyphHover")<br /><br /> **悬停 （标记默认值）**|背景|`Tag.TagHoverGlyphHoverBackground`|  
|![标记&#40;标志符号&#41;上悬停](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303年 182_TagGlyphHover")<br /><br /> **悬停 （标记默认值）**|前景（标志符号）|`Tag.TagHoverGlyphHover`|  
|![标记&#40;标志符号&#41;上悬停](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303年 182_TagGlyphHover")<br /><br /> **悬停 （标记默认值）**|Border|`Tag.TagHoverGlyphHoverBorder`|  
  
 **按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![标记&#40;标志符号&#41;按下](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303年 183_TagGlyphPressed")<br /><br /> **按下 （标记默认值）**|背景|`Tag.TagHoverGlyphPressedBackground`|  
|![标记&#40;标志符号&#41;按下](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303年 183_TagGlyphPressed")<br /><br /> **按下 （标记默认值）**|前景（标志符号）|`Tag.TagHoverGlyphPressed`|  
|![标记&#40;标志符号&#41;按下](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303年 183_TagGlyphPressed")<br /><br /> **按下 （标记默认值）**|Border|`Tag.TagHoverGlyphPressedBorder`|  
  
 **标记标志符号所选/默认值**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已选定标记](../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303年 184_TagSelected")<br /><br /> **默认值 （已选定标记）**|背景|不适用|  
|![已选定标记](../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303年 184_TagSelected")<br /><br /> **默认值 （已选定标记）**|前景（标志符号）|`Tag.TagSelectedGlyph`|  
  
 **标记选择/悬停标志符号**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的已选定标记](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303年 185_TagSelectedHover")<br /><br /> **悬停 （已选定标记）**|背景|`Tag.TagSelectedGlyphHoverBackground`|  
|![悬停时的已选定标记](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303年 185_TagSelectedHover")<br /><br /> **悬停 （已选定标记）**|前景（标志符号）|`Tag.TagSelectedGlyphHover`|  
|![悬停时的已选定标记](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303年 185_TagSelectedHover")<br /><br /> **悬停 （已选定标记）**|Border|`Tag.TagSelectedGlyphHoverBorder`|  
  
 **标记选择/标志符号按下**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已选定标记按下](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303年 186_TagSelectedPressed")<br /><br /> **按下 （已选定标记）**|背景|`Tag.TagSelectedGlyphPressedBackground`|  
|![已选定标记按下](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303年 186_TagSelectedPressed")<br /><br /> **按下 （已选定标记）**|前景（标志符号）|`Tag.TagSelectedGlyphPressed`|  
|![已选定标记按下](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303年 186_TagSelectedPressed")<br /><br /> **按下 （已选定标记）**|Border|`Tag.TagSelectedGlyphPressedBorder`|  
  
### <a name="shell"></a>shell  
  
#### <a name="background"></a>背景  
 环境背景由两层组成。 下层是覆盖整个 IDE 的纯色。 上层位于命令架下，以及 IDE 左边缘和右边缘上的工具窗口自动隐藏通道之间。 从 Visual Studio 2013 开始，背景上层和下层在浅色和深色主题中设置为相同颜色。  
  
 ![外壳背景红线](../extensibility/ux-guidelines/media/0303-187-shellbackgroundredline.png "0303年 187_ShellBackgroundRedline")  
  
 使用...  
 对于要在其中与 Visual Studio 环境背景匹配的位置。  
  
请勿使用...  
- 作为不是背景图面的位置的填充。  

- 作为要在其上放置前景元素的背景。  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|下层|背景|`Environment.EnvironmentBackground`|  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|上层|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.EnvironmentBackgroundGradientBegin`|  
|上层|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.EnvironmentBackgroundGradientEnd`|  
|上层|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.EnvironmentBackgroundGradientMiddle1`|  
|上层|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.EnvironmentBackgroundGradientMiddle2`|  
  
#### <a name="command-shelf"></a>命令架  
 有两组标记名称用于命令架背景：一组用于菜单栏所在的位置，另一组用于命令栏所在的位置。 单个命令栏组具有自己的背景色值（在“命令栏”部分中进行更详细的讨论）。 菜单栏和命令栏文本分别在菜单和命令栏部分中进行了讨论。  
  
 ![命令架红线](../extensibility/ux-guidelines/media/0303-188-commandshelfredline.png "0303年 188_CommandShelfRedline")  
  
使用...  
- 用于在其中放置菜单或工具栏的区域。  

- 具有正确的背景 / 前景标记名称组合。  
  
  请勿使用...  
  对于与命令架不相似的区域。  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|菜单栏|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.CommandShelfHighlightGradientBegin`|  
|菜单栏|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.CommandShelfHighlightGradientMiddle`|  
|菜单栏|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.CommandShelfHighlightGradientEnd`|  
|命令栏|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.CommandShelfBackgroundGradientBegin`|  
|命令栏|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.CommandShelfBackgroundGradientMiddle`|  
|命令栏|背景<br /><br /> *梯度停止点设置为 Visual Studio 2013 浅色和深色主题中的相同颜色值。*|`Environment.CommandShelfBackgroundGradientEnd`|  
  
### <a name="toolbox"></a>工具箱  
 工具箱是 Visual Studio 中最常使用的公共工具窗口之一。 它实质上是应用了特殊主题和样式的树控件。  
  
 ![工具箱红线](../extensibility/ux-guidelines/media/0303-189-toolboxredline.png "0303年 189_ToolboxRedline")  
  
 使用...  
 在设计希望始终与 shell 工具箱保持一致的工具窗口时。  
  
 请勿使用...  
 对于不类似于工具箱 UI 的任何内容，或者如果不确定 UI 在 shell 工具箱颜色更改中是否会出现问题。  
  
 **默认**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![工具箱父节点](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303年 190_ToolboxParentNode")<br /><br /> **父节点**|背景|`Environment.ToolboxContent`<br /><br /> 标题<br /><br /> `Environment.ToolWindowBackground`<br /><br /> 各个项或整个窗口（如果没有可用控件）|  
|![工具箱子节点](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303年 191_ToolboxChildNode")<br /><br /> **子节点**|背景|`Environment.ToolboxContent`<br /><br /> 标题<br /><br /> `Environment.ToolWindowBackground`<br /><br /> 各个项或整个窗口（如果没有可用控件）|  
|![工具箱父节点](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303年 190_ToolboxParentNode")<br /><br /> **父节点**|Border|None|  
|![工具箱子节点](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303年 191_ToolboxChildNode")<br /><br /> **子节点**|Border|None|  
|![工具箱父节点](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303年 190_ToolboxParentNode")<br /><br /> **父节点**|前景（标志符号）|`Environment.ToolboxContent`|  
|![工具箱子节点](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303年 191_ToolboxChildNode")<br /><br /> **子节点**|前景（标志符号）|`Environment.ToolboxContent`|  
|![工具箱父节点](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303年 190_ToolboxParentNode")<br /><br /> **父节点**|前景（文本）|`Environment.ToolboxContent`|  
|![工具箱子节点](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303年 191_ToolboxChildNode")<br /><br /> **子节点**|前景（文本）|`Environment.ToolboxContent`|  
  
 **Hover**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![悬停时的工具箱子节点](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303年 192_ToolboxChildNodeHover")<br /><br /> **子节点上的工具箱悬停**|背景|`Environment.ToolboxContentMouseOver`<br /><br /> 仅限单个项|  
|![悬停时的工具箱子节点](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303年 192_ToolboxChildNodeHover")<br /><br /> **子节点上的工具箱悬停**|Border|None|  
|![悬停时的工具箱子节点](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303年 192_ToolboxChildNodeHover")<br /><br /> **子节点上的工具箱悬停**|前景（文本）|`Environment.ToolboxContentMouseOver`<br /><br /> 仅限单个项|  
  
 **选择**  
  
|组件|元素|令牌名称：Category.color|  
|---------------|-------------|--------------------------------|  
|![已设定焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303年 193_ToolboxParentNodeFocused")<br /><br /> **已设定焦点的父节点**|背景|`TreeView.SelectedItemActive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303年 194_ToolboxChildNodeFocused")<br /><br /> **已设定焦点的子节点**|背景|`TreeView.SelectedItemActive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303年 193_ToolboxParentNodeFocused")<br /><br /> **已设定焦点的父节点**|Border|`TreeView.FocusVisualBorder`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303年 194_ToolboxChildNodeFocused")<br /><br /> **已设定焦点的子节点**|Border|`TreeView.FocusVisualBorder`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303年 193_ToolboxParentNodeFocused")<br /><br /> **已设定焦点的父节点**|前景（标志符号）|`TreeView.SelectedItemActive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303年 194_ToolboxChildNodeFocused")<br /><br /> **已设定焦点的子节点**|前景（标志符号）|`TreeView.SelectedItemActive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303年 193_ToolboxParentNodeFocused")<br /><br /> **已设定焦点的父节点**|前景（文本）|`TreeView.SelectedItemActive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![已设定焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303年 194_ToolboxChildNodeFocused")<br /><br /> **已设定焦点的子节点**|前景（文本）|`TreeView.SelectedItemActive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![失去焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303年 195_ToolboxParentNodeUnfocused")<br /><br /> **失去焦点的父节点**|背景|`TreeView.SelectedItemInactive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![失去焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303年 196_ToolboxChildNodeUnfocused")<br /><br /> **失去焦点的子节点**|背景|`TreeView.SelectedItemInactive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![失去焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303年 195_ToolboxParentNodeUnfocused")<br /><br /> **失去焦点的父节点**|Border|None|  
|![失去焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303年 196_ToolboxChildNodeUnfocused")<br /><br /> **失去焦点的子节点**|Border|None|  
|![失去焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303年 195_ToolboxParentNodeUnfocused")<br /><br /> **失去焦点的父节点**|前景（标志符号）|`TreeView.SelectedItemInactive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![失去焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303年 196_ToolboxChildNodeUnfocused")<br /><br /> **失去焦点的子节点**|前景（标志符号）|`TreeView.SelectedItemInactive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![失去焦点的工具箱父节点](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303年 195_ToolboxParentNodeUnfocused")<br /><br /> **失去焦点的父节点**|前景（文本）|`TreeView.SelectedItemInactive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
|![失去焦点的工具箱子节点](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303年 196_ToolboxChildNodeUnfocused")<br /><br /> **失去焦点的子节点**|前景（文本）|`TreeView.SelectedItemInactive`<br /><br /> 来自 [Tree view](../misc/shared-colors.md#BKMK_TreeView) 类别|  
  
## <a name="color-value-reference"></a>颜色值参考  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|组件|部件|元素|状态|浅|深|蓝色|高对比度|  
|分隔线|||默认|FFEEEEF2|FF2D2D30|FFEEEEF2|ControlDark|  
|扩展器标志符号||Foreground|默认|||||  
|扩展器标志符号||Foreground|悬停|||||  
|扩展器标志符号||背景|默认|||||  
|扩展器标志符号||背景|悬停|||||  
|扩展器标志符号||Border|默认|||||  
|扩展器标志符号||Border|悬停|||||