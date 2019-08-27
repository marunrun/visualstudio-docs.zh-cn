---
title: CommandPlacements 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CommandPlacements
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 78a5724a-3b9f-4c78-9c0d-8faa3924f81c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb22359c936caacef81f4c9b81993a46d47ccc0b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341887"
---
# <a name="commandplacements-element"></a>CommandPlacements 元素
CommandPlacements 元素组 CommandPlacement 元素和其他 CommandPlacements 分组。

 CommandPlacements 元素是可选的。 如果没有命令、 组或菜单必须包含在辅助位置，不需要包含在此部分你 *.vsct*文件。

## <a name="syntax"></a>语法

```xml
<CommandPlacements>
  <CommandPlacement>... </CommandPlacement>
  <CommandPlacement>... </CommandPlacement>
</CommandPlacements>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|CommandPlacements|CommandPlacement 元素进行分组和其他 CommandPlacements 分组。|
|[CommandPlacement 元素](../extensibility/commandplacement-element.md)|启用要包含在多个组或菜单中的按钮、 组和菜单。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的所有元素。|

## <a name="example"></a>示例

```xml
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>请参阅
- [CommandPlacement 元素](../extensibility/commandplacement-element.md)
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)