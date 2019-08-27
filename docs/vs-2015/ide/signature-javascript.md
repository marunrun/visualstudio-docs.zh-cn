---
title: '&lt;签名&gt;(JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <signature> JavaScript XML tag
- signature JavaScript XML tag
ms.assetid: 319138e7-cfbe-4b37-9643-2ddb7f9c63d4
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 02a4c36f3969ca0f9ef61e817afb82eb8247f041
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203487"
---
# <a name="ltsignaturegt-javascript"></a>&lt;签名&gt;(JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

组的相关元素的函数或方法提供重载函数的文档。  
  
## <a name="syntax"></a>语法  
  
```  
<signature externalid="id" externalFile="filename"  
    helpKeyword="keyword" locid="descriptionID">  
</signature>   
```  
  
#### <a name="parameters"></a>参数  
 `externalid`  
 可选。 如果`format`特性[ \<loc >](../ide/loc-javascript.md)元素是`vsdoc`，此属性指定的成员 ID 用于查找与签名关联的 XML 代码。 与不同`locid`属性，此属性指定应加载中具有此 ID 的成员的所有元素。 在 XML 代码中的任何相关的描述信息也将与在签名中指定的元素合并。 这使您可以指定其他元素，如`<capability>`，而无需指定源文件中的挎斗文件中。 `externalid` 为可选属性。  
  
 `externalFile`  
 可选。 指定在其中查找文件的名称`externalid`。 如果没有，则忽略此特性`externalid`存在。 此为可选属性。 默认值为但而不是.js 的.xml 文件扩展名的当前文件的名称。 默认情况下，用于本地化的托管的资源查找规则用于找到的文件。  
  
 `helpKeyword`  
 可选。 F1 帮助的关键字。  
  
 `locid`  
 可选。 有关字段的本地化信息的标识符。 标识符是成员 ID 或对应于 OpenAjax 元数据定义的消息绑定中的 `name` 属性值。 标识符类型取决于 [\<loc>](../ide/loc-javascript.md) 标记中指定的格式。  
  
## <a name="remarks"></a>备注  
 使用一个`<signature>`元素为每个重载中的.js 文件或使用以下任意函数说明`<signature>`元素指定每个外部成员 ID。  
  
 `<signature>`元素必须置于任何语句之前在函数体中。 使用时[\<摘要 >](../ide/summary-javascript.md)， [ \<param >](../ide/param-javascript.md)，或者[\<返回 >](../ide/returns-javascript.md)元素`<signature>`元素，将放置在其他元素`<signature>`块。  
  
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
