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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2b83e4a208553b0ad732cfe927aec02b47e389dd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187512"
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
  
## <a name="exceptions"></a>Exceptions  
  
|异常类型|条件|  
|--------------------|---------------|  
|<xref:System.ArgumentNullException>|设置时，`value` 为 `null`。|  
  
## <a name="remarks"></a>备注  
 此属性等效于 <xref:System.Xml.Linq.XAttribute.Value%2A> 类的 <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> 属性，但此动态属性还支持更改通知。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>   
 [XAttribute 类动态属性](../designers/xattribute-class-dynamic-properties.md)   
 [特性](../designers/attribute-xelement-dynamic-property.md)
