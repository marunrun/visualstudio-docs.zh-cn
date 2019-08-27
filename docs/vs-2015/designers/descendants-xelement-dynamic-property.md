---
title: 子代（XElement 动态属性）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 9611d00f-23bf-444b-ab0c-f30701bfc13d
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8c89e04346a4b08d6ee7bbc0012ef52f3b648512
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178198"
---
# <a name="descendants-xelement-dynamic-property"></a>子代（XElement 动态属性）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

获取一个索引器，用于检索与指定扩展名匹配的当前元素的所有子代元素。  
  
## <a name="syntax"></a>语法  
  
```  
elem.Descendants[{namespaceName}localName]  
```  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个类型为 `IEnumerable<XElement> Item(String expandedName)` 的索引器。 此索引器获取指定子代元素的扩展名，并返回 <xref:System.Collections.IEnumerable>`<`<xref:System.Xml.Linq.XElement>`>` 集合中的匹配子元素。  
  
## <a name="remarks"></a>备注  
 此属性等效于 <xref:System.Xml.Linq.XContainer.Descendants%28System.Xml.Linq.XName%29?displayProperty=fullName> 类的 <xref:System.Xml.Linq.XContainer> 方法。  
  
 返回集合中的元素按 XML 源文档顺序排列。  
  
 此属性使用延迟执行。  
  
## <a name="see-also"></a>请参阅  
 [XElement 类动态属性](../designers/xelement-class-dynamic-properties.md)   
 [元素](../designers/elements-xelement-dynamic-property.md)
