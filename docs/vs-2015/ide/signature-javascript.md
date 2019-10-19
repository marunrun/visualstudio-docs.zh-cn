---
title: '&lt;signature &gt; （JavaScript） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <signature> JavaScript XML tag
- signature JavaScript XML tag
ms.assetid: 319138e7-cfbe-4b37-9643-2ddb7f9c63d4
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b4c640c28ada16a8a03943fcd1362d4fd521772c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671131"
---
# <a name="ltsignaturegt-javascript"></a>&lt;signature &gt; （JavaScript）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对函数或方法的一组相关元素进行分组，以提供重载函数的文档。

## <a name="syntax"></a>语法

```
<signature externalid="id" externalFile="filename"
    helpKeyword="keyword" locid="descriptionID">
</signature>
```

#### <a name="parameters"></a>参数
 `externalid`（可选）。 如果 `vsdoc` [\<loc >](../ide/loc-javascript.md)元素的 `format` 属性，则此属性指定用于查找与签名关联的 XML 代码的成员 ID。 与 `locid` 特性不同，此特性指定应加载具有此 ID 的成员中的所有元素。 XML 代码中提供的任何关联的说明信息还将与签名中指定的元素合并在一起。 这使您可以在挎斗文件中指定其他元素（如 `<capability>`），而无需在源文件中指定它们。 `externalid` 是一个可选属性。

 `externalFile`（可选）。 指定要在其中查找 `externalid` 的文件的名称。 如果没有 `externalid`，则忽略此属性。 这是一个可选属性。 默认值是当前文件的名称，但文件扩展名为 .xml，而不是 .js。 默认情况下，用于本地化的托管资源查找规则用于查找文件。

 `helpKeyword`（可选）。 F1 帮助的关键字。

 `locid`（可选）。 有关字段的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 标记中指定的格式。

## <a name="remarks"></a>备注
 对 .js 文件中的每个重载函数说明使用一个 `<signature>` 元素，或为指定的每个外部成员 ID 使用一个 `<signature>` 元素。

 在任何语句之前，必须将 `<signature>` 元素放在函数体中。 使用[\<summary >](../ide/summary-javascript.md)、 [\<param >](../ide/param-javascript.md)[或 \<returns 元素与](../ide/returns-javascript.md)> 元素 `<signature>` 时，请将其他元素放置在 `<signature>` 块内。

## <a name="example"></a>示例
 下面的代码示例演示如何使用 `<signature>` 元素。

```javascript
// Use of <signature> with externalid.
// Requires use of the <loc> tag to identify the external functions.
function illuminate(light) {
    /// <signature externalid='M:Windows.Devices.Light.Illuminate()' />
    /// <signature externalid='M:Windows.Devices.Light.Illuminate(System.Int32)'>
    ///   <param name='light' type='Number' />
    /// </signature>
}

// Use of <signature> for overloads implemented in JavaScript.
function add(a, b) {
    /// <signature>
    /// <summary>function summary 1</summary>
    /// <param name="a" type="Number">The first number</param>
    /// <param name="b" type="Number">The second number</param>
    /// <returns type="Number" />
    /// </signature>
    /// <signature>
    /// <summary>function summary 2 – differ by number of params</summary>
    /// <param name="a" type="Number">Only 1 parameter</param>
    /// <returns type="Number" />
    /// </signature>
    /// <signature>
    /// <summary>function summary 3 – differ by parameter type</summary>
    /// <param name="a" type="Number">Number parameter</param>
    /// <param name="b" type="String">String parameter</param>
    /// <returns type="Number" />
    /// </signature>
    /// <signature>
    /// <summary>function summary 4 – differ by return type</summary>
    /// <param name="a" type="Number">The first number</param>
    /// <param name="b" type="Number">The second number</param>
    /// <returns type="String" />
    /// </signature>

    return a + b;
}
```

## <a name="see-also"></a>另请参阅
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
