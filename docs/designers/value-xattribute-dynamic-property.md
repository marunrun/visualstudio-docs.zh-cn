---
title: 值（XAttribute 动态属性）
ms.date: 11/04/2016
ms.topic: reference
apiname:
- XAttribute.Value
apitype: Assembly
ms.assetid: 019733d2-e050-4120-b537-831cd3fc008e
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fefa3d13f1a38b5d1c329fa9df9220e13e769b1c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72634518"
---
# <a name="value-xattribute-dynamic-property"></a>值（XAttribute 动态属性）

获取或设置 XML 属性的值。

## <a name="syntax"></a>语法

```xaml
attrib.Value
```

## <a name="property-valuereturn-value"></a>属性值/返回值

包含此属性的值的 <xref:System.String>。

## <a name="exceptions"></a>异常

|异常类型|条件|
| - |---------------|
|<xref:System.ArgumentNullException>|设置时，`value` 为 `null`。|

## <a name="remarks"></a>备注

此属性等效于 <xref:System.Xml.Linq.XAttribute.Value%2A> 类的 <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> 属性，但此动态属性还支持更改通知。

## <a name="see-also"></a>请参阅

- <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>
- [XAttribute 类动态属性](../designers/value-xattribute-dynamic-property.md)
- [特性](../designers/attribute-xelement-dynamic-property.md)