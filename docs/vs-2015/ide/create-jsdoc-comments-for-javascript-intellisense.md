---
title: 为 JavaScript IntelliSense 创建 JSDoc 注释 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: a0dadc81-3755-4a47-bcee-c1010819ff2a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b974f3450b88ab22e58e284881f270c1b3d72298
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619273"
---
# <a name="create-jsdoc-comments-for-javascript-intellisense"></a>为 JavaScript IntelliSense 创建 JSDoc 注释
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 中的 IntelliSense 显示你使用标准 JSDoc 注释添加到脚本中的信息。 你可以使用 JSDoc 注释来提供有关代码元素（如函数、字段和变量）的信息。

## <a name="jsdoc-comment-tags"></a>JSDoc 注释标记
 intellisense 使用以下标准 JSDoc 注释标记显示有关代码的信息。

|  JSDoc 标记   |                       语法                        |                                                     注意                                                      |
|--------------|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| @deprecated  |              @deprecated description              |                                   指定一个不推荐使用的函数或方法。                                   |
| @description |             @description description              |                              指定函数或方法的说明。                               |
|    @param    | @param {type} parameterName<em>description</em> | 指定函数或方法中的参数信息。<br /><br /> TypeScript 还支持 @paramTag。 |
|  @property   |          @property {type} propertyName          |   为在对象上定义的字段或成员指定信息（包括说明）。    |
|   @returns   |                  @returns {type}                  |           指定一个返回值。<br /><br /> 对于 TypeScript，请使用 @returnType 而不是 @returns。           |
|   @summary   |               @summary description                |                   指定函数或方法的说明（与 @description 相同）。                   |
|    @type     |                   @type {type}                    |                                指定常量或变量的类型。                                |
|   @typedef   |         @typedef {type} customTypeName          |                                            指定自定义的类型。                                            |

### <a name="examples"></a>示例
 下面的示例演示如何对名为 `getArea` 的函数使用 @description、@param 和 @return JSDoc 标记。

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

 ![函数的 IntelliSense 信息](../ide/media/js-intellisense-jsdoc-comments.png "JS_IntelliSense_JSDoc_Comments")

 下面的示例演示如何将 @typedef 标记与 @property 标记一起使用。

```javascript
/**
  * @typedef {object} Weather
  * @property {string} current The current weather.
  */
function getForecast(Weather) {
}

var w = new Weather();
```

 下面的示例演示如何使用 @type JSDoc 标记。 正如此示例中所示，位于初始星号对 (\*\*) 之后的单个星号 (*) 不是必需的。

```javascript
/**
    @type {string}
*/
const RED = 'FF0000';

```

 下面的示例演示如何使用 @deprecated JSDoc 标记。

```javascript
/**
 * @deprecated since version 2.0
 */
function old() {
}
```
