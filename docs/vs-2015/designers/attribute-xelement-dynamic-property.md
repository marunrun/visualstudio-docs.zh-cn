---
title: 特性（XElement 动态属性） | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 8440fc7d-b3b4-4726-8ec8-492e6af79642
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 551e072b05e7a88ff9624c5d16e4aa199a6afd66
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657984"
---
# <a name="attribute-xelement-dynamic-property"></a>特性（XElement 动态属性）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

获取一个索引器，该索引器用于检索与指定扩展名对应的属性实例。

## <a name="syntax"></a>语法

```
elem.Attribute[{namespaceName}attribName]
```

## <a name="property-valuereturn-value"></a>属性值/返回值
 一个类型为 `XAttribute Item(String expandedName)` 的索引器。 此索引器获取指定属性的扩展名，然后返回相应的 <xref:System.Xml.Linq.XAttribute>，如果没有具有指定名称的属性，则返回 `null`。

## <a name="remarks"></a>备注
 此属性等效于 <xref:System.Xml.Linq.XElement.Attribute%2A> 类的 <xref:System.Xml.Linq.XElement?displayProperty=fullName> 方法。

## <a name="see-also"></a>请参阅
 <xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName> [System.xml.linq.xelement> 类动态属性](../designers/xelement-class-dynamic-properties.md)[值](../designers/value-xattribute-dynamic-property.md)
