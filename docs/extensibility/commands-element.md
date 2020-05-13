---
title: 命令元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3ea2400cca19a02475caecec3d022e0b78794ae4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739687"
---
# <a name="commands-element"></a>Commands 元素
表示 VSPackage 工具栏上的命令集合。 集合最多可以有五个子节，如下所示：菜单、组、按钮、组合和位图。

 每个子节子元素（例如，\<菜单>）都由一个唯一的命令 ID 标识，该 ID 是 GUID 和数字标识符对。 GUID 标识"命令集"，用于对逻辑相关命令进行分组。 VSPackage 应定义自己的命令集，以避免与其他 VSPackage 定义的命令指示号发生冲突。

## <a name="syntax"></a>语法

```xml
<Commands package="GuidMyPackage" >
  <Menus>... </Menus>
  <Groups>... </Groups>
  <Buttons>... </Buttons>
  <Combos>... </Combos>
  <Bitmaps>... </Bitmaps>
</Commands>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|包|标识提供命令的 VSPackage 的 GUID。<br /><br /> 例如，包="guidV 包1Pkg"。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|
|[组元素](../extensibility/groups-element.md)|包含在 VSPackage 中定义命令组的条目。|
|[按钮元素](../extensibility/buttons-element.md)|对按钮元素进行分组。|
|[位图元素](../extensibility/bitmaps-element.md)|对位图元素。|
|[组合元素](../extensibility/combos-element.md)|对组合元素进行分组。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[命令表元素](../extensibility/commandtable-element.md)|定义表示 VS 包向 IDE 提供的命令的所有元素。 可能的元素是菜单项、菜单、工具栏和组合框。|

## <a name="example"></a>示例
 下面的示例演示如何使用[命令元素](../extensibility/commands-element.md)。

```
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

## <a name="see-also"></a>请参阅
- [VS包如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
