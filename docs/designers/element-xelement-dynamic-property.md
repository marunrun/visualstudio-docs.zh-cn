---
title: 元素（XElement 动态属性）
ms.date: 11/04/2016
ms.topic: reference
apiname:
- XElement.Element
apitype: Assembly
ms.assetid: c6c25b8d-a1da-41ff-aeff-867ff1dcf749
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 08b2f7f008c1522c5f65b5ee7a58c3ed98e8a845
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72637328"
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
- [XElement 类动态属性](../designers/attribute-xelement-dynamic-property.md)
- [元素](../designers/elements-xelement-dynamic-property.md)