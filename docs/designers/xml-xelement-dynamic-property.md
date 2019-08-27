---
title: Xml（XElement 动态属性）
ms.date: 11/04/2016
ms.topic: reference
apiname:
- XElement.Xml
ms.assetid: 69ab2a33-4fe7-4cfa-97f8-eaf063decb18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7d58dea02a45ccc84e7829da2acdb479eb17dda3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843948"
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

- [XElement 类动态属性](../designers/xelement-class-dynamic-properties.md)
- [值](../designers/value-xelement-dynamic-property.md)