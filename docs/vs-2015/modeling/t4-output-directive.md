---
title: T4 输出指令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 03a14993-47ad-4f2e-8032-57db28d5842a
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 149370bfee1b142876dff881625d08083afadea4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652316"
---
# <a name="t4-output-directive"></a>T4 输出指令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 文本模板中，`output` 指令用于定义转换文件的文件扩展名和编码。

 例如，如果 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目包含名为**MyTemplate.tt**的模板文件，其中包含以下指令：

 `<#@output extension=".cs"#>`

 然后 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会生成一个名为**MyTemplate.cs**的文件

 运行时（预处理）文本模板中不需要 `output` 指令。 相反，应用程序通过调用 `TextTransform()` 来获取已生成的字符串。 有关详细信息，请参阅[带有 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

## <a name="using-the-output-directive"></a>使用输出指令

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

 每个文本模板中不应该有多个 `output`。

## <a name="extension-attribute"></a>extension 特性
 指定生成的文本输出文件的文件扩展名。

 默认值为 **.cs**

 示例： `<#@ output extension=".txt" #>`

 `<#@ output extension=".htm" #>`

 `<#@ output extension=".cs" #>`

 `<#@ output extension=".vb" #>`

 可接受的值：任何有效的文件扩展名。

## <a name="encoding-attribute"></a>编码属性
 指定生成输出文件时要使用的编码。 例如:

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
