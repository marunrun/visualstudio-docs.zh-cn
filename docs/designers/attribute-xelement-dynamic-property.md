---
title: 特性（XElement 动态属性）
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 8440fc7d-b3b4-4726-8ec8-492e6af79642
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0d7fc1aa0419863e933bdc0a828455fcda8671fc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72637396"
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
- [XElement 类动态属性](../designers/attribute-xelement-dynamic-property.md)
- [值](../designers/value-xattribute-dynamic-property.md)