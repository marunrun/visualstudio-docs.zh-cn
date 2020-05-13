---
title: 可见性项目元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9129d64e430d661bbdd8f7682e64c93650570211
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698151"
---
# <a name="visibilityitem-element"></a>可见性项目元素
该`VisibilityItem`元素确定命令和工具栏的静态可见性。 每个条目标识命令或菜单，以及关联的命令 UI 上下文。 Visual Studio 检测命令、菜单和工具栏及其可见性，而无需加载定义它们的 VS 包。 IDE 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>方法确定命令 UI 上下文是否处于活动状态。

 加载 VSPackage 后，Visual Studio 希望命令可见性由 VSPackage 而不是 确定`VisibilityItem`。 要确定命令的可见性，可以实现<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>事件处理程序或<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法，具体取决于实现命令的方式。

 仅当关联的上下文处于活动状态时，才会`VisibilityItem`显示具有元素的命令或菜单。 通过为每个命令上下文组合包含一个条目，可以将单个命令、菜单或工具栏与一个或多个命令 UI 上下文相关联。 如果命令或菜单与多个命令 UI 上下文相关联，则当任何关联的命令 UI 上下文处于活动状态时，命令或菜单可见。

 该`VisibilityItem`元素仅适用于命令、菜单和工具栏，不适用于组。 每当其父菜单处于活动状态时，没有`VisibilityItem`相关元素的元素都会可见。

## <a name="syntax"></a>语法

```xml
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
|guid|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|上下文|必需。 命令可见的 UI 上下文。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[可见性约束元素](../extensibility/visibilityconstraints-element.md)|该`VisibilityConstraints`元素确定命令组和工具栏的静态可见性。|

## <a name="remarks"></a>备注
 标准可视化工作室 UI 上下文在 Visual *Studio SDK 安装路径*[VisualStudio 集成]公共_Inc_vsshlids.h 文件中以及<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids><xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>和 类中定义。 <xref:Microsoft.VisualStudio.VSConstants>类中定义了一组更完整的 UI 上下文。

## <a name="example"></a>示例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [可见性约束元素](../extensibility/visibilityconstraints-element.md)
- [可视化工作室命令表 （.Vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
