---
title: Combos 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: ef48d2d2-0c47-4f93-8cfe-52026b6c463e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d005ea69aea7f0331877326abe4087fcff403553
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739800"
---
# <a name="combos-element"></a>Combos 元素
组 [组合元素](../extensibility/combo-element.md) 元素。

## <a name="syntax"></a>语法

```
<Combos>
  <Combo>... </Combo>
  <Combo>... </Combo>
</Combos>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[Combos 元素](../extensibility/combos-element.md)|组组合元素。|
|[组合元素](../extensibility/combo-element.md)|定义在组合框中显示的命令。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[命令元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上命令的集合。|

## <a name="example"></a>示例

```
<Combos>
  <Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
    defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">
    <CommandFlag>DynamicVisibility</CommandFlag>
    <Strings>
      <ButtonText>Select Insert Options</ButtonText>
    </Strings>
  </Combo>

  <Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0500" type="DropDownCombo" defaultWidth="100"
    idCommandList="cmdidGetInsertOptionsList">
    <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
    <CommandFlag>DynamicVisibility</CommandFlag>
    <Strings>
      <ButtonText>Select Insert Options</ButtonText>
    </Strings>
  </Combo>
</Combos>
```

## <a name="see-also"></a>另请参阅
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
