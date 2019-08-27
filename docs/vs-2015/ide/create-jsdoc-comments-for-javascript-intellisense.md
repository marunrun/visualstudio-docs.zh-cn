---
title: 为 JavaScript IntelliSense 创建 JSDoc 注释 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: a0dadc81-3755-4a47-bcee-c1010819ff2a
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f4d300651731b38b9b86421d36d9de169dc6464d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188791"
---
# <a name="create-jsdoc-comments-for-javascript-intellisense"></a>为 JavaScript IntelliSense 创建 JSDoc 注释
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 中的 IntelliSense 显示你使用标准 JSDoc 注释添加到脚本中的信息。 你可以使用 JSDoc 注释来提供有关代码元素（如函数、字段和变量）的信息。  

## <a name="jsdoc-comment-tags"></a>JSDoc 注释标记  
 intellisense 使用以下标准 JSDoc 注释标记显示有关代码的信息。  

|  JSDoc 标记   |                       语法                        |                                                     说明                                                      |
|--------------|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| @deprecated  |              @deprecated description               |                                   指定一个不推荐使用的函数或方法。                                   |
| @description |             @description description               |                              指定函数或方法的说明。                               |
|    @param    | @param {type} parameterName<em>description</em>   | 指定函数或方法中的参数信息。<br /><br /> TypeScript 还支持@paramTag。 |
|  @property   |          @property {type} propertyName            |   为在对象上定义的字段或成员指定信息（包括说明）。    |
|   @returns   |                  @returns {type}                   |           指定一个返回值。<br /><br /> 对于 TypeScript，请使用@returnType而不是@returns。           |
|   @summary   |               @summary description                 |                   指定函数或方法的说明 (与相同@description)。                   |
|    @type     |                   @type {type}                     |                                指定常量或变量的类型。                                |
|   @typedef   |         @typedef {type} customTypeName            |                                            指定自定义的类型。                                            |

### <a name="examples"></a>示例  
 下面的示例演示如何使用@description， @param，并@returnJSDoc 标记的一个名为函数`getArea`。  

```javascript  
/** @description Determines the area of a circle that has the specified radius parameter.  
 * @param {number} radius The radius of the circle.  
 * @return {number}  
 */  
function getArea(radius) {  
    var areaVal;  
    areaVal = Math.PI * radius * radius;  
    return areaVal;  
}  
```  

 在前面的示例中，当你为 `getArea` 键入左括号时，IntelliSense 显示说明、参数和返回信息。  

 ![对于函数的 IntelliSense 信息](../ide/media/js-intellisense-jsdoc-comments.png "JS_IntelliSense_JSDoc_Comments")  

 下面的示例演示如何使用@typedef标记@property标记。  

```javascript  
/**  
  * @typedef {object} Weather  
  * @property {string} current The current weather.  
  */  
function getForecast(Weather) {  
}  

var w = new Weather();  
```  

 下面的示例演示如何使用@typeJSDoc 标记。 正如此示例中所示，位于初始星号对 (\*\*) 之后的单个星号 (*) 不是必需的。  

```javascript  
/**  
    @type {string}  
*/  
const RED = 'FF0000';  

```  

 下面的示例演示如何使用@deprecatedJSDoc 标记。  

```javascript  
/**  
 * @deprecated since version 2.0  
 */  
function old() {  
}  
```
