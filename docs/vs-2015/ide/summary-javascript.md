---
title: '&lt;摘要&gt; (JavaScript) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- summary JavaScript XML tag
- <summary> JavaScript XML tag
ms.assetid: 6540582d-bdb3-42ec-ad2f-c176783e6f9c
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 81d41918d61bbe95cfe19d2382535449a47deb8c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431415"
---
# <a name="ltsummarygt-javascript"></a>&lt;summary&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定函数或方法的说明。  
  
## <a name="syntax"></a>语法  
  
```  
<summary locid="descriptionID">description  
</summary>  
```  
  
#### <a name="parameters"></a>参数  
 `locid`  
 可选。 有关函数或方法的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 元素中指定的格式。  
  
 `description`  
 可选。 函数或方法的描述。  
  
## <a name="remarks"></a>备注  
 用于批注函数的元素（包括 [\<summary>](../ide/summary-javascript.md)、[\<param>](../ide/param-javascript.md) 和 [\<returns>](../ide/returns-javascript.md)）必须置于任何语句前的函数体中。  
  
## <a name="example"></a>示例  
 下面的代码演示如何使用 `<summary>` 元素。  
  
```javascript  
function areaFunction(radiusParam)  
{  
    /// <summary>Determines the area of a circle when supplied a radius parameter.</summary>  
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>  
    /// <returns type="Number">The area.</returns>  
    var areaVal;  
    areaVal = Math.PI * radiusParam * radiusParam;  
    return areaVal;  
}  
  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
