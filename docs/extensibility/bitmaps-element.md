---
title: Bitmaps 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: 74652e1b-fcfa-421b-aa9f-fbc081d3b476
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00486f4edd68d2cc5e158d567a28f78ef12f8cd1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333403"
---
# <a name="bitmaps-element"></a>Bitmaps 元素
组[位图元素](../extensibility/bitmap-element.md)元素。

## <a name="syntax"></a>语法

```
<Bitmaps>
  <Bitmap>... </Bitmap>
  <Bitmap>... </Bitmap>
</Bitmaps>
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
|[Bitmaps 元素](../extensibility/bitmaps-element.md)|位图元素进行分组。|
|[Bitmap 元素](../extensibility/bitmap-element.md)|定义位图。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上的命令的集合。|

## <a name="example"></a>示例

```
<Bitmaps>
  <Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
  <Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
    usedList="1, 2, 3, 4"/>
</Bitmaps>
```

## <a name="see-also"></a>请参阅
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)