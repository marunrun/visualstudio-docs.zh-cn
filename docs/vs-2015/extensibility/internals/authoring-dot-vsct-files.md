---
title: 创作。Vsct 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 85e466e7ebb6294a77e89040260c16fe0043e372
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437671"
---
# <a name="authoring-vsct-files"></a>创作。Vsct 文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本文档演示如何创作.vsct 文件以将菜单项、 工具栏和其他用户界面 (UI) 元素添加到 Visual Studio 集成的开发环境 (IDE)。 将 UI 元素添加到不具备.vsct 文件 Visual Studio 包 (VSPackage) 时，请使用以下步骤。  
  
 对于新项目，我们建议你使用 Visual Studio 包模板，因为它会生成一个.vsct 文件，具体取决于你的选择，已具有菜单命令、 工具窗口，或自定义编辑器所需的元素。 您可以修改此.vsct 文件以满足你的 VSPackage 的要求。 有关如何修改.vsct 文件的详细信息，请参阅中的示例[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。  
  
## <a name="authoring-the-file"></a>编写文件  
 在这些阶段中创作.vsct 文件：创建文件和资源的结构、 声明的 UI 元素、 将 UI 元素放在 IDE 中，并添加任何专用的行为。  
  
### <a name="file-structure"></a>文件结构  
 .Vsct 文件的基本结构[CommandTable](../../extensibility/commandtable-element.md)根元素，其中包含[命令](../../extensibility/commands-element.md)元素和一个[符号](../../extensibility/symbols-element.md)元素。  
  
##### <a name="to-create-the-file-structure"></a>若要创建的文件结构  
  
1. 按照中的步骤将.vsct 文件添加到你的项目[如何：创建。Vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。  
  
2. 添加到所需命名空间`CommandTable`元素，如下面的示例中所示。  
  
    ```xml  
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"   
        xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  
    ```  
  
3. 在中`CommandTable`元素中，添加`Commands`要承载您的自定义菜单、 工具栏、 命令组和命令的所有元素。 以便可以加载自定义的 UI 元素，`Commands`元素必须具有其`Package`属性设置为包的名称。  
  
     之后`Commands`元素中，添加`Symbols`元素定义的包和名称的 Guid 和命令 Id 的 UI 元素。  
  
### <a name="including-visual-studio-resources"></a>包括 Visual Studio 资源  
 使用[Extern](../../extensibility/extern-element.md)要访问文件，用于定义 Visual Studio 命令和菜单在 IDE 中将 UI 元素所需的元素。 如果要将您的包的外部定义的命令，使用[UsedCommands](../../extensibility/usedcommands-element.md)元素以通知 Visual Studio。  
  
##### <a name="to-include-visual-studio-resources"></a>若要包括的 Visual Studio 资源  
  
1. 在顶部`CommandTable`元素中，添加一个`Extern`元素为每个外部文件引用，并设置`href`属性的文件的名称。 你可以引用以下的标头文件，若要访问 Visual Studio 资源：  
  
    - Stdidcmd.h，由 Visual Studio 公开的所有命令的定义 Id。  
  
    - Vsshlids.h，包含用于 Visual Studio 菜单的命令 Id。  
  
2. 如果您的包调用由 Visual Studio 或其他包定义的任何命令，将添加`UsedCommands`元素后的`Commands`元素。 填充此元素与[UsedCommand](../../extensibility/usedcommand-element.md)调用是不是您的包的一部分的每个命令的元素。 设置`guid`并`id`的属性`UsedCommand`元素与要调用的命令 GUID 和 ID 值。 有关如何查找 Guid 和 Id 的 Visual Studio 命令的详细信息，请参阅[Guid 和 Id 的 Visual Studio 命令](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)。 若要从其他包调用命令，使用 GUID 和这些包在.vsct 文件中定义的命令的 ID。  
  
### <a name="declaring-ui-elements"></a>声明 UI 元素  
 声明中的所有新 UI 元素`Symbols`.vsct 文件的部分。  
  
##### <a name="to-declare-ui-elements"></a>若要声明的 UI 元素  
  
1. 在中`Symbols`元素中，添加三个[GuidSymbol](../../extensibility/guidsymbol-element.md)元素。 每个`GuidSymbol`元素具有`name`属性和一个`value`属性。 设置`name`属性，以便其能够反映元素的用途。 `value`属性采用一个 GUID。 (若要在生成 GUID，**工具**菜单上，单击**创建 GUID**，然后选择**注册表格式**。)  
  
     第一个`GuidSymbol`元素表示您的软件包，并通常没有任何子级。 第二个`GuidSymbol`元素表示该命令设置，并将包含所有菜单、 组和命令定义的符号。 第三个`GuidSymbol`元素表示映像存储区，并包含所有命令的图标的符号。 如果不必须使用图标的任何命令，则可以省略第三个`GuidSymbol`元素。  
  
2. 在中`GuidSymbol`元素，它表示命令集，添加一个或多个[IDSymbol](../../extensibility/idsymbol-element.md)元素。 每个表示菜单、 工具栏、 组或要添加到用户界面的命令。  
  
     每个`IDSymbol`元素中，设置`name`属性为您的名称将用于指代相应的菜单、 组或命令，然后设置`value`为十六进制数字表示其命令 id 的元素。没有两个`IDSymbol`具有相同的父元素可以具有相同的值。  
  
3. 如果任何 UI 元素需要的图标，添加`IDSymbol`元素的每个图标到`GuidSymbol`元素，它表示映像存储区。  
  
### <a name="putting-ui-elements-in-the-ide"></a>在 IDE 中将 UI 元素  
 [菜单](../../extensibility/menus-element.md)元素，[组](../../extensibility/groups-element.md)元素，并[按钮](../../extensibility/buttons-element.md)元素包含的所有菜单、 组和您的包中定义的命令定义。 通过使用在 IDE 中放置这些菜单、 组和命令[父](../../extensibility/parent-element.md)元素，它是一部分的 UI 元素定义，或使用[CommandPlacement](../../extensibility/commandplacement-element.md)元素的其他位置定义。  
  
 每个`Menu`， `Group`，并`Button`元素具有`guid`属性和一个`id`属性。 始终设置`guid`要匹配的名称特性`GuidSymbol`元素，它表示您的命令设置，并设置`id`属性的名称为`IDSymbol`元素，它表示菜单、 组或命令中`Symbols`部分。  
  
##### <a name="to-define-ui-elements"></a>若要定义用户界面元素  
  
1. 如果您要定义任何新的菜单、 子菜单、 快捷菜单或工具栏，添加`Menus`元素`Commands`元素。 然后，对于要创建每个菜单上，添加[菜单](../../extensibility/menu-element.md)元素`Menus`元素。  
  
    设置`guid`并`id`的属性`Menu`元素，并设置`type`的所需的菜单类型的属性。 此外可以设置`priority`特性来确定父组中的菜单的相对位置。  
  
   > [!NOTE]
   > `priority`属性不适用于工具栏和上下文菜单。  
  
2. Visual Studio IDE 中的所有命令都必须直接子项的菜单和工具栏的命令组由都承载。 如果要向 IDE 添加新菜单或工具栏，它们必须包含新的命令组。 可能还向现有菜单和工具栏添加命令组，以便你命令可以直观地进行分组。  
  
    当添加新的命令组时，必须首先创建`Groups`元素，然后将添加到它[组](../../extensibility/group-element.md)为每个命令组的元素。  
  
    设置`guid`并`id`每个属性`Group`元素，并设置`priority`特性来确定父菜单上的组的相对位置。 有关详细信息，请参阅[按钮创建可重用组](../../extensibility/creating-reusable-groups-of-buttons.md)。  
  
3. 如果您要向 IDE 添加新的命令，将添加`Buttons`元素`Commands`元素。 然后，对于每个命令，添加[按钮](../../extensibility/button-element.md)元素`Buttons`元素。  
  
   1. 设置`guid`并`id`每个属性`Button`元素，并设置`type`的所需的按钮类型的属性。 此外可以设置`priority`特性来确定父组中的命令的相对位置。  
  
      > [!NOTE]
      > 使用`type="button"`标准菜单命令和工具栏上的按钮。  
  
   2. 在中`Button`元素中，添加[字符串](../../extensibility/strings-element.md)元素，其中包含[ButtonText](../../extensibility/buttontext-element.md)元素和一个[CommandName](../../extensibility/commandname-element.md)元素。 `ButtonText`元素提供为菜单项或工具栏按钮的工具提示的文本标签。 `CommandName`元素提供要在命令中也使用的命令的名称。  
  
   3. 如果您的命令将具有一个图标，创建[图标](../../extensibility/icon-element.md)中的元素`Button`元素，并将设置其`guid`并`id`属性到`Bitmap`图标的元素。  
  
      > [!NOTE]
      > 工具栏按钮必须具有图标。  
  
      有关详细信息，请参阅[MenuCommands 与。OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md)。  
  
4. 如果你的命令的任何需要的图标，添加[位图](../../extensibility/bitmaps-element.md)元素`Commands`元素。 然后，对于每个图标，添加[位图](../../extensibility/bitmap-element.md)元素`Bitmaps`元素。 这是你在其中指定位图资源的位置。 有关详细信息，请参阅[添加到菜单命令的图标](../../extensibility/adding-icons-to-menu-commands.md)。  
  
   您可以依赖子女教养结构正确放置大多数菜单、 组和命令。 对于非常大的命令集，或当菜单、 组或命令必须出现在多个位置中，我们建议您指定命令放置。  
  
##### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>若要依赖于在 IDE 中将 UI 元素的子级  
  
1. 有关典型设置父级，创建`Parent`中每个元素`Menu`， `Group`，和`Command`在包中定义的元素。  
  
    目标的`Parent`元素是菜单或将包含菜单上的组、 组或命令。  
  
   1. 设置`guid`属性的名称为`GuidSymbol`元素，用于定义设置的命令。 如果目标元素不是包的一部分，该命令集，使用的 guid 对应的.vsct 文件中定义。  
  
   2. 设置`id`属性以匹配`id`目标菜单或组的属性。 有关菜单和由 Visual Studio 公开的组的列表，请参阅[Guid 和 Id 的 Visual Studio 菜单](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或[Guid 和 Id 的 Visual Studio 工具栏](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)。  
  
   如果有大量的 UI 元素将在 IDE 中，或者您有应出现在多个位置的元素，定义在其位置[CommandPlacements](../../extensibility/commandplacements-element.md)元素，如以下步骤中所示。  
  
##### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>若要使用命令放置在 IDE 中将 UI 元素  
  
1. 之后`Commands`元素中，添加`CommandPlacements`元素。  
  
2. 在中`CommandPlacements`元素中，添加`CommandPlacement`为每个菜单、 组或命令放置的元素。  
  
    每个`CommandPlacement`元素或`Parent`元素放在一个 IDE 位置放置一个菜单、 组或命令。 UI 元素只能有一个父级，但它可以具有多个命令放置。 若要将 UI 元素放在多个位置，将添加`CommandPlacement`为每个位置的元素。  
  
3. 设置`guid`并`id`每个属性`CommandPlacement`元素到托管的菜单或组，就像您一样`Parent`元素。 您还可以设置`priority`特性来确定的 UI 元素的相对位置。  
  
   可以混合使用通过设置父级的位置和命令位置。 但是，对于非常大的命令集，我们建议使用仅命令放置。  
  
### <a name="adding-specialized-behaviors"></a>添加专用的行为  
 可以使用[CommandFlag](../../extensibility/command-flag-element.md)元素若要修改的行为的菜单和命令，例如，若要更改其外观和可见性。 可能还会影响当命令是可见的通过使用[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)，或通过使用添加键盘快捷方式[键绑定](../../extensibility/keybindings-element.md)。 某些类型的菜单和命令已拥有的专用内置的行为。  
  
##### <a name="to-add-specialized-behaviors"></a>若要添加专用的行为  
  
1. 若要在加载解决方案时显示仅在某些 UI 上下文中，例如，UI 元素，使用可见性限制。  
  
   1. 之后`Commands`元素中，添加`VisibilityConstraints`元素。  
  
   2. 若要将限制每个 UI 项，将添加[VisibilityItem](../../extensibility/visibilityitem-element.md)元素。  
  
   3. 每个`VisibilityItem`元素中，设置`guid`并`id`与菜单、 组或命令和设置的属性`context`属性为所需的 UI 上下文中定义<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>类。 有关详细信息，请参阅[VisibilityItem 元素](../../extensibility/visibilityitem-element.md)。  
  
2. 若要在代码中设置的可见性或可用性 UI 项，使用一个或多个以下的命令标志：  
  
   - DefaultDisabled  
  
   - DefaultInvisible  
  
   - DynamicItemStart  
  
   - DynamicVisibility  
  
   - NoShowOnMenuController  
  
   - NotInTBList  
  
     有关详细信息，请参阅[Command Flag 元素](../../extensibility/command-flag-element.md)。  
  
3. 若要更改元素出现，或动态更改其外观的方式，使用一个或多个以下的命令标志：  
  
   - AlwaysCreate  
  
   - CommandWellOnly  
  
   - DefaultDocked  
  
   - DontCache  
  
   - DynamicItemStart  
  
   - FixMenuController  
  
   - IconAndText  
  
   - pict  
  
   - StretchHorizontally  
  
   - TextMenuUseButton  
  
   - TextChanges  
  
   - TextOnly  
  
     有关详细信息，请参阅[Command Flag 元素](../../extensibility/command-flag-element.md)。  
  
4. 若要更改元素如何接收命令时做出响应，请使用一个或多个以下的命令标志：  
  
   - AllowParams  
  
   - CaseSensitive  
  
   - CommandWellOnly  
  
   - FilterKeys  
  
   - NoAutoComplete  
  
   - NoButtonCustomize  
  
   - NoKeyCustomize  
  
   - NoToolbarClose  
  
   - PostExec  
  
   - RouteToDocs  
  
   - TextIsAnchorCommand  
  
     有关详细信息，请参阅[Command Flag 元素](../../extensibility/command-flag-element.md)。  
  
5. 若要将依赖于菜单的键盘快捷方式附加到菜单或菜单上的项，添加一个 & 号字符 (&) 在`ButtonText`菜单或菜单项的元素。 打开父菜单时，遵循 & 符的字符是活动的键盘快捷方式。  
  
6. 若要将独立于菜单的键盘快捷方式附加到命令，使用[键绑定](../../extensibility/keybindings-element.md)。 有关详细信息，请参阅[KeyBinding 元素](../../extensibility/keybinding-element.md)。  
  
7. 若要将本地化的菜单文本，请使用`LocCanonicalName`元素。 有关详细信息，请参阅[字符串元素](../../extensibility/strings-element.md)。  
  
   一些菜单和按钮的类型包括专用的行为。 下表介绍一些专用的菜单和按钮类型。 对于其他类型，请参阅`types`属性中的说明[Menu Element](../../extensibility/menu-element.md)， [Button 元素](../../extensibility/button-element.md)，和[组合元素](../../extensibility/combo-element.md)。  
  
   组合框  
   组合框进行了可以使用工具栏的下拉列表。 若要将组合框添加到 UI 中，创建[Combos](../../extensibility/combos-element.md)中的元素`Commands`元素。 然后将添加到`Combos`元素`Combo`添加每个组合框的元素。 `Combo` 元素具有相同的属性和子级用作`Button`元素并且还要`DefaultWidth`和`idCommandList`属性。 `DefaultWidth`属性以像素为单位设置宽度和`idCommandList`属性指向用于填充组合框的命令 ID。 有关详细信息，请参阅`Combo`元素文档。  
  
   MenuController  
   菜单控制器是包含它旁边的箭头的按钮。 单击箭头将打开一个列表。 若要将菜单控制器添加到 UI 中，创建`Menu`元素，并设置其`type`归于**MenuController**或**MenuControllerLatched**，取决于所需的行为。 若要填充菜单控制器，请将其设置为父级的`Group`元素。 菜单控制器将在其下拉列表显示该组的所有子级。  
  
## <a name="see-also"></a>请参阅  
 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)   
 [Visual Studio 命令表 (。Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
