---
title: '&lt;param&gt; (JavaScript) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <param> JavaScript XML tag
- param JavaScript XML tag
ms.assetid: 2c4e0167-c1dd-4e54-83f1-c437856bddc1
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ca6207d22d82e607fa589f944230b36b46e633c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670364"
---
# <a name="ltparamgt-javascript"></a>&lt;param&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定函数或方法中的参数的文档信息。

## <a name="syntax"></a>语法

```
<param name="parameterName" type="ParameterType"
    integer="true|false" domElement="true|false"
    mayBeNull="true|false" elementType="ArrayElementType"
    elementInteger="true|false" elementDomElement="true|false"
    elementMayBeNull="true|false" locid="descriptionID"
    parameterArray="true|false" optional="true|false"
    value="code">description
</param>
```

#### <a name="parameters"></a>参数
 `name`（必需）。 参数的名称。

 `type`（可选）。 参数的数据类型。 类型可以是下列类型之一：

- ECMAScript 5 规范中的 ECMAScript 语言类型，例如 `Number` 和 `Object` 。

- DOM 对象，例如 `HTMLElement`、`Window` 和 `Document`。

- JavaScript 构造函数。

  `integer`（可选）。 如果 `type` 为 `Number` ，则指定参数是否为整数。 如果设置为，则 `true` 指示参数为整数; 否则，设置为 `false` 。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `domElement`（可选）。 此属性已弃用；`type` 属性优先于此属性。 此属性指定所记录的参数是否为 DOM 元素。 如果设置为，则 `true` 指定该参数是 DOM 元素; 否则，将设置为 `false` 。 如果 `type` 未设置属性，并且 `domElement` 设置为，则 `true` `HTMLElement` 在执行语句完成时，IntelliSense 将记录的参数视为。

  `mayBeNull`（可选）。 指定记录的参数是否可以设置为 null。 如果设置为， `true` 则指示参数可以设置为 null; 否则设置为 `false` 。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `elementType`（可选）。 如果 `type` 是 `Array`，此属性指定数组中元素的类型。

  `elementInteger`（可选）。 如果 `type` 是 `Array` 且 `elementType` 是 `Number`，此属性指定数组中的元素是否为整数。 设置为 `true`，指示数组中的元素都是整数；否则，设置为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `elementDomElement`（可选）。 此属性已弃用；`elementType` 属性优先于此属性。 如果 `type` 是 `Array`，此属性指定数组中的元素是否是 DOM 元素。 设置为 `true`，指定该元素是 DOM 元素；否则，设置为 `false`。 如果未指定 `elementType` 属性，且 `elementDomElement` 设置为 `true`，执行语句完成时，IntelliSense 将数组中的每个元素视为 `HTMLElement`。

  `elementMayBeNull`（可选）。 如果 `type` 是 `Array`，指定是否可将数组中的元素设置为 null。 设置为 `true`，指示数组中的元素可以设置为 null；否则，设置为 `false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `locid`（可选）。 有关参数的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于元素中指定的格式 [\<loc>](../ide/loc-javascript.md) 。

  `parameterArray`（可选）。 指定是否可以在函数调用中重复记录的参数，这类似于函数中支持的重复参数 `String.format` 。 如果设置为， `true` 则指示可以重复参数; 否则设置为 `false` 。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `optional`（可选）。 指定所记录的参数是否在调用函数中是可选的。 设置为 `true` 可指示参数是可选的; 否则设置为 `false` 。

  `value`（可选）。 指定应计算以供 IntelliSense 使用的代码，而不是函数代码本身。 当参数类型未定义时，可以使用此特性来提供类型信息。 例如，可以使用 `value=’1’` 将参数类型视为数字。

  `description`（可选）。 参数的说明。

## <a name="remarks"></a>备注
 唯一必需的属性是 `name` 。 所有其他属性都是可选的。

 用于批注函数的元素（如 [\<summary>](../ide/summary-javascript.md) 、 [\<param>](../ide/param-javascript.md) 和 [\<returns>](../ide/returns-javascript.md) ）必须位于函数体中任何语句之前。

 如果有多个 `<param>` 具有相同名称的元素，则将使用其中一个 `<param>` 元素，并忽略冗余元素。 确定所使用的元素的行为未定义。 如果 `name` 引用不存在的参数，则忽略该元素。

## <a name="example"></a>示例
 下面的代码示例演示如何使用 `<param>` 元素。

```javascript
function areaFunction(radiusParam)
{
    /// <summary>Determines the area of a circle when provided a radius parameter.</summary>
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>
    /// <returns type="Number">The area.</returns>
    var areaVal;
    areaVal = Math.PI * radiusParam * radiusParam;
    return areaVal;
}

// Uses of <param> with the value attribute.

function calculate(a) {
    /// <param name='a' value='1'/>
    a.    // Completion list for a Number.
}

function calculate(a) {
    /// <param name='a' value='{x:0,y:0}'/>
    a.    // x and y appear in the completion list.
}

```

## <a name="see-also"></a>另请参阅
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
