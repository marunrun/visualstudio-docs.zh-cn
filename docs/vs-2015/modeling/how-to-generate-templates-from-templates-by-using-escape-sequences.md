---
title: 如何：使用转义序列从模板生成模板 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, generating templates from templates
ms.assetid: 4126156a-7cea-48b8-925e-7790806cfe6c
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 501b7f040cb841d19c06ccc8fe7615a5b4a5e70d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657350"
---
# <a name="how-to-generate-templates-from-templates-by-using-escape-sequences"></a>如何：使用转义序列从模板生成模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以创建一个文本模板，用于创建另一个文本模板作为其生成的文本输出。 为此，必须使用转义序列来描绘文本模板标记。 如果不使用转义序列，则生成的文本模板将具有预定义的含义。 有关在文本模板中使用转义序列的详细信息，请参阅 [在文本模板中使用转义序列](../modeling/using-escape-sequences-in-text-templates.md)。

### <a name="to-generate-a-text-template-from-within-a-text-template"></a>从文本模板内生成文本模板

- 使用反斜杠 (\\) 作为转义字符，为单独的文本模板文件中的指令、语句、表达式和类功能生成文本模板中所需的标记标记。

    ```
    \<#@ directive \#>
    \<# statement \#>
    \<#= expression \#>
    \<#+ classfeature \#>
    ```

## <a name="example"></a>示例
 下面的示例使用转义字符从文本模板生成文本模板。 `output`指令将目标文件类型设置为文本模板文件类型 ( tt) 。

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

 生成的文本输出为文本模板。

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
