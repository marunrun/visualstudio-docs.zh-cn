---
title: 特性（XElement 动态属性）
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 8440fc7d-b3b4-4726-8ec8-492e6af79642
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ec27fe2d7824ca32cbf97dbabac8b7ea6c4aed6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926918"
---
# <a name="attribute-xelement-dynamic-property"></a>特性（XElement 动态属性）

获取一个索引器，该索引器用于检索与指定扩展名对应的属性实例。

## <a name="syntax"></a>语法

```xaml
elem.Attribute[{namespaceName}attribName]
```

## <a name="property-valuereturn-value"></a>属性值/返回值

一个类型为 `XAttribute Item(String expandedName)` 的索引器。 此索引器获取指定属性的扩展名，然后返回相应的 <xref:System.Xml.Linq.XAttribute>，如果没有具有指定名称的属性，则返回 `null`。

## <a name="remarks"></a>备注

此属性等效于 <xref:System.Xml.Linq.XElement.Attribute%2A> 类的 <xref:System.Xml.Linq.XElement?displayProperty=fullName> 方法。

## <a name="see-also"></a>请参阅

- <xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName>
- [XElement 类动态属性](../designers/xelement-class-dynamic-properties.md)
- [值](../designers/value-xattribute-dynamic-property.md)