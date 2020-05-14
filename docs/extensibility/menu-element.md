---
title: 菜单元素 |微软文档
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
ms.openlocfilehash: 8dc4731f95e31781f6b10704d7cb14dc83e96d7a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702600"
---
# <a name="menu-element"></a>菜单元素
定义一个菜单项。 它们是六种菜单：上下文、菜单、菜单控制器、菜单控制器、工具栏和工具窗口工具栏。

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

|特性|描述|
|---------------|-----------------|
|guid|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|priority|可选。 指定菜单组中菜单的相对位置的数值。|
|工具栏优先级内带|可选。 在窗口停靠时指定工具栏在波段的相对位置的数值。|
|type|可选。 指定元素类型的枚举值。<br /><br /> 如果不存在，则默认类型为"菜单"。<br /><br /> 上下文<br /> 当用户右键单击窗口时显示的快捷菜单。 快捷菜单具有以下特征：<br /><br /> - 当菜单显示为快捷菜单时，不使用 **"父**"和 **"优先级**"字段。<br />- 可用作子菜单和快捷菜单。 在这种情况下，**受遵守组 ID**和**优先级**字段。<br />- 并非始终可用。<br /><br /> 仅当以下条件为 true 时，才会显示快捷菜单：<br /><br /> - 显示承载它的窗口。<br />- VSPackage 中的鼠标处理程序检测到右键单击窗口，然后调用处理该命令的方法。<br />- 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A>方法（建议的方法）或方法来<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>显示快捷菜单。<br /><br /> 菜单<br /> 提供下拉菜单。 下拉菜单具有以下特征：<br /><br /> - 在其定义中尊重父项。<br />- 必须具有父组或组的命令放置。<br />- 可以是任何其他种类的菜单中的子菜单。<br />- 每当显示其父菜单时，都会自动显示。<br />- 不需要实现任何 VSPackage 代码来使其显示。<br /><br /> 菜单控制器<br /> 提供拆分按钮下拉菜单，该菜单通常用于工具栏。 菜单控制器菜单具有以下特征：<br /><br /> - 必须通过父级或命令放置包含在其他菜单中。<br />- 在其定义中尊重父项。<br />- 可以有任何类型的菜单作为其父菜单。<br />- 只要显示其父菜单，将自动提供。<br />- 不需要编程支持来显示菜单。<br /><br /> 拆分按钮菜单中的命令将显示在菜单按钮上。 显示的命令具有以下特征之一：<br /><br /> - 如果该命令仍然显示并启用，则使用该命令的最后一个命令。<br />- 这是第一个显示的命令。<br /><br /> 菜单控制器锁定<br /> 提供拆分按钮下拉菜单，通过将命令标记为锁定，可以将命令指定为默认选择。<br /><br /> 锁定命令是一个命令，在菜单中标记为所选，通常通过显示复选标记。 如果命令在`QueryStatus`<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口方法的实现中设置了OLECMDF_LATCHED标志，则可以将其标记为锁定。 菜单控制器锁定菜单具有以下特征：<br /><br /> - 必须通过父组或命令放置包含在其他菜单中。<br />- 在其定义中尊重父项。<br />- 可以有任何类型的菜单作为其父菜单。<br />- 只要显示其父菜单，都可用。<br />- 不需要编程支持来显示菜单。<br /><br /> 拆分按钮菜单中的命令将显示在菜单按钮上。 显示的命令具有以下特征之一：<br /><br /> - 这是第一个显示的命令被锁定。<br />- 这是第一个显示的命令。<br /><br /> 工具栏<br /> 提供工具栏。 工具栏具有以下特征：<br /><br /> - 忽略父项的定义。<br />- 不能成为任何组的子菜单，甚至无法使用命令放置。<br />- 始终可以通过单击 **"视图"** 菜单上**的工具栏**显示。<br />- 可以使用[可见性项](../extensibility/visibilityitem-element.md)显示 。<br />- 不需要任何代码来创建它。 有关如何创建工具栏的示例，请参阅[添加工具栏](../extensibility/adding-a-toolbar.md)。<br /><br /> 工具窗口工具栏<br /> 提供附加到特定工具窗口的工具栏，就像工具栏附加到开发环境一样。<br /><br /> - 忽略父项的定义。<br />- 不能成为任何组的子菜单，甚至无法使用命令放置。<br />- 仅当显示承载工具栏的工具窗口和 VSPackage 显式将工具栏添加到工具窗口中时，才会显示。 这通常是通过从工具窗口框架获取工具栏主机属性（由<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost>接口表示）然后调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A>方法来创建工具窗口时完成的。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent|可选。 菜单项的父元素。|
|命令标志|必需。 请参阅[命令标志元素](../extensibility/command-flag-element.md)。 菜单的有效命令Flag值如下所示：<br /><br /> -   **始终创建**<br />-   **默认已装**<br />-   **默认不可见**- 此标志不会影响工具栏的显示。<br />-   **唐特卡奇**<br />-   **动态可见性**- 此标志不会影响工具栏的显示。<br />-   **图标和文本**<br />-   **无定制**<br />-   **NOTTBlist**<br />-   **无工具栏关闭**<br />-   **文本更改**<br />-   **文本 Isanchor 命令**|
|字符串|必需。 请参阅[字符串元素](../extensibility/strings-element.md)。 必须定义`ButtonText`子元素。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|

## <a name="example"></a>示例

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
    <CommandFlag>AlwaysCreate</CommandFlag>
    <Strings>
      <ButtonText>Edit Widget</ButtonText>
    </Strings>
    </Parent>
</Menu>
```

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
