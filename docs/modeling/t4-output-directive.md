---
title: T4 输出指令
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dfbe77f5b6e2bbda6a51d392c4dd16b079100e81
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856256"
---
# <a name="t4-output-directive"></a>T4 输出指令

在 Visual Studio 文本模板中`output`指令用于定义的文件扩展名和编码已转换文件。

 例如，如果你的 Visual Studio 项目包含名为的模板文件**MyTemplate.tt**其中包含以下指令：

 `<#@output extension=".cs"#>`

 Visual Studio 将生成名为的文件，然后**MyTemplate.cs**

 运行时（预处理）文本模板中不需要 `output` 指令。 相反，应用程序通过调用 `TextTransform()` 来获取已生成的字符串。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

## <a name="using-the-output-directive"></a>使用输出指令

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

 每个文本模板中不应该有多个 `output`。

## <a name="extension-attribute"></a>扩展属性
 指定生成的文本输出文件的文件扩展名。

 默认值是 **.cs**

 示例： `<#@ output extension=".txt" #>`

 `<#@ output extension=".htm" #>`

 `<#@ output extension=".cs" #>`

 `<#@ output extension=".vb" #>`

 可接受的值：任何有效的文件扩展名。

## <a name="encoding-attribute"></a>编码属性
 指定生成输出文件时要使用的编码。 例如：

 `<#@ output encoding="utf-8"#>`

 默认值为文本模板文件使用的编码。

 可接受的值： `us-ascii`

 `utf-16BE`

 `utf-16`

 `utf-8`

 `utf-7`

 `utf-32`

 `0`（系统默认）

 一般情况下，可以使用 WebName 字符串或 <xref:System.Text.Encoding.GetEncodings%2A?displayProperty=fullName> 返回的任一编码的 CodePage 编号。