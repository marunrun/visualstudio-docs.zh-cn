---
title: 创作..Vsct Files |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8f02c7ec0e453f0758ba2ab13145fcdff11b442a
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173598"
---
# <a name="author-vsct-files"></a>创作 .vsct 文件
本文档演示如何创作 *.vsct*文件，以便将菜单项、工具栏和其他用户界面（UI）元素添加到 Visual Studio 集成开发环境（IDE）。 将 UI 元素添加到尚不具有 *.vsct*文件的 Visual Studio 包（VSPackage）时，请使用以下步骤。

 对于新项目，建议使用 Visual Studio 包模板，因为它会生成一个 *.vsct*文件，该文件根据你的选择，已具有菜单命令、工具窗口或自定义编辑器所需的元素。 可以修改此 *.vsct*文件以满足 VSPackage 的要求。 有关如何修改 *.vsct*文件的详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)中的示例。

## <a name="author-the-file"></a>创作文件
 在以下阶段创作 *.vsct*文件：创建文件和资源的结构，声明 ui 元素，将 ui 元素放入 IDE，并添加任何专用行为。

### <a name="file-structure"></a>文件结构
 *.Vsct*文件的基本结构是一个[CommandTable](../../extensibility/commandtable-element.md)根元素，其中包含[命令](../../extensibility/commands-element.md)元素和[符号](../../extensibility/symbols-element.md)元素。

#### <a name="to-create-the-file-structure"></a>创建文件结构

1. 按照[如何：创建 .vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)中的步骤，将 *.vsct*文件添加到你的项目中。

2. 向元素添加所需的命名空间 `CommandTable` ，如以下示例中所示：

    ```xml
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"
        xmlns:xs="http://www.w3.org/2001/XMLSchema">

    ```

3. 在 `CommandTable` 元素中，添加一个 `Commands` 元素来承载所有自定义菜单、工具栏、命令组和命令。 为了能够加载自定义 UI 元素，该 `Commands` 元素必须 `Package` 将其特性设置为包的名称。

     在 `Commands` 元素之后，添加 `Symbols` 元素以定义包的 guid，并添加用户界面元素的名称和命令 id。

### <a name="include-visual-studio-resources"></a>包括 Visual Studio 资源
 使用[Extern](../../extensibility/extern-element.md)元素访问定义 Visual Studio 命令的文件，以及将 UI 元素放入 IDE 所需的菜单。 如果要使用在包外定义的命令，请使用[UsedCommands](../../extensibility/usedcommands-element.md)元素来通知 Visual Studio。

#### <a name="to-include-visual-studio-resources"></a>包括 Visual Studio 资源

1. 在元素顶部，为 `CommandTable` `Extern` 要引用的每个外部文件添加一个元素，并将 `href` 属性设置为该文件的名称。 可以引用以下头文件来访问 Visual Studio 资源：

   - *Stdidcmd*：定义 Visual Studio 公开的所有命令的 id。

   - *Vsshlids*：包含 Visual Studio 菜单的命令 id。

2. 如果你的包调用由 Visual Studio 或其他包定义的任何命令，请在 `UsedCommands` 元素后面添加元素 `Commands` 。 对于您调用的不属于包的每个命令，使用[UsedCommand](../../extensibility/usedcommand-element.md)元素填充此元素。 将 `guid` 元素的和 `id` 特性设置 `UsedCommand` 为要调用的命令的 GUID 和 ID 值。

   有关如何查找 Visual Studio 命令的 Guid 和 Id 的详细信息，请参阅[Visual studio 命令的 guid 和 id](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)。 若要从其他包调用命令，请使用这些包的 *.vsct*文件中定义的 GUID 和命令 ID。

### <a name="declare-ui-elements"></a>声明 UI 元素
 在 .vsct 文件的节中声明所有新的 UI 元素 `Symbols` 。 *.vsct*

#### <a name="to-declare-ui-elements"></a>声明 UI 元素

