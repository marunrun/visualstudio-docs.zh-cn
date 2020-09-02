---
title: Vspackage 如何添加用户界面元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, adding elements
- UI element design [Visual Studio SDK], VSPackages
- VSPackages, contributing UI elements
ms.assetid: abc5d9d9-b267-48a1-92ad-75fbf2f4c1b9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d9cc3184009dd98e743064db1b8eb2abe6059d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "81649598"
---
# <a name="how-vspackages-add-user-interface-elements"></a>Vspackage 如何添加用户界面元素
VSPackage 可以通过 *.vsct* 文件 (UI) 元素（例如，菜单、工具栏和工具窗口）添加到 Visual Studio 的用户界面。

可在 [Visual Studio 用户体验指南](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中找到 UI 元素的设计指南。

## <a name="the-visual-studio-command-table-architecture"></a>Visual Studio 命令表体系结构
如上所述，命令表体系结构支持上述体系结构原则。 此命令表体系结构的抽象、数据结构和工具背后的原则如下：

- 有三种基本类型的项：菜单、命令和组。 菜单可以在 UI 中作为菜单、子菜单、工具栏或工具窗口公开。 命令是用户可以在 IDE 中执行的过程，它们可以作为菜单项、按钮、列表框或其他控件公开。 组是用于菜单和命令的容器。

- 每一项由描述项的定义、其相对于其他项的优先级以及修改其行为的标志指定。

- 每个项都有一个描述项的父项的位置。 一个项可以有多个父项，因此它可以出现在 UI 中的多个位置。

每个命令都必须将组作为其父项，即使它是该组中唯一的子节点也是如此。 每个标准菜单还必须有一个父组。 工具栏和工具窗口充当其自身的父级。 组可以将主 Visual Studio 菜单栏或菜单、工具栏或工具窗口作为其父项。

### <a name="how-items-are-defined"></a>如何定义项
*.Vsct*文件采用 XML 格式。 它定义包的 UI 元素并确定这些元素在 IDE 中的显示位置。 包中的每个菜单、组或命令首先在部分中分配了 GUID 和 ID `Symbols` 。 在 *.vsct* 文件的其余部分中，每个菜单、命令和组都由其 GUID 和 ID 组合标识。 以下示例显示在 `Symbols` 模板中选择了 **菜单命令** 时 Visual Studio 包模板生成的典型节。

```xml
<Symbols>
  <!-- This is the package guid. -->
  <GuidSymbol name="guidMenuTextPkg" value="{b1253bc6-d266-402b-89e7-5e3d3b22c746}" />

  <!-- This is the guid used to group the menu commands together -->
  <GuidSymbol name="guidMenuTextCmdSet" value="{a633d4e4-6c65-4436-a138-1abeba7c9a69}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
  </GuidSymbol>

  <GuidSymbol name="guidImages" value="{53323d9a-972d-4671-bb5b-9e418480922f}">
    <IDSymbol name="bmpPic1" value="1" />
    <IDSymbol name="bmpPic2" value="2" />
    <IDSymbol name="bmpPicSearch" value="3" />
    <IDSymbol name="bmpPicX" value="4" />
    <IDSymbol name="bmpPicArrows" value="5" />
  </GuidSymbol>
</Symbols>
```

部分的顶级元素 `Symbols` 是 [GuidSymbol 元素](../../extensibility/guidsymbol-element.md)。 `GuidSymbol` 元素将名称映射到由 IDE 用于标识包及其组件部分的 Guid。

> [!NOTE]
> Guid 由 Visual Studio 包模板自动生成。 还可以通过单击 "**工具**" 菜单上的 "**创建 guid** " 来创建唯一的 guid。

第一个 `GuidSymbol` 元素 `guid<PackageName>Pkg` 是包本身的 GUID。 这是 Visual Studio 用来加载包的 GUID。 通常，它不具有子元素。

按照约定，菜单和命令在第二个元素下分组， `GuidSymbol` `guid<PackageName>CmdSet` 位图位于第三个 `GuidSymbol` 元素下 `guidImages` 。 您不必遵循此约定，但每个菜单、组、命令和位图都必须是元素的子 `GuidSymbol` 元素。

在 `GuidSymbol` 表示 package 命令集的第二个元素中，是多个 `IDSymbol` 元素。 每个 [IDSymbol 元素](../../extensibility/idsymbol-element.md) 将名称映射到一个数值，并且可能表示作为命令集的一部分的菜单、组或命令。 `IDSymbol`第三个元素中的元素 `GuidSymbol` 表示可用作命令图标的位图。 由于 GUID/ID 对在应用程序中必须是唯一的，因此，同一元素的两个子级不能 `GuidSymbol` 具有相同的值。

### <a name="menus-groups-and-commands"></a>菜单、组和命令
当菜单、组或命令具有 GUID 和 ID 时，可以将其添加到 IDE 中。 每个 UI 元素必须具有以下内容：

- 一个 `guid` 属性，该属性与定义 UI 元素的元素的名称相匹配 `GuidSymbol` 。

- `id`与关联的元素的名称相匹配的属性 `IDSymbol` 。

同时， `guid` 和 `id` 特性构成 UI 元素的 *签名* 。

- 一个 `priority` 特性，确定 UI 元素在其父菜单或组中的位置。

- 具有和特性的 [父元素](../../extensibility/parent-element.md) ， `guid` `id` 它们指定了父菜单或组的签名。

#### <a name="menus"></a>菜单
每个菜单都定义为节中的 [menu 元素](../../extensibility/menu-element.md) `Menus` 。 菜单必须具有 `guid` 、和 `id` 属性以及 `priority` `Parent` 元素，还必须具有以下附加属性和子级：

- 一个 `type` 特性，该特性指定菜单应作为菜单类型还是作为工具栏出现在 IDE 中。

- 一个包含[ButtonText 元素](../../extensibility/buttontext-element.md)的[string 元素](../../extensibility/strings-element.md)，该元素指定 IDE 中的菜单的标题和一个[CommandName 元素](../../extensibility/commandname-element.md)，该元素指定在**命令**窗口中用于访问菜单的名称。

- 可选标志。 [CommandFlag 元素](../../extensibility/command-flag-element.md)可能出现在菜单定义中，以更改其在 IDE 中的外观或行为。

每个 `Menu` 元素都必须有一个组作为其父元素，除非它是一个可停靠的元素（如工具栏）。 可停靠菜单是其自身的父级。 有关属性的菜单和值的详细信息 `type` ，请参阅 [Menu 元素](../../extensibility/menu-element.md) 文档。

下面的示例显示一个菜单，该菜单显示在 Visual Studio 菜单栏上的 " **工具** " 菜单旁边。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
  <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
  <Strings>
    <ButtonText>TestMenu</ButtonText>
    <CommandName>TestMenu</CommandName>
  </Strings>
</Menu>
```

#### <a name="groups"></a>组
组是在 .vsct 文件的部分中定义的项 `Groups` 。 *.vsct* 组只是容器。 它们不会在 IDE 中显示，除非是菜单上的分隔线。 因此， [Group 元素](../../extensibility/group-element.md) 仅由其签名、优先级和父项定义。

一个组可以有一个菜单、另一个组或其本身作为父项。 但是，父级通常是菜单或工具栏。 前面示例中的菜单是组的子级 `IDG_VS_MM_TOOLSADDINS` ，该组是 Visual Studio 菜单栏的子组。 以下示例中的组是前面示例中的菜单的子组。

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

因为它是菜单的一部分，所以此组通常包含命令。 但是，它还可以包含其他菜单。 这就是子菜单的定义方式，如以下示例中所示。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="SubMenu" priority="0x0100" type="Menu">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"/>
  <Strings>
    <ButtonText>Sub Menu</ButtonText>
    <CommandName>Sub Menu</CommandName>
  </Strings>
</Menu>
```

#### <a name="commands"></a>命令
向 IDE 提供的命令被定义为 [Button 元素](../../extensibility/button-element.md) 或 [组合元素](../../extensibility/combo-element.md)。 若要显示在菜单或工具栏上，该命令必须具有组作为其父项。

##### <a name="buttons"></a>按钮
按钮在部分中定义 `Buttons` 。 用户单击以执行单个命令的任何菜单项、按钮或其他元素都被视为按钮。 某些按钮类型还可以包含列表功能。 按钮具有菜单具有的必需属性和可选属性，并且还可以具有一个 [Icon 元素](../../extensibility/icon-element.md) ，该元素指定表示 IDE 中的按钮的位图的 GUID 和 ID。 有关按钮及其属性的详细信息，请参阅 [钮扣元素](../../extensibility/buttons-element.md) 文档。

以下示例中的按钮是前面示例中的组的子级，并将在 IDE 中显示为该组父菜单上的菜单项。

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

##### <a name="combos"></a>Combos
Combos 在部分中定义 `Combos` 。 每个 `Combo` 元素都表示 IDE 中的一个下拉列表框。 用户可以或不能写入列表框，具体取决于组合的属性的值 `type` 。 Combos 具有按钮具有的相同元素和行为，还可以具有以下附加属性：

- `defaultWidth`指定像素宽度的特性。

- 一个 `idCommandList` 特性，该特性指定包含列表框中显示的项的列表。 命令列表必须在包含组合的同一节点中声明 `GuidSymbol` 。

下面的示例定义了一个组合元素。

```xml
<Combos>
  <Combo guid="guidFirstToolWinCmdSet"
         id="cmdidWindowsMediaFilename"
         priority="0x0100" type="DynamicCombo"
         idCommandList="cmdidWindowsMediaFilenameGetList"
         defaultWidth="130">
    <Parent guid="guidFirstToolWinCmdSet"
            id="ToolbarGroupID" />
    <CommandFlag>IconAndText</CommandFlag>
    <CommandFlag>CommandWellOnly</CommandFlag>
    <CommandFlag>StretchHorizontally</CommandFlag>
    <Strings>
      <CommandName>Filename</CommandName>
      <ButtonText>Enter a Filename</ButtonText>
    </Strings>
  </Combo>
</Combos>
```

##### <a name="bitmaps"></a>位图
将与图标一起显示的命令必须包含 `Icon` 使用其 GUID 和 ID 引用位图的元素。 每个位图定义为节中的 [位图元素](../../extensibility/bitmap-element.md) `Bitmaps` 。 定义唯一必需的属性 `Bitmap` 是 `guid` 和 `href` ，它们指向源文件。 如果源文件是资源条，则还需要 **usedList** 属性来列出条带中的可用图像。 有关详细信息，请参阅 [Bitmap 元素](../../extensibility/bitmap-element.md) 文档。

### <a name="parenting"></a>父级
以下规则控制项如何将另一项作为其父级来调用。

|元素|在命令表的此部分中定义|可以 (作为父项，也可以在节中放置 `CommandPlacements` ，或同时包含这两种) |可能包含被称为父级)  (|
|-------------| - | - | - |
|组|[Groups 元素](../../extensibility/groups-element.md)、IDE、其他 vspackage|菜单、组、项本身|菜单、组和命令|
|菜单|[菜单元素](../../extensibility/menus-element.md)、IDE、其他 vspackage|1到 *n* 组|0到 *n* 组|
|工具栏|[菜单元素](../../extensibility/menus-element.md)、IDE、其他 vspackage|项本身|0到 *n* 组|
|菜单项|[按钮元素](../../extensibility/buttons-element.md)、IDE、其他 vspackage|1到 *n* 组，项本身|-0 到 *n* 组|
|Button|[按钮元素](../../extensibility/buttons-element.md)、IDE、其他 vspackage|1到 *n* 组，项本身||
|组合图|[Combos 元素](../../extensibility/combos-element.md)，IDE，其他 vspackage|1到 *n* 组，项本身||

### <a name="menu-command-and-group-placement"></a>菜单、命令和组放置
菜单、组或命令可以出现在 IDE 的多个位置中。 要使项出现在多个位置，必须将其 `CommandPlacements` 作为 [CommandPlacement 元素](../../extensibility/commandplacement-element.md)添加到节中。 任何菜单、组或命令均可作为命令位置添加。 但是，不能以这种方式定位工具栏，因为它们不能出现在多个区分上下文的位置。

命令放置具有 `guid` 、 `id` 和 `priority` 属性。 GUID 和 ID 必须与定位的项的 GUID 和 ID 匹配。 `priority`特性控制项相对于其他项的位置。 当 IDE 合并具有相同优先级的两个或多个项时，它们的位置是不确定的，因为 IDE 不保证每次生成包时按相同顺序读取包资源。

如果菜单或组出现在多个位置，则该菜单或组的所有子级都将显示在每个实例中。

## <a name="command-visibility-and-context"></a>命令可见性和上下文
安装多个 Vspackage 时，菜单、菜单项和工具栏的如此可能会打乱 IDE 的混乱程度。 若要避免此问题，可以使用 *可见性约束* 和命令标志来控制各个 UI 元素的可见性。

### <a name="visibility-constraints"></a>可见性约束
可见性约束设置为部分中的 [VisibilityItem 元素](../../extensibility/visibilityitem-element.md) `VisibilityConstraints` 。 可见性约束定义了可在其中查看目标项的特定 UI 上下文。 仅当其中一个定义的上下文处于活动状态时，才会显示此部分中包含的菜单或命令。 如果未在此部分中引用菜单或命令，默认情况下它始终可见。 本部分不适用于组。

`VisibilityItem` 元素必须具有三个属性，如下所示 `guid` ： `id` 目标 UI 元素和的和 `context` 。 `context`特性指定目标项何时可见，并将任何有效的 UI 上下文作为其值。 Visual Studio 的 UI 上下文常量是类的成员 <xref:Microsoft.VisualStudio.VSConstants> 。 每个 `VisibilityItem` 元素只能采用一个上下文值。 若要应用第二个上下文，请创建一个指向同一项的第二个 `VisibilityItem` 元素，如下面的示例中所示。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

### <a name="command-flags"></a>命令标志
以下命令标志可能会影响应用于的菜单和命令的可见性。

`AlwaysCreate` 即使没有组或按钮，也会创建菜单。

适用于： `Menu`

`CommandWellOnly` 如果命令未显示在顶级菜单上，并且您要使其可用于其他外壳自定义（例如，将其绑定到密钥），请应用此标志。 安装 VSPackage 后，用户可以通过打开 " **选项** " 对话框，然后编辑 " **键盘环境** " 类别下的命令位置来自定义这些命令。 不影响快捷菜单、工具栏、菜单控制器或子菜单上的位置。

适用于： `Button` 、 `Combo`

`DefaultDisabled` 默认情况下，如果未加载实现该命令的 VSPackage 或未调用 QueryStatus 方法，则该命令处于禁用状态。

适用于： `Button` 、 `Combo`

`DefaultInvisible` 默认情况下，如果未加载实现命令的 VSPackage 或未调用 QueryStatus 方法，则该命令将不可见。

应与 `DynamicVisibility` 标志结合。

适用于： `Button` 、 `Combo` 、 `Menu`

`DynamicVisibility` 可以通过使用该 `QueryStatus` 部分中包含的方法或上下文 GUID 来更改该命令的可见性 `VisibilityConstraints` 。

适用于菜单上显示的命令，而不是工具栏上的命令。 当 `OLECMDF_INVISIBLE` 从方法返回标志时，可以禁用顶级工具栏项，但不能隐藏 `QueryStatus` 。

在菜单上，此标志还指示在隐藏其成员时应自动隐藏它。 此标志通常分配给子菜单，因为顶级菜单已经有了此行为。

应与 `DefaultInvisible` 标志结合。

适用于： `Button` 、 `Combo` 、 `Menu`

`NoShowOnMenuController` 如果将具有此标志的命令定位在菜单控制器上，则该命令不会出现在下拉列表中。

适用于： `Button`

有关命令标志的详细信息，请参阅 [CommandFlag 元素](../../extensibility/command-flag-element.md) 文档。

#### <a name="general-requirements"></a>一般要求
你的命令必须传递以下系列的测试，然后才能显示和启用：

- 命令位置正确。

- `DefaultInvisible`未设置标志。

- 父菜单或工具栏可见。

- 由于 [VisibilityConstraints 元素](../../extensibility/visibilityconstraints-element.md) 部分中的上下文条目，命令不可见。

- 用于实现接口的 VSPackage 代码会 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 显示并启用你的命令。 没有接口代码截获并对其进行操作。

- 当用户单击你的命令时，它将受到 [路由算法](../../extensibility/internals/command-routing-algorithm.md)中所述的过程的制约。

## <a name="call-pre-defined-commands"></a>调用预定义的命令
[UsedCommands 元素](../../extensibility/usedcommands-element.md)使 vspackage 可以访问由其他 VSPACKAGE 或 IDE 提供的命令。 为此，请创建一个 [UsedCommand 元素](../../extensibility/usedcommand-element.md) ，该元素具有要使用的命令的 GUID 和 ID。 这可确保命令将由 Visual Studio 加载，即使它不是当前 Visual Studio 配置的一部分也是如此。 有关详细信息，请参阅 [UsedCommand 元素](../../extensibility/usedcommand-element.md)。

## <a name="interface-element-appearance"></a>接口元素外观
选择和定位命令元素的注意事项如下：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供了许多不同的位置显示的 UI 元素。

- 使用标志定义的 UI 元素 `DefaultInvisible` 将不会显示在 IDE 中，除非它是通过其 VSPackage 实现显示的 <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> ，或与部分中的特定 UI 上下文相关联 `VisibilityConstraints` 。

- 甚至可能不会显示成功定位的命令。 这是因为 IDE 会自动隐藏或显示某些命令，具体取决于 VSPackage 已 (或未) 实现的接口。 例如，VSPackage 的某些生成接口的实现将导致自动显示生成相关菜单项。

- `CommandWellOnly`在 UI 元素的定义中应用标志意味着只能通过自定义添加该命令。

- 命令仅在某些 UI 上下文中可用，例如，当 IDE 在设计视图中时显示对话框。

- 若要使某些 UI 元素在 IDE 中显示，您必须实现一个或多个接口或编写一些代码。

## <a name="see-also"></a>另请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
