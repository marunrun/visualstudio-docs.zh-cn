---
title: '&lt;字段&gt;(JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <field> JavaScript XML tag
- field JavaScript XML tag
ms.assetid: c494bae0-3095-42a3-aa0a-4c415188c65c
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b2fe09070261460b7b83f54de44a07cf96d40cf2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68181275"
---
# <a name="ltfieldgt-javascript"></a>&lt;field&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定文档的信息，包括说明，为字段或在对象定义的成员。  
  
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
 `name`  
 字段或成员的名称。 当`<field>`在构造函数中使用元素`name`是必需的定义标记应用到的成员。 当`<field>`元素直接批注字段，则忽略此属性，并由 Visual Studio 使用的名称是在源代码中的实际字段的名称。  
  
 `static`  
 可选。 指定是否该字段是构造函数的成员，或者对象的成员函数返回的构造函数。 设置为`true`将字段视为构造函数的成员。 设置为`false`将字段视为构造函数返回的对象的成员。  
  
 `type`  
 可选。 字段的数据类型。 类型可以是下列类型之一：  
  
- ECMAScript 语言键入在 ECMAScript 5 规范中，如`Number`和`Object`。  
  
- DOM 对象，例如 `HTMLElement`、`Window` 和 `Document`。  
  
- JavaScript 构造函数。  
  
  `integer`  
  可选。 如果`type`是`Number`，指定该字段是否是一个整数。 设置为`true`以指示该字段是一个整数; 否则，将设置为`false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。  
  
  `domElement`  
  可选。 此属性已弃用；`type` 属性优先于此属性。 此属性指定是否有案可稽的字段是 DOM 元素。 设置为`true`以指定该字段是一个 DOM 元素; 否则，将设置为`false`。 如果`type`未设置属性和`domElement`设置为`true`，IntelliSense 将有案可稽的字段视为`HTMLElement`执行语句完成时。  
  
  `mayBeNull`  
  可选。 指定是否可以设置有案可稽的字段为 null。 设置为`true`若要指示字段可以设置为 null; 否则为将设置为`false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。  
  
  `elementType`  
  可选。 如果 `type` 是 `Array`，此属性指定数组中元素的类型。  
  
  `elementInteger`  
  可选。 如果 `type` 是 `Array` 且 `elementType` 是 `Number`，此属性指定数组中的元素是否为整数。 设置为 `true`，指示数组中的元素都是整数；否则，设置为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。  
  
  `elementDomElement`  
  可选。 此属性已弃用；`elementType` 属性优先于此属性。 如果 `type` 是 `Array`，此属性指定数组中的元素是否是 DOM 元素。 设置为 `true`，指定该元素是 DOM 元素；否则，设置为 `false`。 如果未指定 `elementType` 属性，且 `elementDomElement` 设置为 `true`，执行语句完成时，IntelliSense 将数组中的每个元素视为 `HTMLElement`。  
  
  `elementMayBeNull`  
  可选。 如果 `type` 是 `Array`，指定是否可将数组中的元素设置为 null。 设置为 `true`，指示数组中的元素可以设置为 null；否则，设置为 `false`。 默认值为 `false`。 Visual Studio 不使用此属性以提供 IntelliSense 信息。  
  
  `helpKeyword`  
  可选。 F1 帮助的关键字。  
  
  `locid`  
  可选。 有关字段的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 标记中指定的格式。  
  
  `value`  
  可选。 指定应将使用由评估 IntelliSense 而不是函数代码本身的代码。 有关`<field>`，此属性支持的构造函数，但不是支持对象文字。 可以使用此属性是未定义的字段类型时提供类型信息。 例如，可以使用`value=’1’`要被视为一个数字字段类型。  
  
  `description`  
  可选。 字段说明。  
  
## <a name="remarks"></a>备注  
 `name`属性是必需的当正在记录的构造函数中的字段。 对于所有其他情况，所有属性的`<field>`元素是可选的。  
  
 当您要记录的构造函数，`<field>`元素必须出现在字段声明之前立即。 `name`属性必须与在源代码中使用的字段名称匹配。 为对象成员`name`属性，则可省略`<field>`元素将显示紧靠对象成员声明之前。  
  
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
 下面的示例演示如何使用`<field>`具有元素`static`属性设置为`true`。  
  
```javascript  
function Engine() {  
    /// <field name='HorsePower' static='true' type='Number'>static field desc.</field>  
}  
  
Engine.HorsePower = 140;  
// IntelliSense on the field is available here.  
Engine.  
  
```  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`<field>`具有元素`static`属性设置为`false`。  
  
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
 下面的示例演示如何使用`<field>`具有元素`value`属性。  
  
```javascript  
function calculator(a) {  
    /// <field name='f' value='1'/>  
}  
new calculator().f.   // Completion list for a Number.  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
