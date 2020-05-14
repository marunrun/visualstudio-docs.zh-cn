---
title: 创作。Vsct 文件 |微软文档
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
ms.openlocfilehash: dfa276d04e2d312d7ff00b1e9bc0015beb1e254e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709997"
---
# <a name="author-vsct-files"></a>作者 .vsct 文件
本文档演示如何创作 *.vsct*文件，将菜单项、工具栏和其他用户界面 （UI） 元素添加到 Visual Studio 集成开发环境 （IDE）。 将 UI 元素添加到尚未具有 *.vsct*文件的 Visual Studio 包 （VSPackage） 时，请使用以下步骤。

 对于新项目，我们建议您使用 Visual Studio 包模板，因为它会生成一个 *.vsct*文件，该文件根据您的选择，该文件已经具有菜单命令、工具窗口或自定义编辑器所需的元素。 您可以修改此 *.vsct*文件以满足 VSPackage 的要求。 有关如何修改 *.vsct*文件的详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)中的示例。

## <a name="author-the-file"></a>创作文件
 在这些阶段中编写一个 *.vsct*文件：为文件和资源创建结构，声明 UI 元素，将 UI 元素放入 IDE 中，并添加任何专用行为。

### <a name="file-structure"></a>文件结构
 *.vsct*文件的基本结构是命令[表](../../extensibility/commandtable-element.md)根元素，其中包含[命令](../../extensibility/commands-element.md)元素和[Symbols](../../extensibility/symbols-element.md)元素。

#### <a name="to-create-the-file-structure"></a>创建文件结构

1. 按照[操作中的步骤：创建 .vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)，将 *.vsct*文件添加到项目中。

2. 向`CommandTable`元素添加所需的命名空间，如以下示例所示：

    ```xml
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"
        xmlns:xs="http://www.w3.org/2001/XMLSchema">

    ```

3. 在`CommandTable`元素中，添加`Commands`一个元素来承载所有自定义菜单、工具栏、命令组和命令。 因此，自定义 UI 元素可以加载，`Commands`该元素的属性必须`Package`设置为包的名称。

     元素`Commands`之后，添加一个`Symbols`元素来定义包的 GUID，以及 UI 元素的名称和命令 ID。

### <a name="include-visual-studio-resources"></a>包括可视化工作室资源
 使用[Extern](../../extensibility/extern-element.md)元素访问定义 Visual Studio 命令的文件以及将 UI 元素放入 IDE 所需的菜单。 如果要使用包外定义的命令，请使用["已使用命令"](../../extensibility/usedcommands-element.md)元素通知 Visual Studio。

#### <a name="to-include-visual-studio-resources"></a>包括视觉工作室资源

1. 在`CommandTable`元素的顶部，为每个要引用的外部文件`Extern`添加一个元素，并将`href`属性设置为文件的名称。 您可以引用以下标头文件来访问 Visual Studio 资源：

   - *Stdidcmd.h*： 为 Visual Studio 公开的所有命令定义 ID。

   - *Vsshlids.h*： 包含可视化工作室菜单的命令 ID。

2. 如果包调用由 Visual Studio 或其他包定义的任何命令，请在`UsedCommands``Commands`元素之后添加元素。 对于不属于包的每个命令，使用[UsedCommand](../../extensibility/usedcommand-element.md)元素填充此元素。 将`UsedCommand`元素`guid`的`id`和 属性设置为要调用的命令的 GUID 和 ID 值。

   有关如何查找 Visual Studio 命令的 GUID 和 IT 的详细信息，请参阅[Visual Studio 命令的 GUID 和 IT。](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md) 要从其他包调用命令，请使用这些包 *.vsct*文件中定义的 GUID 和命令 ID。

### <a name="declare-ui-elements"></a>声明 UI 元素
 声明 *.vsct*文件`Symbols`部分中的所有新 UI 元素。

#### <a name="to-declare-ui-elements"></a>声明 UI 元素

1. 在元素`Symbols`中，添加三个[GuidSymbol](../../extensibility/guidsymbol-element.md)元素。 每个`GuidSymbol`元素都有一`name`个属性和`value`一个属性。 设置属性`name`，以便它反映元素的用途。 该`value`属性采用 GUID。 （要生成 GUID，请在 **"工具"** 菜单上，选择 **"创建 GUID"，** 然后选择**注册表格式**。

     第一`GuidSymbol`个元素表示包，通常没有子元素。 第二`GuidSymbol`个元素表示命令集，并将包含定义菜单、组和命令的所有符号。 第三`GuidSymbol`个元素表示图像存储，并包含命令的所有图标的符号。 如果没有使用图标的命令，则可以省略第三`GuidSymbol`个元素。

