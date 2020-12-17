---
title: 菜单元素 |Microsoft Docs
description: 菜单元素定义 VSPackage 实现的所有菜单和工具栏。 本文包含一个示例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: d825a99b-e05c-4dd9-8933-a180216d667a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: abc5621784579c295393d77c792013dd0c737871
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97615572"
---
# <a name="menus-element"></a>菜单元素
定义 VSPackage 实现的所有菜单和工具栏。

## <a name="syntax"></a>语法

```xml
<Menus>
  <Menu>... </Menu>
  <Menu>... </Menu>
</Menus>
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
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单和工具栏。|
|[Menu 元素](../extensibility/menu-element.md)|表示单个菜单或工具栏。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 中命令的集合。|

## <a name="example"></a>示例

```xml
<Commands package="guidMyPackage">
    <Menus>
      <Menu Condition="'%(DEBUG)' != 'true'"
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"
        priority="0x0000" type="Menu">
        <Annotation>
          <Documentation>this is an annotation</Documentation>
          <AppInfo>
            <CustomData>
              <CustomSubElement>Some data</CustomSubElement>
            </CustomData>
          </AppInfo>
        </Annotation>
        <CommandFlag>AlwaysCreate</CommandFlag>
        <Strings>
          <ButtonText>MainMenu</ButtonText>
        </Strings>
      </Menu>
  </Menus>
<Commands>
```

## <a name="see-also"></a>另请参阅
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
