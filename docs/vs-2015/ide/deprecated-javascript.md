---
title: '&lt;deprecated &gt; （JavaScript） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: cf33d371-59da-4310-95ee-d7524fd9d58c
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 343f3ebe4bea7ee999f60741c189f35defb0ac7b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665807"
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
 `type`（可选）。 指定是否将在未来版本中移除该函数或方法，或者函数或方法是否已被移除，并且其使用可能导致错误。 设置为 "`deprecate`"，以指定将在未来版本中删除函数或方法。 设置为 `remove` 以指定已删除函数或方法。

 `locid`（可选）。 有关函数或方法的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 元素中指定的格式。

 `description`（可选）。 不推荐使用的函数或方法的说明。

## <a name="remarks"></a>备注
 用于批注包含 `<deprecated>` 的函数的元素必须置于函数体中任何语句之前。 如果将某个函数标记为已弃用，我们建议你将其[\<summary >](../ide/summary-javascript.md)元素替换为 `<deprecated>` 元素。

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