2. 在`GuidSymbol`表示命令集的元素中，添加一个或多个[IDSymbol](../../extensibility/idsymbol-element.md)元素。 其中每个表示要添加到 UI 的菜单、工具栏、组或命令。

     对于每个`IDSymbol`元素，将`name`属性设置为用于引用相应菜单、组或命令的名称，然后将`value`元素设置为表示其命令 ID 的十六进制数字。 没有两`IDSymbol`个具有相同父元素的元素可以具有相同的值。

3. 如果任何 UI 元素需要图标，请为每个`IDSymbol`图标添加一个元素到`GuidSymbol`表示图像存储的元素。

### <a name="put-ui-elements-in-the-ide"></a>将 UI 元素放入 IDE
 [菜单](../../extensibility/menus-element.md)、[组](../../extensibility/groups-element.md)和[按钮](../../extensibility/buttons-element.md)元素包含包中定义的所有菜单、组和命令的定义。 通过使用作为 UI 元素定义的一部分[的父](../../extensibility/parent-element.md)元素，或者使用在其他地方定义的[Command安置](../../extensibility/commandplacement-element.md)元素，将这些菜单、组和命令放在 IDE 中。

 每个`Menu` `Group`，`Button`和 元素`guid`都有一个`id`属性和一个属性。 `guid`始终将属性设置为匹配表示命令集`GuidSymbol`的元素的名称，并将`id`该属性设置为表示`IDSymbol``Symbols`节中菜单、组或命令的元素的名称。

#### <a name="to-define-ui-elements"></a>定义 UI 元素

1. 如果要定义任何新菜单、子菜单、快捷菜单或工具栏，则向`Menus``Commands`元素添加元素。 然后，要创建每个菜单，向`Menus`元素添加一个[菜单](../../extensibility/menu-element.md)元素。

    设置`Menu`元素`guid`的`id`和 属性，然后将`type`属性设置为所需的菜单类型。 还可以设置属性`priority`以在父组中建立菜单的相对位置。

   > [!NOTE]
   > 该`priority`属性不适用于工具栏和上下文菜单。

