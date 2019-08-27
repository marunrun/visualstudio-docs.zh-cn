---
title: Menu 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 79a8fafc748274015dac7f8f0938bba37ba5a8bc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194355"
---
# <a name="menu-element"></a>Menu 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义一个菜单项。 这些是菜单的六种：上下文、 菜单、 MenuController、 MenuControllerLatched、 工具栏和 ToolWindowToolbar。  
  
## <a name="syntax"></a>语法  
  
```  
<Menu guid=”guidMyCommandSet” id=”MyCommand” priority=”0x100” type=”button”>  
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
|guid|必需。 GUID ID 的命令标识符的 GUID。|  
|id|必需。 GUID ID 的命令标识符的 ID。|  
|priority|可选。 一个数字值，该值的菜单组中指定一个菜单的相对位置。|  
|ToolbarPriorityInBand|可选。 停靠窗口时带区在指定工具栏的相对位置的数字值。|  
|类型|可选。 一个枚举的值，指定的元素的类型。<br /><br /> 如果不存在，则默认类型是菜单。<br /><br /> 上下文<br /> 当用户右键单击一个窗口，显示快捷菜单。 快捷菜单包含以下特征：<br /><br /> -不使用父和优先级字段，以作为快捷方式菜单显示菜单时。<br />-可以使用子菜单，而且还为快捷方式菜单。 在这种情况下，会遵循组 ID 和优先级字段。<br />-不始终可用。<br /><br /> 仅当以下条件成立时，将显示一个快捷方式菜单：<br /><br /> 的将显示承载它窗口。<br />的在 VSPackage 中鼠标处理程序检测到的窗口上右键单击，然后调用的方法用于处理该命令。<br />-的快捷菜单，系统会通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A>方法 （建议） 或<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>方法。<br /><br /> 菜单<br /> 提供一个下拉列表菜单。 下拉列表菜单还拥有以下特征：<br /><br /> -会考虑在其定义中的父级。<br />-必须具有父组或 CommandPlacement 到组。<br />-可以是菜单的任何其他类型中的子菜单。<br />-会自动显示时显示其父菜单。<br />-不需要任何 VSPackage 的代码，使其显示的实现。<br /><br /> MenuController<br /> 提供了一个拆分按钮下拉列表菜单，其中通常使用工具栏中。 MenuController 菜单还拥有以下特征：<br /><br /> -必须包含在通过父或 CommandPlacement 的另一个菜单。<br />-会考虑在其定义中的父级。<br />-可以作为其父级具有任何类型的菜单。<br />-会自动成为可用时显示其父菜单。<br />-不需要编程支持，以使显示的菜单。<br /><br /> 拆分按钮菜单中的命令菜单按钮上显示。 该命令显示具有以下特征之一：<br /><br /> -它是如果仍显示和启用该命令使用的最后一个命令。<br />-它是第一个显示的命令。<br /><br /> MenuControllerLatched<br /> 提供了为其命令可以指定为默认选择通过将命令标记为锁定一个拆分按钮下拉列表菜单。<br /><br /> 锁定的命令是在标记为已选中的菜单通常通过显示复选标记的命令。 命令会被标记为闩锁是否 OLECMDF_LATCHED 标志上它的实现中的设置`QueryStatus`方法的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。 MenuControllerLatched 菜单还拥有以下特征：<br /><br /> -必须包含在父组或 CommandPlacement 通过另一个菜单。<br />-会考虑在其定义中的父级。<br />-可以作为其父级具有任何类型的菜单。<br />-是可显示其父菜单时的不同而不同。<br />-不需要编程支持，以使显示的菜单。<br /><br /> 拆分按钮菜单中的命令菜单按钮上显示。 该命令显示具有以下特征之一：<br /><br /> -它是第一个，则会显示的命令。<br />-它是第一个显示的命令。<br /><br /> Toolbar<br /> 提供一个工具栏。 工具栏具有以下特征：<br /><br /> -将忽略其定义中的父级。<br />-不能进行任何组的子菜单甚至不使用 CommandPlacement。<br />-始终可以通过单击显示**工具栏**上**视图**菜单。<br />-可以通过使用显示[VisibilityItem](../extensibility/visibilityitem-element.md)。<br />-不需要任何代码来创建它。 有关如何创建工具栏的示例，请参阅[将工具栏添加](../extensibility/adding-a-toolbar.md)。<br /><br /> ToolWindowToolbar<br /> 提供一个工具栏，它附加到特定的工具窗口，就像一个工具栏附加到开发环境。<br /><br /> -将忽略其定义中的父级。<br />-不能进行任何组的子菜单甚至不使用 CommandPlacement。<br />-仅时显示工具窗口承载工具栏的显示和 VSPackage 显式将工具栏添加到工具窗口。 这通常是通过获取 toolbar 主机属性创建工具窗口 (由<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost>接口) 从工具窗口框架并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A>方法。|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|父级|可选。 菜单项的父元素。|  
|CommandFlag|必需。 请参阅[命令标志元素](../extensibility/command-flag-element.md)。 菜单 CommandFlag 有效值如下所示：<br /><br /> -   **AlwaysCreate**<br />-   **DefaultDocked**<br />-   **DefaultInvisible** -此标志不会影响显示的工具栏。<br />-   **DontCache**<br />-   **DynamicVisibility** -此标志不会影响显示的工具栏。<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextChanges**<br />-   **TextIsAnchorCommand**|  
|字符串|必需。 请参阅[字符串元素](../extensibility/strings-element.md)。 子`ButtonText`必须定义元素。|  
|批注|可选注释。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|  
  
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
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)