1. 在 `Symbols` 元素中，添加三个[GuidSymbol](../../extensibility/guidsymbol-element.md)元素。 每个 `GuidSymbol` 元素都有一个 `name` 属性和一个 `value` 属性。 设置 `name` 属性，使其反映元素的用途。 `value`属性采用 GUID。 （若要生成 GUID，请在 "**工具**" 菜单上选择 "**创建 guid**"，然后选择 "**注册表格式**"。）

     第一个 `GuidSymbol` 元素表示包，并且通常没有子级。 第二个 `GuidSymbol` 元素表示命令集，并将包含定义菜单、组和命令的所有符号。 第三个 `GuidSymbol` 元素表示映像存储，并包含命令的所有图标的符号。 如果你没有使用图标的命令，则可以省略第三个 `GuidSymbol` 元素。

2. 在 `GuidSymbol` 表示命令集的元素中，添加一个或多个[IDSymbol](../../extensibility/idsymbol-element.md)元素。 其中每个都表示要添加到 UI 的菜单、工具栏、组或命令。

     对于每个 `IDSymbol` 元素，请将 `name` 属性设置为将用于引用相应菜单、组或命令的名称，然后将元素设置 `value` 为将表示其命令 ID 的十六进制数。 `IDSymbol`具有相同父级的两个元素不能具有相同的值。

3. 如果任意 UI 元素需要图标，请将 `IDSymbol` 每个图标的元素添加到 `GuidSymbol` 表示映像存储的元素中。

### <a name="put-ui-elements-in-the-ide"></a>在 IDE 中放置 UI 元素
 [菜单](../../extensibility/menus-element.md)、[组](../../extensibility/groups-element.md)和[按钮](../../extensibility/buttons-element.md)元素包含包中定义的所有菜单、组和命令的定义。 将这些菜单、组和命令放置在 IDE 中，方法是使用[父](../../extensibility/parent-element.md)元素，该元素是 UI 元素定义的一部分，或使用在其他位置定义的[CommandPlacement](../../extensibility/commandplacement-element.md)元素。

 每个 `Menu` 、 `Group` 和 `Button` 元素都具有 `guid` 属性和 `id` 属性。 始终将 `guid` 属性设置为与 `GuidSymbol` 表示命令集的元素的名称匹配，并将 `id` 特性设置为元素的名称，该 `IDSymbol` 元素表示节中的菜单、组或命令 `Symbols` 。

#### <a name="to-define-ui-elements"></a>定义 UI 元素

1. 如果要定义任何新的菜单、子菜单、快捷菜单或工具栏，请将 `Menus` 元素添加到 `Commands` 元素。 然后，对于要创建的每个菜单，将[menu](../../extensibility/menu-element.md)元素添加到 `Menus` 元素。

    设置 `guid` 元素的和 `id` 属性 `Menu` ，然后将属性设置为所 `type` 需的菜单类型。 您还可以将 `priority` 属性设置为在父组中建立菜单的相对位置。

   > [!NOTE]
   > `priority`特性不适用于工具栏和上下文菜单。

