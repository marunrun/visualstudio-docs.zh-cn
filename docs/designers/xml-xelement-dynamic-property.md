---
title: Xml（XElement 动态属性）
ms.date: 11/04/2016
ms.topic: reference
apiname:
- XElement.Xml
ms.assetid: 69ab2a33-4fe7-4cfa-97f8-eaf063decb18
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c93aaf3b43a930fe88020738460ec131972a205a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72633526"
---
# <a name="xml-xelement-dynamic-property"></a>Xml（XElement 动态属性）

获取元素的非格式化 XML 内容。

## <a name="syntax"></a>语法

```xaml
elem.Xml
```

## <a name="property-valuereturn-value"></a>属性值/返回值

表示元素的非格式化 XML 内容的 <xref:System.String>。

## <a name="remarks"></a>备注

此属性等效于 <xref:System.Xml.Linq.XNode.ToString(System.Xml.Linq.SaveOptions)> 类的 <xref:System.Xml.Linq.XNode?displayProperty=fullName> 方法，其 `SaveOptions` 参数设置为 <xref:System.Xml.Linq.SaveOptions>。

## <a name="see-also"></a>请参阅

- [XElement 类动态属性](../designers/attribute-xelement-dynamic-property.md)
- [值](../designers/value-xelement-dynamic-property.md)