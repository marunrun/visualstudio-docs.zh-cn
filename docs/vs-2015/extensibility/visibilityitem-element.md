---
title: VisibilityItem 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f6f71e145282d1d6e340060b9798ca54c9af9f4e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62584832"
---
# <a name="visibilityitem-element"></a>VisibilityItem 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`VisibilityItem`元素可确定命令和工具栏的静态可见性。 每个条目标识命令或菜单中，以及关联的命令 UI 上下文。 Visual Studio 检测命令、 菜单和工具栏和其可见性，而不加载 Vspackage 的定义它们。 IDE 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>方法来确定命令 UI 上下文是否处于活动状态。  
  
 VSPackage 加载后，Visual Studio 期望命令可见性由 VSPackage 而不是`VisibilityItem`。 若要确定命令的可见性，您可以实现<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>事件处理程序或<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法，具体取决于您的命令的实现方式。  
  
 命令或具有菜单`VisibilityItem`元素将显示仅当关联的上下文处于活动状态时。 可以包括每个命令上下文组合的条目，将单个命令、 菜单或工具栏关联具有一个或多个命令 UI 上下文。 与多个命令 UI 上下文关联的命令或菜单时，然后命令或菜单可见时关联的命令 UI 上下文中的任何一个处于活动状态。  
  
 `VisibilityItem`元素仅适用于命令、 菜单和工具栏，不到组。 不具有相关的元素`VisibilityItem`元素是否可见的只要其父菜单处于活动状态。  
  
## <a name="syntax"></a>语法  
  
```  
<VisibilityItem  
  guid ="="cmdGuidMyProductCommands"  
  id=="cmdidAddWidget"  
  context="guidNotViewSourceMode"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|guid|必需。 GUID ID 的命令标识符的 GUID。|  
|id|必需。 GUID ID 的命令标识符的 ID。|  
|Context — 上下文|必需。 该命令处于可见 UI 上下文。|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
 None  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)|`VisibilityConstraints`元素可确定组的命令和工具栏的静态可见性。|  
  
## <a name="remarks"></a>备注  
 在中定义的标准的 Visual Studio UI 上下文*Visual Studio SDK 安装路径*\VisualStudioIntegration\Common\Inc\vsshlids.h 中的文件以及作为<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>和<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>类。 中定义一组更完整的 UI 上下文<xref:Microsoft.VisualStudio.VSConstants>类。  
  
## <a name="example"></a>示例  
  
```  
<VisibilityConstraints>  
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"  
    context="guidNotViewSourceMode"/>  
</VisibilityConstraints>  
```  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>   
 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>   
 <xref:Microsoft.VisualStudio.VSConstants>   
 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>   
 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>   
 [VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
