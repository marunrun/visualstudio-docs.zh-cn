---
title: '&lt;field &gt; （JavaScript） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <field> JavaScript XML tag
- field JavaScript XML tag
ms.assetid: c494bae0-3095-42a3-aa0a-4c415188c65c
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a3fc786e4d99d1eaff4a8b152ea9496ce8400ff1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663857"
---
# <a name="ltfieldgt-javascript"></a>&lt;field&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

为在对象上定义的字段或成员指定文档信息（包括说明）。

## <a name="syntax"></a>语法

```
<field name="fieldName" static="true|false"
    type="FieldType" integer="true|false"
    domElement="true|false" mayBeNull="true|false"
    elementType="ArrayElementType" elementInteger="true|false"
    elementDomElement="true|false" elementMayBeNull="true|false"
    helpKeyword="keyword" locid="descriptionID"
    value="code">description
</field>
```

#### <a name="parameters"></a>参数
 `name` 字段或成员的名称。 如果在构造函数中使用 `<field>` 元素，则 `name` 是必需的，并且定义标记应用到的成员。 当 `<field>` 元素直接为字段加批注时，将忽略此属性，并且 Visual Studio 使用的名称是源代码中实际字段的名称。

 `static`（可选）。 指定该字段是否为构造函数的成员或构造函数返回的对象的成员。 设置为 `true` 以将字段视为构造函数的成员。 设置为 `false`，以便将字段视为构造函数返回的对象的成员。

 `type`（可选）。 字段的数据类型。 类型可以是下列类型之一：

- ECMAScript 5 规范中的 ECMAScript 语言类型，如 `Number` 和 `Object`。

- DOM 对象，例如 `HTMLElement`、`Window` 和 `Document`。

- JavaScript 构造函数。

  `integer`（可选）。 如果 `Number` `type`，则指定该字段是否为整数。 设置为 `true` 以指示该字段为整数;否则，设置为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `domElement`（可选）。 此属性已弃用；`type` 属性优先于此属性。 此属性指定已记录字段是否为 DOM 元素。 设置为 "`true`" 可指定该字段是 DOM 元素;否则，设置为 `false`。 如果未设置 `type` 特性，并且 `domElement` 设置为 `true`，则在执行语句完成时，IntelliSense 会将文档中的字段作为 `HTMLElement` 处理。

  `mayBeNull`（可选）。 指定记录的字段是否可以设置为 null。 设置为 `true`，以指示字段可以设置为 null;否则，设置为 `false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `elementType`（可选）。 如果 `type` 是 `Array`，此属性指定数组中元素的类型。

  `elementInteger`（可选）。 如果 `type` 是 `Array` 且 `elementType` 是 `Number`，此属性指定数组中的元素是否为整数。 设置为 `true`，指示数组中的元素都是整数；否则，设置为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `elementDomElement`（可选）。 此属性已弃用；`elementType` 属性优先于此属性。 如果 `type` 是 `Array`，此属性指定数组中的元素是否是 DOM 元素。 设置为 `true`，指定该元素是 DOM 元素；否则，设置为 `false`。 如果未指定 `elementType` 属性，且 `elementDomElement` 设置为 `true`，执行语句完成时，IntelliSense 将数组中的每个元素视为 `HTMLElement`。

  `elementMayBeNull`（可选）。 如果 `type` 是 `Array`，指定是否可将数组中的元素设置为 null。 设置为 `true`，指示数组中的元素可以设置为 null；否则，设置为 `false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。

  `helpKeyword`（可选）。 F1 帮助的关键字。

  `locid`（可选）。 有关字段的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 标记中指定的格式。

  `value`（可选）。 指定应计算以供 IntelliSense 使用的代码，而不是函数代码本身。 对于 `<field>`，构造函数支持此属性，但对于对象文本不支持。 当字段类型未定义时，可以使用此特性来提供类型信息。 例如，可以使用 `value=’1’` 将字段类型视为数字。

  `description`（可选）。 字段的说明。

## <a name="remarks"></a>备注
 在构造函数中记录字段时，`name` 属性是必需的。 对于所有其他情况，`<field>` 元素的所有属性都是可选的。

 在记录构造函数时，`<field>` 元素必须紧跟在字段声明之前。 @No__t_0 特性必须与源代码中使用的字段名称匹配。 对于对象成员，如果 `<field>` 元素紧邻对象成员声明之前出现，则可以省略 `name` 特性。

## <a name="example"></a>示例
 下面的代码示例演示如何使用 `<field>` 元素。

```javascript
// Use of <field> in an object definition.
var Rectangle = {
    /// <field type='Number'>The width of the rectangle.</field>
    wid: 5,
    /// <field type='Number'>The length of the rectangle.</field>
    len: 0,
    /// <field type='Number'>Returns the area of the rectangle.</field>
    getArea: function (wid, len) {
        return len * wid;
    }
}

// Use of <field> in a constructor function.
// The name attribute is required.
function Engine() {
    /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>
    this.HorsePower = 150;
}
```

## <a name="example"></a>示例
 下面的示例演示如何使用 `static` 属性设置为 `true` 的 `<field>` 元素。

```javascript
function Engine() {
    /// <field name='HorsePower' static='true' type='Number'>static field desc.</field>
}

Engine.HorsePower = 140;
// IntelliSense on the field is available here.
Engine.

```

## <a name="example"></a>示例
 下面的示例演示如何使用 `static` 属性设置为 `false` 的 `<field>` 元素。

```javascript
function Engine() {
    /// <field name='HorsePower' static='false' type='Number'>Non-static field desc.</field>
}

Engine.HorsePower = 140;
var eng = new Engine();
// IntelliSense on the field is available here.
eng.

```

## <a name="example"></a>示例
 下面的示例演示如何将 `<field>` 元素与 `value` 特性结合使用。

```javascript
function calculator(a) {
    /// <field name='f' value='1'/>
}
new calculator().f.   // Completion list for a Number.

```

## <a name="see-also"></a>另请参阅
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
