---
title: 按钮元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 9f2cf94d-dec5-4776-a836-9a89c75f0c87
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2150ec240880987bc63bb3c2adf33682ebf34580
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321165"
---
# <a name="buttons-element"></a>Buttons 元素
组[按钮](../extensibility/button-element.md)元素，它表示单个命令。

## <a name="syntax"></a>语法

```
<Buttons>
  <Button>... </Button>
  <Button>... </Button>
</Buttons>
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
|[Buttons 元素](../extensibility/buttons-element.md)|按钮元素进行分组。|
|[Button 元素](../extensibility/button-element.md)|定义用户可与之交互的命令。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上的命令的集合。|

## <a name="example"></a>示例

```
<Buttons>
  <Button guid="guidMenuAndCommandsCmdSet" id="cmdidMyCommand"     priority="0x100" type="Button">
    <Parent guid="guidMenuAndCommandsCmdSet" id="MyMenuGroup"/>
    <Icon guid="guidGenericCmdBmp" id="bmpArrow"/>
    <Strings>
      <ButtonText>C# Command Sample</ButtonText>
    </Strings>
  </Button>
</Buttons>
```

## <a name="see-also"></a>请参阅
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)