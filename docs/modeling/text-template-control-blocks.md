---
title: 文本模板控制块
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, template code
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3a3396caf4f1ade860f4727095d3305d86e837c3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434174"
---
# <a name="text-template-control-blocks"></a>文本模板控制块
控制块可使你在文本模板中编写代码以便改变输出。 有三种类型的控制块，通过其左大括号来区分：

- `<# Standard control blocks #>` 可以包含语句。

- `<#= Expression control blocks #>` 可以包含表达式。

- `<#+ Class feature control blocks #>` 可以包含方法、字段和属性。

## <a name="standard-control-block"></a>标准控制块
 标准控制块包含语句。 例如，下面的标准块可获取 XML 文档中所有特性的名称：

```
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>

<#
    List<string> allAttributes = new List<string>();
    XmlDocument xDoc = new XmlDocument();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes.Count > 0)
    {
       foreach (XmlAttribute attr in attributes)
       {
           allAtributes.Add(attr.Name);
       }
     }
#>
```

 你可以将纯文本嵌入到复合语句中，例如 `if` 或 `for`。 例如，此片段会在每个循环迭代中生成输出行：

```
<#
       foreach (XmlAttribute attr in attributes)
       {
#>
Found another one!
<#
           allAtributes.Add(attr.Name);
       }
#>
```

> [!WARNING]
> 始终使用 {...} 若要分隔包含嵌入的纯文本的嵌套的语句。 以下示例可能无法正常工作：
>
> `<# if (ShouldPrint) #> Some text. -- WRONG`
>
> 相反，应包括 {大括号}，如下所示：

```

<#
 if (ShouldPrint)
 {   //  "{" REQUIRED
#>
Some text.
<#
 }
#>
```

## <a name="expression-control-block"></a>表达式控制块
 表达式控制块用于某类代码，该代码提供要写入到输出文件的字符串。 例如，在上述示例中，你可以通过修改代码块将特性名称打印到输出文件，如下所示：

```
<#
    XmlDocument xDoc = new XmlDocument();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {
#><#= attr.Name #><#
       }
    }
#>
```

## <a name="class-feature-control-block"></a>类功能控制块
 你可以使用类功能控制块将方法、属性、字段或甚至嵌套的类添加到文本模板。 类功能块的最常见用途是，为文本模板的其他部分的代码提供帮助程序函数。 例如，以下类功能块会将特性名称的首字母大写（或者，如果名称包含空格，则会将每个单词的首字母大写）：

```
<#@ import namespace="System.Globalization" #>
```

```
<#+
    private string FixAttributeName(string name)
    {
        return CultureInfo.CurrentCulture.TextInfo.ToTitleCase(name);
    }
#>
```

> [!NOTE]
> 类功能控制块的后面一定不能跟相同模板文件中的标准控制块。 但是，此限制并不适用于使用 `<#@include#>` 指令的结果。 每个包含的文件都可以具有后跟类功能块的标准块。

 你可以通过将文本和表达式块嵌入到类功能控制块来创建生成输出的函数。 例如：

```
<#+
    private void OutputFixedAttributeName(string name)
    {
#>
 Attribute:  <#= CultureInfo.CurrentCulture.TextInfo.ToTitleCase(name) #>
<#+  // <<< Notice that this is also a class feature block.
    }
#>
```

 你可以从标准块或从其他类功能块调用此函数：

```
<# foreach (Attribute attribute in item.Attributes)
{
  OutputFixedAttributeName(attribute.Name);
}
#>
```

## <a name="how-to-use-control-blocks"></a>如何使用控制块
 将单个模块中所有标准和表达式控制块中的所有代码（包括包含模板中的所有代码）组合在一起，以便形成所生成代码的 `TransformText()` 方法。 (有关包括与其他文本模板的详细信息`include`指令，请参阅[T4 文本模板指令](../modeling/t4-text-template-directives.md)。)

 在使用控制块时，请记住考虑以下事项：

- **语言。** 你可以使用文本模板中的 C# 或 Visual Basic 代码。 默认语言为 C#，但你可以使用 `template` 指令的 `language` 参数指定 Visual Basic。 (有关详细信息`template`指令，请参阅[T4 文本模板指令](../modeling/t4-text-template-directives.md)。)

     控制块中使用的语言与文本模板中生成的文本的语言或格式无关。 你可以使用 Visual Basic 代码生成 C#，反之亦然。

     在给定的文本模板（包括使用 `include` 指令包含的所有文本模板）中只能使用一种语言。

- **本地变量。** 由于文本模板中标准和表达式控制块中的所有代码合并生成了一个单独的方法，因此，应确保不与局部变量的名称发生冲突。 如果包含其他文本模板，则必须确保变量名称在所有包含的模板中是唯一的。 要确保这种情况，可以将字符串添加到每个局部变量名称，该名称标识在其中进行声明的文本模块。

     当你对局部变量进行声明时，尤其是当包括多个文本模板时，将局部变量初始化为合理的值也是一种不错的方法。

- **嵌套控制块。** 控制块之间可能无法相互嵌套在各自内部。 在打开另一个控制块之前，必须始终终止给定的控制块。 例如，下面的示例演示了如何将表达式块中的部分文本作为标准控制块的一部分打印。

    ```
    <#
    int x = 10;
    while (x-- > 0)
    {
    #>
    <#= x #>
    <# } #>
    ```

- **重构。** 为了使你的文本模板简短并易于理解，强烈建议你避免重复代码，可通过将可重用的代码分解到类功能块中的帮助程序函数或通过创建你自己的文本模板类（继承自 Microsoft.VisualStudio.TextTemplating.TextTransformation 类）实现。