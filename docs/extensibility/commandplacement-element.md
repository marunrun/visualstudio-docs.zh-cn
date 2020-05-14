---
title: 命令放置元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 2cbd7ac8-c55a-43d8-a26d-713b3d790016
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dcf9f23b5e860b895baa4c2a7a783f2ee15fcc77
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739744"
---
# <a name="commandplacement-element"></a>命令放置元素
"命令放置"元素允许按钮、组和菜单包含在多个组或菜单中。 通过使用 Command放置元素，您不必完全重新定义这些项目，以修改用户界面的外观。

 有关详细信息，请参阅[创建可重用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md)。

## <a name="syntax"></a>语法

```
<CommandPlacement guid="guidMyCommandSet" id="MyCommand" priority="0x001" >
  <Parent>... </Parent>
</CommandPlacement>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 命令集的 guid，如[符号元素](../extensibility/symbols-element.md)中定义的那样。|
|id|必需。 要放置的菜单、组或命令的 ID，如 中`Symbols Element`定义的那样。|
|priority|必需。 确定项在其父元素中的可视位置。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent|必需。 承载要放置的项的菜单或组。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[命令放置元素](../extensibility/commandplacements-element.md)|指定命令放置和命令放置元素的组。|

## <a name="example"></a>示例

```
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>请参阅
- [命令放置元素](../extensibility/commandplacements-element.md)
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
