---
title: 值（XAttribute 动态属性）|Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
api_name:
- XAttribute.Value
api_type:
- Assembly
ms.assetid: 019733d2-e050-4120-b537-831cd3fc008e
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e9a31b4c4182ed67a3e67d3c25c2c5ccf50e083f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664051"
---
# <a name="value-xattribute-dynamic-property"></a>值（XAttribute 动态属性）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

获取或设置 XML 属性的值。

## <a name="syntax"></a>语法

```
attrib.Value
```

## <a name="property-valuereturn-value"></a>属性值/返回值
 包含此属性的值的 <xref:System.String>。

## <a name="exceptions"></a>异常

|异常类型|条件|
|--------------------|---------------|
|<xref:System.ArgumentNullException>|设置时，`value` 为 `null`。|

## <a name="remarks"></a>备注
 此属性等效于 <xref:System.Xml.Linq.XAttribute.Value%2A> 类的 <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> 属性，但此动态属性还支持更改通知。

## <a name="see-also"></a>请参阅
 <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName> [System.xml.linq.xattribute> 类的 Dynamic Properties](../designers/xattribute-class-dynamic-properties.md) [特性](../designers/attribute-xelement-dynamic-property.md)
