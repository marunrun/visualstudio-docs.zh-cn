---
title: 为 JavaScript IntelliSense 创建 XML 文档注释 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code comments, JavaScript IntelliSense
- XML documentation comments, JavaScript IntelliSense
- documentation comments [JavaScript]
- IntelliSense [JavaScript], XML documentation comments
ms.assetid: a27f5b50-9807-436f-a0cf-6f3137ecbaf0
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 21fdc15b161b7d1cef30effe82e518a174bc9666
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619551"
---
# <a name="create-xml-documentation-comments-for-javascript-intellisense"></a>为 JavaScript IntelliSense 创建 XML 文档注释
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*XML 文档注释*是添加到脚本中的 JavaScript 注释，用于提供有关代码元素（如函数、字段和变量）的信息。 在 Visual Studio 中，当你引用脚本函数时，这些文本说明与 IntelliSense 一起显示。

 本主题提供有关使用 XML 文档注释的基本教程。 有关使用其他元素（如[\<var >](../ide/var-javascript.md)和[\<value >](../ide/value-javascript.md)）的信息，以及有关其他代码示例的信息，请参阅[XML 文档注释](../ide/xml-documentation-comments-javascript.md)。 有关为异步回调（如 `Promise`）提供 IntelliSense 信息的信息，请参阅[\<returns >](../ide/returns-javascript.md)。

> [!NOTE]
> XML 文档注释只能从引用的文件、程序集和服务中提供。

### <a name="to-create-xml-documentation-comments-for-a-javascript-function"></a>为 JavaScript 函数创建 XML 文档注释

- 在函数中，添加[\<summary >](../ide/summary-javascript.md)、 [\<param >](../ide/param-javascript.md)和[\<returns](../ide/returns-javascript.md) > 元素，并在每个元素前面加上三个斜杠标记（///）。

    > [!NOTE]
    > 每个元素必须在一行上。

     下面的示例演示了一个 JavaScript 函数。

    ```javascript
    function getArea(radius)
    {
        /// <summary>Determines the area of a circle that has the specified radius parameter.</summary>
        /// <param name="radius" type="Number">The radius of the circle.</param>
        /// <returns type="Number">The area.</returns>
        var areaVal;
        areaVal = Math.PI * radius * radius;
        return areaVal;
    }
    ```

- 若要查看 XML 文档注释，请键入标有 XML 文档注释的函数的名称和左括号，如以下示例中所示：

    ```javascript
    var areaVal = getArea(
    ```

     当你键入包含 XML 文档注释的函数的左括号时，代码编辑器使用 IntelliSense 显示 XML 文档注释中定义的信息。

### <a name="to-create-xml-documentation-comments-for-a-javascript-field"></a>为 JavaScript 字段创建 XML 文档注释

- 在构造函数或对象定义中，添加一个[\<field >](../ide/field-javascript.md)元素，该元素前面有三个斜杠标记（///）。

     下面的示例演示如何在构造函数中使用 `<field>` 元素。 有关其他示例，请参阅[\<field >](../ide/field-javascript.md)。

    ```javascript
    function Engine() {
        /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>
        this.HorsePower = 150;
    }
    ```

- 若要查看 XML 文档注释，请使用标记有 XML 文档注释的函数构造函数创建对象，如下面的示例中所示。

    ```javascript
    var eng = new Engine();
    ```

- 在下一行中，键入对象的名称和句点以显示字段的 IntelliSense 信息。

    ```javascript
    eng.
    ```

### <a name="to-create-xml-documentation-comments-for-an-overloaded-function"></a>为重载函数创建 XML 文档注释

1. 在函数中，为每个重载添加一个[\<signature >](../ide/signature-javascript.md)元素。 在这些元素中，添加其他元素，例如 `<summary>`、`<param>` 和 `<returns>`，并在每个元素前面加上三个斜杠标记（///）。

     下面的示例演示一个重载的 JavaScript 函数。 在此示例中，重载不同于参数类型。

    ```javascript
    function calc(a) {
        /// <signature>
        /// <summary>Function summary 1.</summary>
        /// <param name="a" type="Number">A number.</param>
        /// <returns type="Number" />
        /// </signature>
        /// <signature>
        /// <summary>Function summary 2.</summary>
        /// <param name="a" type="String">A string.</param>
        /// <returns type="Number" />
        /// </signature>
        return a;
    }
    ```

2. 若要查看 XML 文档注释，请键入标记有 XML 文档注释的函数的名称和左括号，如以下示例中所示：

    ```javascript
    calc(
    ```

### <a name="to-create-localized-intellisense"></a>创建本地化的 IntelliSense

1. 创建一个 XML 文件，该文件包含 OpenAjax MessageBundle 格式的文档注释。

    > [!IMPORTANT]
    > 建议采用 MessageBundle 格式。 Microsoft Ajax 或 winmd 文件中不支持此格式。 有关使用替代 `VSDoc` 格式的信息，请参阅[\<loc >](../ide/loc-javascript.md)。

     下面的示例显示挎斗文件中包含本地化 IntelliSense 信息的内容。 这是位于特定于区域性的文件夹中的 XML 文件，如 JA。 文件夹必须与包含 `<loc>` 元素的 .js 文件位于同一位置。 XML 文件的文件名必须与 `<loc>` 元素中指定的 `filename` 参数匹配。

    ```
    <messagebundle>
      <msg name="1">A class that represents a rectangle</msg>
      <msg name="2">The length of the rectangle</msg>
      <msg name="3">The height of the rectangle</msg>
    </messagebundle>

    ```

2. 在 .js 文件中，添加以下代码。 @No__t_0 元素必须在任何脚本之前声明，并遵循与 `<reference>` 元素相同的使用规则。 有关详细信息，请参阅[JavaScript IntelliSense](../ide/javascript-intellisense.md)和[\<loc >](../ide/loc-javascript.md)。

    ```javascript
    /// <loc filename="messageFilename.xml" format="messagebundle"/>

    ```

3. 在 .js 文件中，添加 XML 文档元素和默认说明。 设置 `locid` 属性值以与挎斗文件中的相应 `name` 属性值相匹配。 默认说明将替换为本地化的 IntelliSense 信息（如果可用）。

    ```javascript
    function add(a,b)
    {
        /// <summary locid='1'>description</summary>
        /// <param name='a' locid='2'>parameter a description</param>
        /// <param name='b' locid='3'>parameter b description</param>
    }

    ```

4. 若要查看 XML 文档注释，请键入函数的名称和左括号，如以下示例中所示：

    ```javascript
    add(
    ```

## <a name="see-also"></a>请参阅
 [JavaScript intellisense](../ide/javascript-intellisense.md) [XML 文档注释](../ide/xml-documentation-comments-javascript.md)[钢笔尖：演练： JavaScript IntelliSense in ASP.NET](https://msdn.microsoft.com/4f6e0cc2-7f48-4dbf-abb0-7fb743a2d05b)
