---
title: '&lt;value &gt; （JavaScript） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <value> JavaScript XML tag
- value JavaScript XML tag
ms.assetid: 983e31de-cb1d-411e-b60d-eea6698a26f6
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aefe710cc730d5624abc01bbdfc54d9961788787
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656396"
---
# <a name="ltvaluegt-javascript"></a>&lt;value&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定 ECMAScript 3 属性的 `get` 和 `set` 函数的文档信息。

## <a name="syntax"></a>语法

```
<value type="ValueType" integer="true|false"
    domElement="true|false" mayBeNull="true|false"
    elementType="ArrayElementType" elementInteger="true|false"
    elementDomElement="true|false" elementMayBeNull="true|false"
    locid="descriptionID">description
</value>
```

#### <a name="parameters"></a>参数
 `type`（可选）。 属性的数据类型。 类型可以是下列类型之一：

- ECMAScript 5 规范中的 ECMAScript 语言类型，例如 `Number` 和 `Object`。

- DOM 对象，例如 `HTMLElement`、`Window` 和 `Document`。

- JavaScript 构造函数。

  `integer`（可选）。 如果 `Number` `type`，则指定该属性是否为整数。 设置为 `true`，以指示该属性为整数;否则，设置为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `domElement`（可选）。 此属性已弃用；`type` 属性优先于此属性。 此属性指定所记录的属性是否为 DOM 元素。 设置为 `true` 以指定该属性为 DOM 元素;否则，设置为 `false`。 如果未设置 `type` 特性，并且 `domElement` 设置为 `true`，则在执行语句完成时，IntelliSense 将记录的属性作为 `HTMLElement` 处理。

  `mayBeNull`（可选）。 指定记录的属性是否可以设置为 null。 设置为 `true` 以指示属性可以设置为 null;否则，设置为 `false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `elementType`（可选）。 如果 `type` 是 `Array`，此属性指定数组中元素的类型。

  `elementInteger`（可选）。 如果 `type` 是 `Array` 且 `elementType` 是 `Number`，此属性指定数组中的元素是否为整数。 设置为 `true`，指示数组中的元素都是整数；否则，设置为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `elementDomElement`（可选）。 此属性已弃用；`elementType` 属性优先于此属性。 如果 `type` 是 `Array`，此属性指定数组中的元素是否是 DOM 元素。 设置为 `true`，指定该元素是 DOM 元素；否则，设置为 `false`。 如果未指定 `elementType` 属性，且 `elementDomElement` 设置为 `true`，执行语句完成时，IntelliSense 将数组中的每个元素视为 `HTMLElement`。

  `elementMayBeNull`（可选）。 如果 `type` 是 `Array`，指定是否可将数组中的元素设置为 null。 设置为 `true`，指示数组中的元素可以设置为 null；否则，设置为 `false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `locid`（可选）。 有关属性的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 元素中指定的格式。

  `description`（可选）。 属性的说明。

## <a name="remarks"></a>备注
 ECMAScript 5 属性使用[\<summary >](../ide/summary-javascript.md)元素。

 在 `get` 或 `set` 函数之前立即使用 `<value>` 元素。

## <a name="example"></a>示例
 下面的代码示例演示如何对 `get` 函数使用 `<value>` 元素。

```javascript
function Sys$CancelEventArgs$get_cancel() {
    /// <value type="Boolean" locid="P:J#Sys.CancelEventArgs.cancel"></value>
    if (arguments.length !== 0) throw Error.parameterCount();
    return this._cancel();
}
```

## <a name="see-also"></a>另请参阅
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
