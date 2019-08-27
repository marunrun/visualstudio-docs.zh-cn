---
title: 元素（XElement 动态属性）
ms.date: 11/04/2016
ms.topic: reference
apiname:
- XElement.Element
apitype: Assembly
ms.assetid: c6c25b8d-a1da-41ff-aeff-867ff1dcf749
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dbd197082174bcd23ab6b47d64eb4eb0f7944ca2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62845537"
---
# <a name="element-xelement-dynamic-property"></a>元素（XElement 动态属性）

获取一个索引器，用于检索与指定扩展名对应的子元素实例。

## <a name="syntax"></a>语法

```xaml
elem.Element[{namespaceName}localName]
```

## <a name="property-valuereturn-value"></a>属性值/返回值

一个类型为 `XElement Item(String expandedName)` 的索引器。 此索引器获取扩展名参数并返回相应的 <xref:System.Xml.Linq.XElement>，或者如果没有具有指定名称的元素，则返回 `null`。

## <a name="remarks"></a>备注

此属性等效于 <xref:System.Xml.Linq.XContainer.Element%2A> 类的 <xref:System.Xml.Linq.XContainer?displayProperty=fullName> 方法。

## <a name="see-also"></a>请参阅

- <xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName>
- [XElement 类动态属性](../designers/xelement-class-dynamic-properties.md)
- [元素](../designers/elements-xelement-dynamic-property.md)