2. 可视化工作室 IDE 中的所有命令必须由命令组托管，命令组是菜单和工具栏的直接子级。 如果要向 IDE 添加新菜单或工具栏，这些菜单或工具栏必须包含新的命令组。 您还可以将命令组添加到现有菜单和工具栏中，以便可以直观地对命令进行分组。

    添加新命令组时，必须首先创建一个`Groups`元素，然后为每个命令组添加一个[组](../../extensibility/group-element.md)元素。

    设置每个`guid``id``Group`元素的 和 属性，然后设置`priority`属性以在父菜单上建立组的相对位置。 有关详细信息，请参阅[创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

3. 如果要向 IDE 添加新命令，则向元素`Buttons``Commands`添加元素。 然后，对于每个命令，向`Buttons`元素添加一个[Button](../../extensibility/button-element.md)元素。

   1. 设置每个`guid``id``Button`元素的 和 属性，然后将`type`属性设置为所需的按钮类型。 还可以设置属性`priority`以在父组中建立命令的相对位置。

       > [!NOTE]
       > 用于`type="button"`工具栏上的标准菜单命令和按钮。

   2. 在元素`Button`中，添加包含[ButtonText](../../extensibility/buttontext-element.md)元素和[命令名称](../../extensibility/commandname-element.md)元素的[字符串](../../extensibility/strings-element.md)元素。 该`ButtonText`元素提供菜单项的文本标签或工具栏按钮的工具提示。 该`CommandName`元素提供要在命令井中使用的命令的名称。

   3. 如果命令将具有图标，请在`Button`元素中创建一个[Icon](../../extensibility/icon-element.md)元素，并将`guid`其`id`和属性设置为`Bitmap`该图标的元素。

       > [!NOTE]
       > 工具栏按钮必须具有图标。

   有关详细信息，请参阅[菜单命令与 OleMenu 命令](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)。

4. 如果任何命令需要图标，请向`Commands`元素添加[位图](../../extensibility/bitmaps-element.md)元素。 然后，对于每个图标，向`Bitmaps`元素添加[位图](../../extensibility/bitmap-element.md)元素。 这是指定位图资源的位置的位置。 有关详细信息，请参阅[向菜单命令添加图标](../../extensibility/adding-icons-to-menu-commands.md)。

   您可以依赖父级结构正确放置大多数菜单、组和命令。 对于非常大的命令集，或者当菜单、组或命令必须出现在多个位置时，我们建议您指定命令放置。

#### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>依靠父子关系在 IDE 中放置 UI 元素

1. 对于典型的父级，请在每个`Parent``Menu`中`Group`创建一个元素`Command`，并在包中定义的元素。

    `Parent`元素的目标是包含菜单、组或命令的菜单或组。

   1. 将`guid`属性设置为定义命令集`GuidSymbol`的元素的名称。 如果目标元素不是包的一部分，请使用该命令集的 guid，如相应的 *.vsct*文件中定义的那样。

   2. 将`id`属性设置为匹配目标菜单`id`或组的属性。 有关 Visual Studio 公开的菜单和组的列表，请参阅 Visual Studio 菜单的[GUID 和 IT](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或[Visual Studio 工具栏的 GUID 和 IT。](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

   如果 ID 中要放置大量 UI 元素，或者元素应出现在多个位置，请将其放置在["命令放置"](../../extensibility/commandplacements-element.md)元素中，如以下步骤所示。

#### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>使用命令放置在 IDE 中放置 UI 元素

1. 在 `Commands` 元素后面添加 `CommandPlacements` 元素。

2. 在`CommandPlacements`元素中，为每个`CommandPlacement`菜单、组或要放置的命令添加一个元素。

    每个`CommandPlacement`元素或`Parent`元素在一个 IDE 位置放置一个菜单、组或命令。 UI 元素只能有一个父元素，但它可以有多个命令放置。 要将 UI 元素放置在多个位置，为每个`CommandPlacement`位置添加一个元素。

3. 将每个`guid``id``CommandPlacement`元素的 和 属性设置为宿主菜单或组，就像对元素一`Parent`样。 还可以设置属性`priority`以建立 UI 元素的相对位置。

   您可以通过父项和命令放置混合放置。 但是，对于非常大的命令集，我们建议您仅使用命令放置。

### <a name="add-specialized-behaviors"></a>添加专门行为
 可以使用[CommandFlag](../../extensibility/command-flag-element.md)元素修改菜单和命令的行为，例如，更改其外观和可见性。 您还可以使用[可见性约束](../../extensibility/visibilityconstraints-element.md)元素影响命令何时可见，或者通过使用[KeyBindings](../../extensibility/keybindings-element.md)元素添加键盘快捷键。 某些类型的菜单和命令已经内置了专门行为。

#### <a name="to-add-specialized-behaviors"></a>添加专门行为

1. 要使 UI 元素仅在某些 UI 上下文中可见（例如，加载解决方案时）请使用可见性约束。

   1. 在 `Commands` 元素后面添加 `VisibilityConstraints` 元素。

   2. 对于要约束的每个 UI 项，添加[可见性项目](../../extensibility/visibilityitem-element.md)元素。

   3. 对于每个`VisibilityItem`元素，将`guid`和`id`属性设置为菜单、组或命令，然后将`context`属性设置为所需的 UI 上下文（如<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>类中定义）。

2. 要在代码中设置 UI 项的可见性或可用性，请使用以下命令标志中的一个或多个：

   - `DefaultDisabled`

   - `DefaultInvisible`

   - `DynamicItemStart`

   - `DynamicVisibility`

   - `NoShowOnMenuController`

   - `NotInTBList`

   有关详细信息，请参阅[CommandFlag](../../extensibility/command-flag-element.md)元素。

3. 要更改元素的显示方式或动态更改其外观，请使用以下一个或多个命令标志：

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

4. 要更改元素在接收命令时的反应方式，请使用以下一个或多个命令标志：

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

5. 要将依赖于菜单的键盘快捷键附加到菜单或菜单上的项目，请在菜单或菜单项`ButtonText`的元素中添加一个 ampand 字符 （&）。 当父菜单打开时，放大器后面的字符是活动键盘快捷键。

6. 要将独立于菜单的键盘快捷键附加到命令，请使用[KeyBindings](../../extensibility/keybindings-element.md)元素。 有关详细信息，请参阅[键绑定](../../extensibility/keybinding-element.md)元素。

7. 要本地化菜单文本，请使用 元素`LocCanonicalName`。 有关详细信息，请参阅[字符串](../../extensibility/strings-element.md)元素。

   某些菜单和按钮类型包括专门行为。 下面的列表描述了一些专用菜单和按钮类型。 有关其他类型，请参阅`types`[菜单](../../extensibility/menu-element.md)、[按钮](../../extensibility/button-element.md)和[组合](../../extensibility/combo-element.md)元素中的属性说明。

   - 组合框：组合框是可在工具栏上使用的下拉列表。 要将组合框添加到 UI，请在`Commands`元素中创建[Combos](../../extensibility/combos-element.md)元素。 然后向`Combos`元素添加要添加`Combo`的每个组合框的元素。 `Combo`元素具有与`Button`元素相同的属性和子级，并且具有`DefaultWidth``idCommandList`和 属性。 属性`DefaultWidth`以像素为单位设置宽度，`idCommandList`该属性指向用于填充组合框的命令 ID。

   - 菜单控制器：菜单控制器是一个按钮，旁边有一个箭头。 单击箭头将打开一个列表。 要向 UI 添加菜单控制器，请创建`Menu`一个元素，`type`并根据所需的`MenuController`行为`MenuControllerLatched`将其属性设置为 或 。 要填充菜单控制器，将其设置为`Group`元素的父级。 菜单控制器将在其下拉列表中显示该组的所有子级。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
- [可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)
