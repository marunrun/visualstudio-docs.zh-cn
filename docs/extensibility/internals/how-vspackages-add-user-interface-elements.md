---
title: VS包如何添加用户界面元素 |微软文档
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
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649598"
---
# <a name="how-vspackages-add-user-interface-elements"></a>VS包如何添加用户界面元素
VSPackage 可以通过 *.vsct*文件将用户界面 （UI） 元素（例如菜单、工具栏和工具窗口）添加到 Visual Studio。

您可以在[Visual Studio 用户体验指南](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中找到 UI 元素的设计指南。

## <a name="the-visual-studio-command-table-architecture"></a>可视化工作室命令表体系结构
如上所述，命令表体系结构支持上述体系结构原则。 命令表体系结构的抽象、数据结构和工具背后的原理如下：

- 有三种基本类型的项：菜单、命令和组。 菜单可以在 UI 中作为菜单、子菜单、工具栏或工具窗口公开。 命令是用户可以在 IDE 中执行的过程，它们可以作为菜单项、按钮、列表框或其他控件公开。 组是菜单和命令的容器。

- 每个项都由描述项、相对于其他项的优先级以及修改其行为的标志的定义指定。

- 每个项都有一个描述项父项的位置。 项目可以有多个父项，以便它可以显示在 UI 中的多个位置。

每个命令都必须有一个组作为其父级，即使它是该组中的唯一子级。 每个标准菜单还必须有一个父组。 工具栏和工具窗口充当自己的父窗口。 组可以作为其父级主 Visual Studio 菜单栏，或任何菜单、工具栏或工具窗口。

### <a name="how-items-are-defined"></a>如何定义项目
*.vsct*文件以 XML 格式格式化。 它定义包的 UI 元素，并确定这些元素在 IDE 中的显示位置。 包中的每个菜单、组或命令首先在`Symbols`节中分配 GUID 和 ID。 在 *.vsct*文件的其余部分中，每个菜单、命令和组都通过其 GUID 和 ID 组合进行标识。 下面的示例显示了 Visual `Symbols` Studio 包模板在模板中选择**菜单命令**时生成的典型部分。

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

`Symbols`该部分的顶级元素是[GuidSymbol 元素](../../extensibility/guidsymbol-element.md)。 `GuidSymbol`元素将名称映射到 IDE 用于标识包及其组件部件的 GUID。

> [!NOTE]
> GUID 由 Visual Studio 包模板自动生成。 您还可以通过单击"工具"菜单上**的"创建 GUID"** 来创建唯一**GUID。**

第一`GuidSymbol`个元素`guid<PackageName>Pkg`， 是包本身的 GUID。 这是 Visual Studio 用于加载包的 GUID。 通常，它没有子元素。

按照惯例，菜单和命令被分组到第`GuidSymbol`二个元素下，`guid<PackageName>CmdSet`并且位图位于第三`GuidSymbol`个元素`guidImages`下。 您不必遵循此约定，但每个菜单、组、命令和位图必须是`GuidSymbol`元素的子级。

在第二`GuidSymbol`个元素（表示包命令集）中，是多个`IDSymbol`元素。 每个[IDSymbol 元素](../../extensibility/idsymbol-element.md)将名称映射到数值，并可以表示作为命令集一部分的菜单、组或命令。 第`IDSymbol`三`GuidSymbol`个元素中的元素表示位图，这些位图可用作命令的图标。 由于 GUID/ID 对在应用程序中必须是唯一的，因此同`GuidSymbol`一元素的两个子级可能具有相同的值。

### <a name="menus-groups-and-commands"></a>菜单、组和命令
当菜单、组或命令具有 GUID 和 ID 时，可以将其添加到 IDE 中。 每个 UI 元素都必须具有以下内容：

- 与`guid`UI 元素下定义的`GuidSymbol`元素的名称匹配的属性。

- 与`id`关联`IDSymbol`元素的名称匹配的属性。

`guid`和`id`属性一起组成 UI 元素*的签名*。

- 确定`priority`UI 元素在其父菜单或组中的位置的属性。

- 具有`guid`指定父菜单或`id`组签名的[父元素](../../extensibility/parent-element.md)和属性。

#### <a name="menus"></a>菜单
每个菜单都定义为`Menus`节中的[菜单元素](../../extensibility/menu-element.md)。 菜单必须具有`guid`和`id`属性`priority`以及`Parent`元素，以及以下附加属性和子项：

- 指定`type`菜单是否应作为菜单或工具栏显示在 IDE 中的属性。

- 包含[ButtonText 元素](../../extensibility/buttontext-element.md)的[字符串元素](../../extensibility/strings-element.md)，该元素指定 IDE 中菜单的标题，以及[命令名称元素](../../extensibility/commandname-element.md)，它指定**命令**窗口中用于访问菜单的名称。

- 可选标志。 [CommandFlag 元素](../../extensibility/command-flag-element.md)可能会出现在菜单定义中，以更改其在 IDE 中的外观或行为。

每个`Menu`元素都必须有一个组作为其父元素，除非它是可停靠的元素（如工具栏）。 可停靠菜单是其自己的父菜单。 有关`type`属性的菜单和值的详细信息，请参阅[菜单元素](../../extensibility/menu-element.md)文档。

下面的示例显示显示在"**工具**"菜单旁边的 Visual Studio 菜单栏上的菜单。

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
组是在`Groups`*.vsct*文件部分中定义的项。 组只是容器。 它们不显示在 IDE 中，除非是菜单上的分界线。 因此，[组元素](../../extensibility/group-element.md)仅由其签名、优先级和父元素定义。

组可以具有菜单、另一个组或本身作为父组。 但是，父级通常是菜单或工具栏。 前面的示例中的菜单是`IDG_VS_MM_TOOLSADDINS`组的子菜单，该组是 Visual Studio 菜单栏的子级。 以下示例中的组是前面示例中菜单的子级。

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

因为它是菜单的一部分，因此此组通常包含命令。 但是，它还可以包含其他菜单。 这是子菜单的定义方式，如以下示例所示。

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
提供给 IDE 的命令定义为[Button 元素](../../extensibility/button-element.md)或[组合元素](../../extensibility/combo-element.md)。 要显示在菜单或工具栏上，该命令必须具有组作为其父级。

##### <a name="buttons"></a>按钮
按钮在`Buttons`节中定义。 用户单击以执行单个命令的任何菜单项、按钮或其他元素都被视为按钮。 某些按钮类型还可以包括列表功能。 按钮具有与菜单相同的必需和可选属性，还可以具有[一个图标元素](../../extensibility/icon-element.md)，该元素指定表示 IDE 中按钮的位图的 GUID 和 ID。 有关按钮及其属性的详细信息，请参阅[Buttons 元素](../../extensibility/buttons-element.md)文档。

以下示例中的按钮是前面示例中的组的子级，并将作为该组父菜单上的菜单项显示在 IDE 中。

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

##### <a name="combos"></a>组合
组合在节中`Combos`定义。 每个`Combo`元素表示 IDE 中的下拉列表框。 列表框可能由用户写写，也可能不由用户写写，具体取决于组合`type`属性的值。 组合具有与按钮相同的元素和行为，也可以具有以下附加属性：

- 指定`defaultWidth`像素宽度的属性。

- 指定`idCommandList`包含列表框中显示的项目的列表的属性。 命令列表必须在包含组合的同`GuidSymbol`一节点中声明。

下面的示例定义组合元素。

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
与图标一起显示的命令必须包含一个`Icon`通过使用其 GUID 和 ID 引用位图的元素。 每个位图都定义为`Bitmaps`节中的[位图元素](../../extensibility/bitmap-element.md)。 定义的唯一`Bitmap`必需属性是`guid`和`href`，它指向源文件。 如果源文件是资源条，则还需要**使用 List**属性来列出条带中的可用图像。 有关详细信息，请参阅[位图元素](../../extensibility/bitmap-element.md)文档。

### <a name="parenting"></a>育儿
以下规则控制项如何将另一个项调用为其父项。

|元素|在命令表的此部分定义|可以包含（作为父级，或通过放置在`CommandPlacements`节中，或两者兼而有之）|可能包含（称为父级）|
|-------------| - | - | - |
|组|[组元素](../../extensibility/groups-element.md)，IDE，其他 VS 包|菜单、组、项目本身|菜单、组和命令|
|菜单|[菜单元素](../../extensibility/menus-element.md)，IDE，其他 VS 包|1 到*n*组|0 到*n*组|
|工具栏|[菜单元素](../../extensibility/menus-element.md)，IDE，其他 VS 包|项目本身|0 到*n*组|
|菜单项|[按钮元素](../../extensibility/buttons-element.md)，IDE，其他 VS 包|1 到*n*个组，项目本身|-0 到*n*组|
|Button|[按钮元素](../../extensibility/buttons-element.md)，IDE，其他 VS 包|1 到*n*个组，项目本身||
|组合图|[组合元素](../../extensibility/combos-element.md)，IDE，其他 VS 包|1 到*n*个组，项目本身||

### <a name="menu-command-and-group-placement"></a>菜单、命令和组放置
菜单、组或命令可以显示在 IDE 中的多个位置。 要将项显示在多个位置，必须将其添加`CommandPlacements`为[命令放置元素](../../extensibility/commandplacement-element.md)。 任何菜单、组或命令都可以添加为命令放置。 但是，工具栏不能以这种方式定位，因为它们不能出现在多个上下文相关位置。

命令位置具有`guid`和`id``priority`属性。 GUID 和 ID 必须与定位项的 ID 匹配。 属性`priority`控制项与其他项的放置。 当 IDE 合并具有相同优先级的两个或多个项时，它们的位置未定义，因为 IDE 不保证每次生成包时都按相同的顺序读取包资源。

如果菜单或组出现在多个位置，则该菜单或组的所有子级将显示在每个实例中。

## <a name="command-visibility-and-context"></a>命令可见性和上下文
安装多个 VS 包时，大量菜单、菜单项和工具栏可能会使 IDE 变得杂乱无章。 为了避免此问题，可以使用*可见性约束*和命令标志来控制各个 UI 元素的可见性。

### <a name="visibility-constraints"></a>可见性约束
可见性约束设置为`VisibilityConstraints`节中的[可见性项目元素](../../extensibility/visibilityitem-element.md)。 可见性约束定义目标项可见的特定 UI 上下文。 仅当其中一个定义的上下文处于活动状态时，本节中包含的菜单或命令才可见。 如果此部分中未引用菜单或命令，则默认情况下始终可见。 本节不适用于组。

`VisibilityItem`元素必须具有三个属性，如下所示：`guid`目标`id`UI 元素 和 和`context`。 该`context`属性指定目标项何时可见，并将任何有效的 UI 上下文作为其值。 Visual Studio 的 UI 上下文常量是<xref:Microsoft.VisualStudio.VSConstants>类的成员。 每个`VisibilityItem`元素只能获取一个上下文值。 要应用第二个上下文，请创建`VisibilityItem`指向同一项的第二个元素，如以下示例所示。

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
以下命令标志可能会影响它们应用于的菜单和命令的可见性。

`AlwaysCreate`即使菜单没有组或按钮，也会创建菜单。

有效期：`Menu`

`CommandWellOnly`如果命令未显示在顶级菜单上，并且您希望使其可用于其他 shell 自定义（例如，将其绑定到键），请应用此标志。 安装 VSPackage 后，用户可以通过打开 **"选项"** 对话框，然后在 **"键盘环境**"类别下编辑命令放置来自定义这些命令。 不影响在快捷菜单、工具栏、菜单控制器或子菜单上放置。

适用于： `Button`， ，`Combo`

`DefaultDisabled`默认情况下，如果未加载实现该命令的 VSPackage 或未调用 QueryStatus 方法，则禁用该命令。

适用于： `Button`， ，`Combo`

`DefaultInvisible`默认情况下，如果未加载实现该命令的 VSPackage 或未调用 QueryStatus 方法，则该命令不可见。

应与`DynamicVisibility`标志组合。

适用于： `Button`、 `Combo`、 、 、 、 、 、 、 、 、 、 、 、 、 、`Menu`

`DynamicVisibility`可以使用`QueryStatus``VisibilityConstraints`本节中包含的方法或上下文 GUID 更改命令的可见性。

应用于显示在菜单上的命令，不适用于工具栏上。 当从`OLECMDF_INVISIBLE``QueryStatus`方法返回标志时，可以禁用顶级工具栏项，但不能隐藏。

在菜单上，此标志还指示在其成员隐藏时应自动隐藏该标志。 此标志通常分配给子菜单，因为顶级菜单已具有此行为。

应与`DefaultInvisible`标志组合。

适用于： `Button`、 `Combo`、 、 、 、 、 、 、 、 、 、 、 、 、 、`Menu`

`NoShowOnMenuController`如果具有此标志的命令位于菜单控制器上，则该命令不会显示在下拉列表中。

有效期：`Button`

有关命令标志的详细信息，请参阅[CommandFlag 元素](../../extensibility/command-flag-element.md)文档。

#### <a name="general-requirements"></a>一般要求
在显示和启用命令之前，命令必须通过以下一系列测试：

- 该命令的位置正确。

- 未`DefaultInvisible`设置标志。

- 父菜单或工具栏可见。

- 由于["可见性约束"元素](../../extensibility/visibilityconstraints-element.md)部分中的上下文条目，该命令不不可见。

- 实现接口并启用命令的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>VSPackage 代码。 没有接口代码截获它并对其进行操作。

- 当用户单击命令时，它将受到[路由算法](../../extensibility/internals/command-routing-algorithm.md)中概述的过程的约束。

## <a name="call-pre-defined-commands"></a>调用预定义的命令
[使用命令元素](../../extensibility/usedcommands-element.md)使 VS 包能够访问其他 VS 包或 IDE 提供的命令。 为此，请创建一个[UseCommand 元素](../../extensibility/usedcommand-element.md)，该元素具有要使用的命令的 GUID 和 ID。 这可确保可视化工作室将加载该命令，即使该命令不是当前 Visual Studio 配置的一部分。 有关详细信息，请参阅[使用命令元素](../../extensibility/usedcommand-element.md)。

## <a name="interface-element-appearance"></a>接口元素外观
选择和定位命令元素的注意事项如下：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供了许多 UI 元素，这些元素的显示方式因位置而异。

- 使用`DefaultInvisible`标志定义的 UI 元素将不会显示在 IDE 中，除非它由<xref:EnvDTE.IDTCommandTarget.QueryStatus%2A>方法的 VSPackage 实现显示，或与`VisibilityConstraints`节中的特定 UI 上下文相关联。

- 即使无法显示成功定位的命令也可能不会显示。 这是因为 IDE 会自动隐藏或显示某些命令，具体取决于 VSPackage 已实现（或尚未）实现的接口。 例如，VSPackage 对某些生成接口的实现会导致自动显示与生成相关的菜单项。

- 在`CommandWellOnly`UI 元素的定义中应用标志意味着只能通过自定义来添加该命令。

- 命令可能仅在某些 UI 上下文中可用，例如，仅当 IDE 位于设计视图中时显示对话框时才可用。

- 要导致某些 UI 元素显示在 IDE 中，必须实现一个或多个接口或编写一些代码。

## <a name="see-also"></a>另请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
