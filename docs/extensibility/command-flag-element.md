---
title: 命令标志元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 84138a69dbb42fc349c12276fd7cca4b593e4d47
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "81649367"
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

|值|说明|
|-----------|-----------------|
|AllowParams|指示当用户键入命令的规范名称时，可以在 **命令** 窗口中输入命令参数。<br /><br /> 适用于： `Button`|
|AlwaysCreate|即使没有组或按钮，也会创建菜单。<br /><br /> 适用于： `Menu`|
|CaseSensitive|用户项区分大小写。<br /><br /> 适用于： `Combo`|
|CommandWellOnly|如果命令未显示在顶级菜单上，并且您要使其可用于其他 shell 自定义（例如，将其绑定到键盘快捷方式），则应用此标志。 安装 VSPackage 后，可以通过打开 " **选项** " 对话框，然后在 " **键盘环境** " 类别下编辑命令位置来自定义这些命令。 此标志不影响快捷菜单、工具栏、菜单控制器或子菜单上的位置。<br /><br /> 适用于： `Button` 、 `Combo`|
|DefaultDisabled|默认情况下，如果未加载实现该命令的 VSPackage 或未调用方法，则该命令处于禁用状态 `QueryStatus` 。<br /><br /> 适用于： `Button` 、 `Combo`|
|DefaultDocked|默认停靠。 此设置不再适用于工具栏，因为它们始终停靠在一起。|
|DefaultInvisible|默认情况下，如果未加载实现该命令的 VSPackage 或未调用方法，则该命令将不可见 `QueryStatus` 。<br /><br /> 建议将此与标志结合起来 `DynamicVisibility` 。<br /><br /> 适用于： `Button` 、 `Combo` 、 `Menu`|
|DontCache|开发环境不会缓存 `QueryStatus` 此命令的方法结果。<br /><br /> 对于菜单，此选项指示菜单控制器不缓存其菜单项的文本。 当菜单包含动态项或具有动态文本的项时，请使用此标志。<br /><br /> 适用于： `Button` 、 `Menu`|
|DynamicItemStart|指示动态列表的开头。 这样，环境就可以通过依次对列表项调用方法来生成列表， `QueryStatus` 直到返回 OLECMDERR_E_UNSUPPORTED 标志。 这非常适用于最常用的项 (MRU) 列表和窗口列表。<br /><br /> 适用于： `Button`|
|DynamicVisibility|可以通过 `QueryStatus` 方法或部分中包含的上下文 GUID 来更改命令的可见性 `VisibilityConstraints` 。<br /><br /> 适用于出现在菜单和工具窗口工具栏上的命令，而不是出现在主窗口中的顶级工具栏上的命令。 当从方法返回 OLECMDF_INVISIBLE 标志时，可以禁用但不隐藏顶级工具栏项 `QueryStatus` 。 可以隐藏工具窗口工具栏上显示的工具栏命令。<br /><br /> 在菜单上，此标志还指示在隐藏其所有成员时，它应自动隐藏。 此标志通常分配给子菜单，因为顶级菜单已经有了此行为。<br /><br /> 此标志应与 `DefaultInvisible` 标志结合。<br /><br /> 适用于： `Button` 、 `Combo` 、 `Menu`|
|键|请参阅 " [组合元素](../extensibility/combo-element.md)" 下的筛选键主题。<br /><br /> 适用于： `Combo`|
|FixMenuController|如果此命令位于菜单控制器上，则该命令始终为默认值;也就是说，只要选择了菜单控制器按钮，就会选择该命令。 如果菜单控制器 `TextIsAnchorCommand` 设置了标志，则菜单控制器还会从具有标志的命令获取其文本 `FixMenuController` 。<br /><br /> 菜单控制器上只有一个命令应具有 `FixMenuController` 标志。 如果有多个命令被标记为，则菜单中的最后一个命令将成为默认命令。<br /><br /> 适用于： `Button`|
|IconAndText|在菜单和工具栏上显示图标和文本。<br /><br /> 适用于： `Button` 、 `Combo` 、 `Menu`|
|NoAutoComplete|已禁用自动完成功能。<br /><br /> 适用于： `Combo`|
|NoButtonCustomize|不要让用户自定义此按钮。<br /><br /> 适用于： `Button` 、 `Combo`|
|NoKeyCustomize|不要启用键盘自定义。<br /><br /> 适用于： `Button` 、 `Combo`|
|NoShowOnMenuController|如果此命令位于菜单控制器上，则该命令不会出现在下拉列表中。<br /><br /> 适用于： `Button`|
|NotInTBList|在可用工具栏列表中不显示。 这仅对工具栏菜单类型有效。<br /><br /> 适用于： `Menu`|
|NoToolbarClose|用户无法关闭工具栏。 这仅对工具栏菜单类型有效。<br /><br /> 适用于： `Menu`|
|图像|只显示工具栏上的图标，而只显示菜单上的文本。 如果未指定图标，则会在工具栏上显示可单击的空白区域。<br /><br /> 适用于： `Button`|
|PostExec|使命令非阻止。 开发环境将延迟执行，直到处理完所有预处理查询。<br /><br /> 适用于： `Button`|
|RouteToDocs|将命令路由到活动文档。<br /><br /> 适用于： `Button`|
|StretchHorizontally|设置此标志后，宽度将变为组合框的最小宽度，如果工具栏上有空间，则组合框会拉伸以填充可用空间。 这种情况仅在工具栏水平停靠时才会发生，而工具栏上只有一个组合框可以使用标志 (除了第一个组合框外，) 忽略标志。<br /><br /> 适用于： `Combo`|
|TextChanges|命令或菜单文本可在运行时通过方法进行更改 `QueryStatus` 。<br /><br /> 适用于： `Button` 、 `Menu`|
|TextChangesButton|适用于： `Button`|
|TextIsAnchorCommand|对于菜单控制器，菜单文本是从默认 (定位点) 命令获取的。 定位符命令是最后一个选定或锁定的命令。 如果未设置此标志，则菜单控制器使用其自己的 `MenuText` 字段。 然而，单击菜单控制器仍将从该控制器启用最后一个选定的命令。<br /><br /> 建议将此标志与标志结合起来 `TextChanges` 。<br /><br /> 此标志仅适用于 MenuController 或 MenuControllerLatched 类型的菜单。<br /><br /> 适用于： `Menu`|
|TextMenuCtrlUseMenu|使用 `MenuText` 菜单控制器上的字段。 默认字段是 `ButtonText` 。<br /><br /> 适用于： `Button`|
|TextMenuUseButton|将 `ButtonText` 字段用于菜单。 如果已指定，则默认值为 `MenuText` 。<br /><br /> 适用于： `Button`|
|TextOnly|仅显示工具栏或菜单上的文本，但不显示图标（即使指定了图标）。<br /><br /> 适用于： `Button`|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[按钮元素](../extensibility/buttons-element.md)|为 [Button 元素](../extensibility/button-element.md) 元素提供组。|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表 (。.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
