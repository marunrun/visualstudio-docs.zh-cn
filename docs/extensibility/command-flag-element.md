---
title: 命令标志元素 |微软文档
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
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649367"
---
# <a name="command-flag-eelement"></a>命令标志 Eelement
修改其父元素。

## <a name="syntax"></a>语法

```
<CommandFlag>DynamicVisibility</CommandFlag>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下部分介绍有效的元素值。

### <a name="attributes"></a>属性
 无。

### <a name="child-elements"></a>子元素

|“值”|说明|
|-----------|-----------------|
|允许帕姆斯|指示用户可以在**命令窗口中输入**命令参数，当他们键入命令的规范名称时。<br /><br /> 有效期：`Button`|
|始终创建|即使菜单没有组或按钮，也会创建菜单。<br /><br /> 有效期：`Menu`|
|CaseSensitive|用户条目区分大小写。<br /><br /> 有效期：`Combo`|
|命令井只|如果命令未显示在顶级菜单上，并且您希望使其可用于其他 shell 自定义（例如，将其绑定到键盘快捷方式），请应用此标志。 安装 VSPackage 后，可以通过打开 **"选项"** 对话框，然后在 **"键盘环境**"类别下编辑命令放置来自定义这些命令。 此标志不会影响在快捷菜单、工具栏、菜单控制器或子菜单上的位置。<br /><br /> 适用于： `Button`， ，`Combo`|
|默认禁用|默认情况下，如果未加载实现该命令的 VSPackage 或未调用该方法，`QueryStatus`则禁用该命令。<br /><br /> 适用于： `Button`， ，`Combo`|
|默认已装|默认情况下停靠。 此设置不再适用于工具栏，因为它们始终停靠。|
|默认不可见|默认情况下，如果未加载实现该命令的 VSPackage 或未调用该方法，`QueryStatus`则该命令不可见。<br /><br /> 我们建议您将此与`DynamicVisibility`标志合并。<br /><br /> 适用于： `Button`、 `Combo`、 、 、 、 、 、 、 、 、 、 、 、 、 、`Menu`|
|唐特卡奇|开发环境不会缓存此命令`QueryStatus`的方法结果。<br /><br /> 对于菜单，这告诉菜单控制器不要缓存其菜单项的文本。 当菜单包含动态项或具有动态文本的项时，使用此标志。<br /><br /> 适用于： `Button`， ，`Menu`|
|动态项目启动|指示动态列表的开头。 这使环境能够生成列表，方法是在返回OLECMDERR_E_UNSUPPORTED标志之前`QueryStatus`在列表项上连续调用该方法。 这适用于最近使用 （MRU） 列表和窗口列表等项。<br /><br /> 有效期：`Button`|
|动态可见性|命令的可见性可以通过`QueryStatus`方法或通过`VisibilityConstraints`本节中包含的上下文 GUID 进行更改。<br /><br /> 应用于显示在菜单和工具窗口工具栏上的命令，但不适用于显示在主窗口中的顶级工具栏。 当从`QueryStatus`方法返回OLECMDF_INVISIBLE标志时，可以禁用但无法隐藏顶级工具栏项。 可以隐藏出现在工具窗口工具栏上的工具栏命令。<br /><br /> 在菜单上，此标志还指示在隐藏所有成员时自动隐藏它。 此标志通常分配给子菜单，因为顶级菜单已具有此行为。<br /><br /> 此标志应与`DefaultInvisible`标志组合。<br /><br /> 适用于： `Button`、 `Combo`、 、 、 、 、 、 、 、 、 、 、 、 、 、`Menu`|
|筛选器键|请参阅[组合元素](../extensibility/combo-element.md)下的筛选键主题。<br /><br /> 有效期：`Combo`|
|修复菜单控制器|如果此命令位于菜单控制器上，则该命令始终为默认值;如果此命令位于菜单控制器上，则该命令始终为默认命令。也就是说，每当选择菜单控制器按钮本身时，都会选择该命令。 如果菜单控制器设置了`TextIsAnchorCommand`标志，则菜单控制器也会从具有`FixMenuController`标志的命令中获取其文本。<br /><br /> 菜单控制器上只有一个命令应具有标志`FixMenuController`。 如果多个命令被如此标记，则菜单中的最后一个命令将成为默认命令。<br /><br /> 有效期：`Button`|
|图标和文本|在菜单和工具栏上显示图标和文本。<br /><br /> 适用于： `Button`、 `Combo`、 、 、 、 、 、 、 、 、 、 、 、 、 、`Menu`|
|无自动完成|自动完成功能已禁用。<br /><br /> 有效期：`Combo`|
|无按钮定制|不要让用户自定义此按钮。<br /><br /> 适用于： `Button`， ，`Combo`|
|NoKey 定制|不要启用键盘自定义。<br /><br /> 适用于： `Button`， ，`Combo`|
|诺秀翁菜单控制器|如果此命令位于菜单控制器上，则该命令不会显示在下拉列表中。<br /><br /> 有效期：`Button`|
|NOTTBlist|不显示在可用工具栏列表中。 这仅适用于工具栏菜单类型。<br /><br /> 有效期：`Menu`|
|无工具栏关闭|用户无法关闭工具栏。 这仅适用于工具栏菜单类型。<br /><br /> 有效期：`Menu`|
|皮克特|仅显示工具栏上的图标，但仅显示菜单上的文本。 如果未指定图标，请在工具栏上显示可单击的空白。<br /><br /> 有效期：`Button`|
|PostExec|使命令不阻塞。 开发环境将延迟执行，直到完成所有预处理查询。<br /><br /> 有效期：`Button`|
|路由到文档|该命令路由到活动文档。<br /><br /> 有效期：`Button`|
|水平拉伸|设置此标志时，宽度将成为组合框的最小宽度，如果工具栏上有空间，组合框将拉伸以填充可用空间。 仅当工具栏水平停靠时，并且工具栏上只有一个组合框可以使用标志（除第一个组合框外，所有组合框上都忽略该标志），才会发生这种情况。<br /><br /> 有效期：`Combo`|
|文本更改|命令或菜单文本可以在运行时更改，通常通过 方法`QueryStatus`。<br /><br /> 适用于： `Button`， ，`Menu`|
|文本更改按钮|有效期：`Button`|
|文本 Isanchor 命令|对于菜单控制器，菜单的文本取自默认（锚点）命令。 锚点命令是选择或锁定的最后一个命令。 如果未设置此标志，菜单控制器将使用其自己的`MenuText`字段。 但是，单击菜单控制器仍启用该控制器的最后一个选定命令。<br /><br /> 我们建议您将此标志与`TextChanges`标志合并。<br /><br /> 此标志仅适用于类型菜单控制器或菜单控制器锁定的菜单。<br /><br /> 有效期：`Menu`|
|文本菜单Ctrluse菜单|使用菜单`MenuText`控制器上的字段。 默认字段为`ButtonText`。<br /><br /> 有效期：`Button`|
|文本菜单使用按钮|对`ButtonText`菜单使用该字段。 默认字段是`MenuText`指定字段。<br /><br /> 有效期：`Button`|
|仅文本|仅在工具栏或菜单上显示文本，但即使指定了图标，也没有图标。<br /><br /> 有效期：`Button`|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[按钮元素](../extensibility/buttons-element.md)|为 Button[元素元素](../extensibility/button-element.md)提供组。|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|

## <a name="see-also"></a>另请参阅
- [可视化工作室命令表 （.Vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
