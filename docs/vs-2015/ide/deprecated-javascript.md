---
title: '&lt;不推荐使用&gt;(JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: cf33d371-59da-4310-95ee-d7524fd9d58c
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b93a2b4dcc541f32c16766da0dd9dd19a4fdfe0d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68177806"
---
# <a name="ltdeprecatedgt-javascript"></a>&lt;deprecated&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定一个不推荐使用的函数或方法。  
  
## <a name="syntax"></a>语法  
  
```  
<deprecated  
    type="deprecate|remove"  
    locid="descriptionID">description  
</deprecated>  
```  
  
#### <a name="parameters"></a>参数  
 `type`  
 可选。 指定是否函数或方法中将删除未来版本中，或是否函数或方法已被移除，并且它的使用可能会导致错误。 设置为`deprecate`来指定，将在未来的版本中删除的函数或方法。 设置为`remove`指定的函数或方法已被移除。  
  
 `locid`  
 可选。 有关函数或方法的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 元素中指定的格式。  
  
 `description`  
 可选。 函数或不推荐使用的方法的说明。  
  
## <a name="remarks"></a>备注  
 用于批注函数，它包含的元素`<deprecated>`，必须放置在任何语句之前在函数体。 将函数标记为已弃用后，我们建议你将为其[\<摘要 >](../ide/summary-javascript.md)具有元素`<deprecated>`元素。  
  
## <a name="example"></a>示例  
 下面的代码演示如何使用 `<deprecated>` 元素。  
  
```javascript  
function areaFunction(radiusParam) {  
    /// <deprecated type="deprecate" >Determines the area of a circle when supplied a radius parameter.</deprecated>  
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>  
    /// <returns type="Number">The area.</returns>  
    var areaVal;  
    areaVal = Math.PI * radiusParam * radiusParam;  
    return areaVal;  
}  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
