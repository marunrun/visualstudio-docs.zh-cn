---
title: Xml（XElement 动态属性）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
api_name:
- XElement.Xml
ms.assetid: 69ab2a33-4fe7-4cfa-97f8-eaf063decb18
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 368b18e7524e0cff31139de67f8092f9069246bf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148042"
---
# <a name="xml-xelement-dynamic-property"></a>Xml（XElement 动态属性）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

获取元素的非格式化 XML 内容。  
  
## <a name="syntax"></a>语法  
  
```  
elem.Xml  
```  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 表示元素的非格式化 XML 内容的 <xref:System.String>。  
  
## <a name="remarks"></a>备注  
 此属性等效于 <xref:System.Xml.Linq.XNode.ToString%28System.Xml.Linq.SaveOptions%29> 类的 <xref:System.Xml.Linq.XNode?displayProperty=fullName> 方法，其 `SaveOptions` 参数设置为 <xref:System.Xml.Linq.SaveOptions>。  
  
## <a name="see-also"></a>另请参阅  
 [XElement 类动态属性](../designers/xelement-class-dynamic-properties.md)   
 [值](../designers/value-xelement-dynamic-property.md)