2. Visual Studio IDE 中的所有命令都必须由命令组托管，命令组是菜单和工具栏的直接子级。 如果要向 IDE 添加新菜单或工具栏，它们必须包含新的命令组。 你还可以向现有菜单和工具栏添加命令组，以便可以直观地对命令进行分组。

    添加新的命令组时，必须首先创建一个 `Groups` 元素，然后将每个命令组的[组](../../extensibility/group-element.md)元素添加到该元素。

    设置 `guid` `id` 每个元素的和属性 `Group` ，然后设置 `priority` 属性以建立父菜单上的组的相对位置。 有关详细信息，请参阅[创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

3. 如果要向 IDE 添加新命令，请将元素添加 `Buttons` 到 `Commands` 元素。 然后，对于每个命令，将[Button](../../extensibility/button-element.md)元素添加到 `Buttons` 元素。

   1. 设置 `guid` `id` 每个元素的和属性 `Button` ，然后将属性设置 `type` 为所需的按钮类型。 你还可以将 `priority` 属性设置为在父组中建立命令的相对位置。

       > [!NOTE]
       > 用于 `type="button"` 工具栏上的标准菜单命令和按钮。

   2. 在 `Button` 元素中，添加一个包含[ButtonText](../../extensibility/buttontext-element.md)元素和[CommandName](../../extensibility/commandname-element.md)元素的[string](../../extensibility/strings-element.md)元素。 `ButtonText`元素为菜单项或工具栏按钮的工具提示提供文本标签。 `CommandName`元素提供要在命令中使用的命令的名称。

   3. 如果命令将包含一个图标，请在元素中创建一个[icon](../../extensibility/icon-element.md)元素 `Button` ，并将其 `guid` 和 `id` 属性设置为该图标的 `Bitmap` 元素。

       > [!NOTE]
       > 工具栏按钮必须具有图标。

   有关详细信息，请参阅[menucommand 与 OleMenuCommands](/visualstudio/misc/menucommands-vs-olemenucommands?view=vs-2015)。

4. 如果你的任何命令需要图标，请将一个[位图](../../extensibility/bitmaps-element.md)元素添加到 `Commands` 元素。 然后，对于每个图标，将[位图](../../extensibility/bitmap-element.md)元素添加到 `Bitmaps` 元素。 此处为指定位图资源位置的位置。 有关详细信息，请参阅[将图标添加到菜单命令](../../extensibility/adding-icons-to-menu-commands.md)。

   您可以依赖于父结构来正确放置大多数菜单、组和命令。 对于非常大的命令集，或当菜单、组或命令必须出现在多个位置时，建议指定命令位置。

#### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>依赖于在 IDE 中放置 UI 元素的父级

1. 对于典型的父级，请 `Parent` 在包中定义的每个 `Menu` 、 `Group` 和元素中创建一个元素 `Command` 。

    元素的目标 `Parent` 是将包含菜单、组或命令的菜单或组。

   1. 将 `guid` 属性设置为 `GuidSymbol` 定义命令集的元素的名称。 如果目标元素不是包的一部分，请使用该命令集的 guid （如相应的 *.vsct*文件中所定义）。

   2. 将 `id` 属性设置为与 `id` 目标菜单或组的属性相匹配。 有关 Visual Studio 公开的菜单和组的列表，请参阅[Visual studio 菜单的 guid 和 id](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)和[visual Studio 工具栏的 guid 和 id](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)。

   如果要在 IDE 中放置大量 UI 元素，或者如果元素出现在多个位置，请在[CommandPlacements](../../extensibility/commandplacements-element.md)元素中定义其位置，如以下步骤中所示。

#### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>使用命令放置在 IDE 中放置 UI 元素

1. 在 `Commands` 元素后面添加 `CommandPlacements` 元素。

2. 在 `CommandPlacements` 元素中，为 `CommandPlacement` 每个要放置的菜单、组或命令添加元素。

    每个 `CommandPlacement` 元素或 `Parent` 元素在一个 IDE 位置中放置一个菜单、组或命令。 一个 UI 元素只能有一个父级，但它可以有多个命令放置。 若要将 UI 元素放置在多个位置，请 `CommandPlacement` 为每个位置添加一个元素。

3. 将 `guid` `id` 每个元素的和属性设置 `CommandPlacement` 为宿主菜单或组，就像为元素所做的那样 `Parent` 。 您还可以设置 `priority` 属性以建立 UI 元素的相对位置。

   可以通过父级和命令放置来混合放置。 但对于非常大的命令集，我们建议你仅使用命令位置。

### <a name="add-specialized-behaviors"></a>添加专用行为
 可以使用[CommandFlag](../../extensibility/command-flag-element.md)元素修改菜单和命令的行为，例如，更改其外观和可见性。 你还可以通过使用[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)元素来影响命令的显示时间，或使用[键绑定](../../extensibility/keybindings-element.md)元素添加键盘快捷方式。 某些类型的菜单和命令已内置了专门的行为。

#### <a name="to-add-specialized-behaviors"></a>添加专用行为

1. 若要使 UI 元素仅在某些 UI 上下文中可见，例如，在加载解决方案时，请使用可见性约束。

   1. 在 `Commands` 元素后面添加 `VisibilityConstraints` 元素。

   2. 对于要约束的每个 UI 项，请添加一个[VisibilityItem](../../extensibility/visibilityitem-element.md)元素。

   3. 对于每个 `VisibilityItem` 元素，将 `guid` 和 `id` 属性设置为菜单、组或命令，然后将 `context` 属性设置为所需的 UI 上下文，如类中所定义 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> 。

2. 若要在代码中设置 UI 项的可见性或可用性，请使用以下一个或多个命令标志：

   - `DefaultDisabled`

   - `DefaultInvisible`

   - `DynamicItemStart`

   - `DynamicVisibility`

   - `NoShowOnMenuController`

   - `NotInTBList`

   有关详细信息，请参阅[CommandFlag](../../extensibility/command-flag-element.md)元素。

3. 若要更改元素的显示方式或动态更改其外观，请使用以下一个或多个命令标志：

   - `AlwaysCreate`

   - `CommandWellOnly`

   - `DefaultDocked`

   - `DontCache`

   - `DynamicItemStart`

   - `FixMenuController`

   - `IconAndText`

   - `Pict`

   - `StretchHorizontally`

   - `TextMenuUseButton`

   - `TextChanges`

   - `TextOnly`

   有关详细信息，请参阅[CommandFlag](../../extensibility/command-flag-element.md)元素。

4. 若要更改元素收到命令时的反应方式，请使用以下一个或多个命令标志：

   - `AllowParams`

   - `CaseSensitive`

   - `CommandWellOnly`

   - `FilterKeys`

   - `NoAutoComplete`

   - `NoButtonCustomize`

   - `NoKeyCustomize`

   - `NoToolbarClose`

   - `PostExec`

   - `RouteToDocs`

   - `TextIsAnchorCommand`

   有关详细信息，请参阅[CommandFlag](../../extensibility/command-flag-element.md)元素。

5. 若要将菜单相关的键盘快捷方式附加到菜单或菜单上的项，请在 `ButtonText` 菜单或菜单项的元素中添加 "&" 符（&）。 当父菜单打开时，与号后面的字符是活动的键盘快捷方式。

6. 若要将独立于菜单的键盘快捷方式附加到命令，请使用[键绑定](../../extensibility/keybindings-element.md)元素。 有关详细信息，请参阅[键绑定](../../extensibility/keybinding-element.md)元素。

7. 若要本地化菜单文本，请使用 `LocCanonicalName` 元素。 有关详细信息，请参阅[字符串](../../extensibility/strings-element.md)元素。

   某些菜单和按钮类型包括特殊行为。 以下列表描述了一些专门的菜单和按钮类型。 对于其他类型，请参见 `types` [菜单](../../extensibility/menu-element.md)、[按钮](../../extensibility/button-element.md)和[组合](../../extensibility/combo-element.md)元素中的属性说明。

   - 组合框：组合框是可在工具栏上使用的下拉列表。 若要将组合框添加到 UI，请在元素中创建一个[Combos](../../extensibility/combos-element.md)元素 `Commands` 。 然后，将添加到 `Combos` `Combo` 要添加的每个组合框的元素中。 `Combo`元素具有与元素相同的属性和子级 `Button` ，还具有 `DefaultWidth` 和 `idCommandList` 属性。 `DefaultWidth`特性设置宽度（以像素为单位）， `idCommandList` 属性指向用于填充组合框的命令 ID。

   - 菜单控制器：菜单控制器是一个按钮，该按钮旁有一个箭头。 单击箭头将打开一个列表。 若要将菜单控制器添加到 UI，请创建一个 `Menu` 元素，并将其 `type` 属性设置为 `MenuController` 或 `MenuControllerLatched` ，具体取决于所需的行为。 若要填充菜单控制器，请将其设置为元素的父项 `Group` 。 菜单控制器会在其下拉列表中显示该组的所有子级。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
- [Visual Studio 命令表（.vsct）文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [.VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)
