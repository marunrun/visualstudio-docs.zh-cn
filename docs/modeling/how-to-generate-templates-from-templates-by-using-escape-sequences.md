---
title: 使用转义序列基于模板生成模板
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, generating templates from templates
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7872b9bf55ad5d712ac01edf10c4b9df2a82feea
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263682"
---
# <a name="how-to-generate-templates-from-templates-by-using-escape-sequences"></a>如何：使用转义序列基于模板生成模板
可以创建用于创建另一个文本模板，为其生成的文本输出的文本模板。 若要执行此操作，必须使用转义序列来描述文本模板标记。 如果不使用转义序列，生成的文本模板将具有预定义的含义。 有关在文本模板中使用转义序列的详细信息，请参阅[在文本模板中使用转义序列](../modeling/using-escape-sequences-in-text-templates.md)。

### <a name="to-generate-a-text-template-from-within-a-text-template"></a>若要生成从文本模板中的文本模板

- 使用反斜杠符号 (\\) 作为转义字符，以生成指令、 语句、 表达式、 文本模板中必需的标记和类中的单独的文本模板文件的功能。

    ```
    \<#@ directive \#>
    \<# statement \#>
    \<#= expression \#>
    \<#+ classfeature \#>
    ```

## <a name="example"></a>示例
 以下示例使用转义字符以生成文本模板中的文本模板。 `output`指令将目标文件类型设置为文本模板文件类型 (.tt)。

```csharp
\<#@ output extension=".tt" \#>
\<#@ assembly name="System.Xml.dll" \#>
\<#@ import namespace="System.Xml" \#>
\<#
XmlDocument xDoc = new XmlDocument();
//System.Diagnostics.Debugger.Break();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {\#>
           \<#= attr.Name \#>
       \<#}
     }
\#>
```

 生成的文本输出是一个文本模板。

```
<#@ output extension=".tt" #>
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>
<#
XmlDocument xDoc = new XmlDocument();
//System.Diagnostics.Debugger.Break();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {#>
           <#= attr.Name #>
       <#}
     }
#>
```