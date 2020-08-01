---
title: Menu 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 020098a3026f600629b8ab186431a1d2d5d7795a
ms.sourcegitcommit: b8ec700fc4c14c68c6ce280f29c19870261990d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87453662"
---
# <a name="menu-element"></a>Menu 元素
定义一个菜单项。 以下是六种类型的菜单： Context、Menu、MenuController、MenuControllerLatched、Toolbar 和 ToolWindowToolbar。

## <a name="syntax"></a>语法

```xml
<Menu guid="guidMyCommandSet" id="MyCommand" priority="0x100" type="button">
  <Parent>... </Parent>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Menu>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|priority|可选。 一个数字值，该值指定菜单在一组菜单中的相对位置。|
|ToolbarPriorityInBand|可选。 一个数值，该数值指定工具栏在停靠窗口时的相对位置。|
|type|可选。 指定元素类型的枚举值。<br /><br /> 如果不存在，则默认类型为 Menu。<br /><br /> 上下文<br /> 用户右键单击窗口时显示的快捷菜单。 快捷菜单具有以下特征：<br /><br /> -当菜单显示为快捷菜单时，不使用 "**父**" 和 "**优先级**" 字段。<br />-可用作子菜单和快捷菜单。 在这种情况下，将同时考虑**组 ID**和**优先级**字段。<br />-并非始终可用。<br /><br /> 仅当满足以下条件时，才会显示快捷菜单：<br /><br /> -显示承载它的窗口。<br />-VSPackage 中的鼠标处理程序检测到在窗口上单击右键，然后调用处理命令的方法。<br />-通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A> 方法（建议的方法）或方法来显示快捷菜单 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> 。<br /><br /> 菜单<br /> 提供一个下拉菜单。 下拉菜单具有以下特征：<br /><br /> -在其定义中遵守父项。<br />-必须具有父组，或组的 CommandPlacement。<br />-可以是任何其他类型的菜单中的子菜单。<br />-每当显示其父菜单时，自动显示。<br />-不需要任何 VSPackage 代码的实现来显示。<br /><br /> MenuController<br /> 提供一个拆分按钮下拉菜单，该菜单通常用于工具栏中。 MenuController 菜单具有以下特征：<br /><br /> -必须通过 Parent 或 CommandPlacement 包含在另一个菜单中。<br />-在其定义中遵守父项。<br />-可将任何类型的菜单作为其父项。<br />-在其父菜单显示时自动变为可用。<br />-无需编程支持即可显示菜单。<br /><br /> 菜单按钮上将显示一个来自拆分按钮菜单的命令。 显示的命令具有以下特征之一：<br /><br /> -如果仍显示并启用该命令，则该命令为最后使用的命令。<br />-它是显示的第一个命令。<br /><br /> MenuControllerLatched<br /> 提供一个拆分按钮下拉菜单，可通过将命令标记为锁定来将命令指定为默认选择。<br /><br /> 锁定命令是在菜单中标记为选中状态的命令，通常通过显示复选标记。 如果命令在接口的方法的实现中为其设置了 OLECMDF_LATCHED 标志，则可以将其标记为锁定 `QueryStatus` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。 MenuControllerLatched 菜单具有以下特征：<br /><br /> -必须包含在通过父组或 CommandPlacement 的其他菜单中。<br />-在其定义中遵守父项。<br />-可将任何类型的菜单作为其父项。<br />-在显示其父菜单时，将变为可用。<br />-无需编程支持即可显示菜单。<br /><br /> 菜单按钮上将显示一个来自拆分按钮菜单的命令。 显示的命令具有以下特征之一：<br /><br /> -它是锁定的第一个显示命令。<br />-它是显示的第一个命令。<br /><br /> 工具栏<br /> 提供工具栏。 工具栏具有以下特征：<br /><br /> -忽略其定义中的父级。<br />-不能成为任何组的子菜单，甚至不能使用 CommandPlacement。<br />-始终可以通过单击 "**视图**" 菜单上的 "**工具栏**" 来显示。<br />-可以使用[VisibilityItem](../extensibility/visibilityitem-element.md)来显示。<br />-无需任何代码即可创建。 有关如何创建工具栏的示例，请参阅[添加工具栏](../extensibility/adding-a-toolbar.md)。<br /><br /> ToolWindowToolbar<br /> 提供附加到特定工具窗口的工具栏，就像将工具栏附加到开发环境一样。<br /><br /> -忽略其定义中的父级。<br />-不能成为任何组的子菜单，甚至不能使用 CommandPlacement。<br />-仅当显示承载工具栏的工具窗口并且 VSPackage 将工具栏显式添加到工具窗口时才显示。 这通常是在创建工具窗口时，通过从工具窗口框架获取工具栏主机属性（由 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> 接口表示），然后调用方法来完成的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> 。|
|条件|可选。 请参阅[条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent|可选。 菜单项的父元素。|
|CommandFlag|必需。 请参阅[命令标志元素](../extensibility/command-flag-element.md)。 菜单的有效 CommandFlag 值如下所示：<br /><br /> -   **AlwaysCreate**<br />-   **DefaultDocked**<br />-   **DefaultInvisible** -此标志不会影响工具栏的显示。<br />-   **DontCache**<br />-   **DynamicVisibility** -此标志不会影响工具栏的显示。<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextChanges**<br />-   **TextIsAnchorCommand**|
|字符串|必需。 请参阅[字符串元素](../extensibility/strings-element.md)。 `ButtonText`必须定义子元素。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|

## <a name="example"></a>示例

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit"/>
  <CommandFlag>AlwaysCreate</CommandFlag>
  <Strings>
    <ButtonText>Edit Widget</ButtonText>
  </Strings>
</Menu>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表（.vsct）文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
