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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9fba6ff1b4c56243a47c8b136a25d6f9d593d8e3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701245"
---
# <a name="create-xml-documentation-comments-for-javascript-intellisense"></a>为 JavaScript IntelliSense 创建 XML 文档注释
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*XML 文档注释*是 JavaScript 注释添加到脚本中以便提供有关代码元素，如函数、 字段和变量的信息。 在 Visual Studio 中，这些文本说明时引用的脚本函数与 IntelliSense 一起显示。  
  
 本主题提供有关使用 XML 文档注释的基本教程。 了解如何使用其他元素，如[ \<var >](../ide/var-javascript.md)并[\<值 >](../ide/value-javascript.md)，和其他代码示例，请参阅[XML 文档注释](../ide/xml-documentation-comments-javascript.md). 了解如何提供 IntelliSense 信息的异步回调，如`Promise`，请参阅[\<返回 >](../ide/returns-javascript.md)。  
  
> [!NOTE]
> XML 文档注释只能从引用的文件、程序集和服务中提供。  
  
### <a name="to-create-xml-documentation-comments-for-a-javascript-function"></a>若要创建 XML 文档注释的 JavaScript 函数  
  
- 在函数中，添加[\<摘要 >](../ide/summary-javascript.md)， [ \<param >](../ide/param-javascript.md)，以及[\<返回 >](../ide/returns-javascript.md)元素，每个元素与前面三个正斜杠标记 （/ /）。  
  
    > [!NOTE]
    > 每个元素必须是单个行上。  
  
     下面的示例显示了一个 JavaScript 函数。  
  
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
  
- 若要查看 XML 文档注释，请键入名称和标记使用 XML 文档注释，如以下示例所示的函数的左括号：  
  
    ```javascript  
    var areaVal = getArea(  
    ```  
  
     当你键入包含 XML 文档注释的函数的左括号时，代码编辑器中使用 IntelliSense 来显示在 XML 文档注释中定义的信息。  
  
### <a name="to-create-xml-documentation-comments-for-a-javascript-field"></a>若要创建 JavaScript 字段的 XML 文档注释  
  
- 在构造函数函数或对象定义中，添加[\<字段 >](../ide/field-javascript.md)元素前面三个斜杠 （/ /）。  
  
     下面的示例演示如何使用`<field>`构造函数中的元素。 有关其他示例，请参阅[\<字段 >](../ide/field-javascript.md)。  
  
    ```javascript  
    function Engine() {  
        /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>  
        this.HorsePower = 150;  
    }  
    ```  
  
- 若要查看 XML 文档注释，请使用 XML 文档注释，如以下示例所示使用 function 构造函数标记为创建对象。  
  
    ```javascript  
    var eng = new Engine();  
    ```  
  
- 在下一步的行中，键入对象和要显示字段的 IntelliSense 信息的段的名称。  
  
    ```javascript  
    eng.  
    ```  
  
### <a name="to-create-xml-documentation-comments-for-an-overloaded-function"></a>若要创建 XML 文档注释的重载函数  
  
1. 在函数中，添加[\<签名 >](../ide/signature-javascript.md)每个重载的元素。 在这些元素中添加其他元素，例如`<summary>`， `<param>`，和`<returns>`，前面带有三个斜杠标记 （/ /） 的每个元素。  
  
     下面的示例演示一个重载的 JavaScript 函数。 在此示例中，重载参数类型不同。  
  
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
  
2. 若要查看 XML 文档注释，请键入名称和标记使用 XML 文档注释，如以下示例所示的函数的左括号：  
  
    ```javascript  
    calc(  
    ```  
  
### <a name="to-create-localized-intellisense"></a>若要创建本地化的 IntelliSense  
  
1. 创建具有 OpenAjax MessageBundle 格式的文档注释的 XML 文件。  
  
    > [!IMPORTANT]
    > MessageBundle 是建议的格式。 在 Microsoft Ajax 或.winmd 文件中不支持此格式。 有关使用替代方法`VSDoc`格式，请参阅[ \<loc >](../ide/loc-javascript.md)。  
  
     下面的示例演示内容，其中包含本地化的 IntelliSense 信息挎斗文件中。 这是特定于区域性的文件夹，如 JA 中的 XML 文件。 文件夹必须位于与包含的.js 文件位于相同位置`<loc>`元素。 XML 文件的文件名称必须匹配`filename`参数中指定`<loc>`元素。  
  
    ```  
    <messagebundle>  
      <msg name="1">A class that represents a rectangle</msg>  
      <msg name="2">The length of the rectangle</msg>  
      <msg name="3">The height of the rectangle</msg>  
    </messagebundle>  
  
    ```  
  
2. 在.js 文件中，添加以下代码。 `<loc>`元素必须在任何脚本之前声明并遵循相同的使用情况规则`<reference>`元素。 有关详细信息，请参阅[JavaScript IntelliSense](../ide/javascript-intellisense.md)并[ \<loc >](../ide/loc-javascript.md)。  
  
    ```javascript  
    /// <loc filename="messageFilename.xml" format="messagebundle"/>  
  
    ```  
  
3. 在.js 文件中，添加的 XML 文档元素和默认说明。 设置`locid`属性值，以匹配相应`name`从挎斗文件属性值。 如果可用，本地化 IntelliSense 信息，将替换默认说明。  
  
    ```javascript  
    function add(a,b)   
    {  
        /// <summary locid='1'>description</summary>  
        /// <param name='a' locid='2'>parameter a description</param>  
        /// <param name='b' locid='3'>parameter b description</param>  
    }  
  
    ```  
  
4. 若要查看 XML 文档注释，请键入的名称和左括号的函数，如以下示例所示：  
  
    ```javascript  
    add(  
    ```  
  
## <a name="see-also"></a>请参阅  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)   
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)   
 [NIB：演练：在 ASP.NET 中的 JavaScript IntelliSense](https://msdn.microsoft.com/4f6e0cc2-7f48-4dbf-abb0-7fb743a2d05b)
