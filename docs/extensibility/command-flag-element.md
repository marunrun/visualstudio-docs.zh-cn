---
title: 命令标志元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a38708d6256556693b7ab1dfc8c04b79f484ee8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334842"
---
# <a name="command-flag-eelement"></a>命令标志 Eelement
修改其父元素。

## <a name="syntax"></a>语法

```
<CommandFlag>DynamicVisibility</CommandFlag>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下部分介绍了有效的元素值。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|值|描述|
|-----------|-----------------|
|AllowParams|指示用户可以输入中的命令参数**命令**窗口中键入该命令的规范名称时。<br /><br /> 适用于： `Button`|
|AlwaysCreate|即使它具有任何组或按钮创建菜单。<br /><br /> 适用于： `Menu`|
|CaseSensitive|用户项是区分大小写。<br /><br /> 适用于： `Combo`|
|CommandWellOnly|如果命令没有出现在顶级菜单上，并且你想要使其可供其他外壳自定义设置，例如，对于绑定到的键盘快捷方式，应用此标志。 VSPackage 安装后，你可以自定义这些命令打开**选项**对话框，然后编辑下的命令放置**键盘环境**类别。 此标志不会影响在快捷菜单、 工具栏、 菜单控制器或子菜单上的位置。<br /><br /> 对有效： `Button`， `Combo`|
|DefaultDisabled|默认情况下，如果未加载 VSPackage 实现该命令将禁用或`QueryStatus`尚未调用方法。<br /><br /> 对有效： `Button`， `Combo`|
|DefaultDocked|默认情况下停靠。 此设置不再适用于工具栏，因为它们始终停靠。|
|DefaultInvisible|默认情况下，该命令是不可见，如果未加载 VSPackage 实现它或`QueryStatus`尚未调用方法。<br /><br /> 我们建议将此与结合`DynamicVisibility`标志。<br /><br /> 对有效： `Button`， `Combo`， `Menu`|
|DontCache|在开发环境不会缓存`QueryStatus`方法此命令的结果。<br /><br /> 对于菜单，这将告知菜单控制器不来缓存其菜单项的文本。 当菜单包含动态项或项具有动态文本时，请使用此标志。<br /><br /> 对有效： `Button`， `Menu`|
|DynamicItemStart|指示动态列表的开头。 这使环境来通过连续调用生成的列表`QueryStatus`直到返回 OLECMDERR_E_UNSUPPORTED 标志的列表项上的方法。 这适用于项如最近使用 (过的 MRU) 列表和窗口列表。<br /><br /> 适用于： `Button`|
|DynamicVisibility|可以通过更改该命令的可见性`QueryStatus`方法或通过上下文中包含的 GUID`VisibilityConstraints`部分。<br /><br /> 适用于显示菜单和工具窗口工具栏上，但不是显示在主窗口的顶级工具栏上的命令。 顶级工具栏项可以禁用，但没有隐藏，请从返回 OLECMDF_INVISIBLE 标志时`QueryStatus`方法。 可以隐藏工具窗口工具栏显示的工具栏命令。<br /><br /> 在菜单上，此标志还指示，它应自动隐藏时隐藏所有其成员。 此标志通常分配给子菜单因为顶级菜单已有此行为。<br /><br /> 此标志应结合`DefaultInvisible`标志。<br /><br /> 对有效： `Button`， `Combo`， `Menu`|
|FilterKeys|请参阅下的筛选键主题[组合元素](../extensibility/combo-element.md)。<br /><br /> 适用于： `Combo`|
|FixMenuController|如果此命令置于菜单控制器，该命令始终是默认设置;也就是说，选择该命令时选择的菜单控制器按钮本身时。 如果菜单控制器`TextIsAnchorCommand`标志设置，则菜单控制器还会有该命令从其文本`FixMenuController`标志。<br /><br /> 菜单控制器上的只有一个命令应具有`FixMenuController`标志。 如果因此标记多个命令，在菜单中的最后一个命令将成为默认命令。<br /><br /> 适用于： `Button`|
|IconAndText|在菜单和工具栏上显示的图标和文本。<br /><br /> 对有效： `Button`， `Combo`， `Menu`|
|NoAutoComplete|禁用自动完成功能。<br /><br /> 适用于： `Combo`|
|NoButtonCustomize|不要让用户可以自定义此按钮。<br /><br /> 对有效： `Button`， `Combo`|
|NoKeyCustomize|不要启用键盘自定义。<br /><br /> 对有效： `Button`， `Combo`|
|NoShowOnMenuController|如果此命令置于菜单控制器，下拉列表中未显示命令。<br /><br /> 适用于： `Button`|
|NotInTBList|中没有可用的工具栏的列表。 这是仅对工具栏菜单类型有效。<br /><br /> 适用于： `Menu`|
|NoToolbarClose|用户不能关闭工具栏。 这是仅对工具栏菜单类型有效。<br /><br /> 适用于： `Menu`|
|pict|显示仅一个图标，在工具栏中，但仅在菜单上的文本。 如果指定无图标，则在工具栏上显示可单击空白区域。<br /><br /> 适用于： `Button`|
|PostExec|使命令非阻塞。 开发环境将延迟执行，直到完成前处理的所有查询。<br /><br /> 适用于： `Button`|
|RouteToDocs|该命令将路由到活动文档。<br /><br /> 适用于： `Button`|
|StretchHorizontally|设置此标志，宽度将成为最小宽度的组合框中，并且如果在工具栏上的空间，组合框拉伸以填充可用空间。 仅当水平停靠工具栏，并在工具栏上的只有一个组合框可以在使用的标志 （在所有除第一个组合框忽略该标志），将发生这种情况。<br /><br /> 适用于： `Combo`|
|TextMenuUseButton|使用`ButtonText`菜单的字段。 默认字段是`MenuText`如果指定它。<br /><br /> 适用于： `Button`|
|TextChanges|命令或菜单文本可以在运行时，通常通过更改`QueryStatus`方法。<br /><br /> 对有效： `Button`， `Menu`|
|TextChangesButton|适用于： `Button`|
|TextIsAnchorCommand|对于菜单控制器，菜单上的文本来自默认 （定位点） 命令。 一个定位点命令，选择或闩锁的最后一个命令。 如果未设置此标志，菜单控制器将使用其自己`MenuText`字段。 但是，单击菜单控制器仍可以启用该控制器中的最后一个所选的命令。<br /><br /> 我们建议结合使用此标志`TextChanges`标志。<br /><br /> 此标志仅适用于类型的菜单 MenuController 或 MenuControllerLatched。<br /><br /> 适用于： `Menu`|
|TextMenuCtrlUseMenu|使用`MenuText`菜单控制器上的字段。 默认字段是`ButtonText`。<br /><br /> 适用于： `Button`|
|TextMenuUseButton|使用`ButtonText`菜单的字段。 默认字段是`MenuText`如果指定它。<br /><br /> 适用于： `Button`|
|TextOnly|在工具栏或菜单，但没有图标上显示纯文本，即使指定图标。<br /><br /> 适用于： `Button`|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Buttons 元素](../extensibility/buttons-element.md)|提供的组[Button 元素](../extensibility/button-element.md)元素。|
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)