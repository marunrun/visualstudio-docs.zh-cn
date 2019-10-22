---
title: 用 TextTransform 实用工具生成文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
ms.assetid: 06a48235-fe02-403e-a1cf-2ae70b4db62f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 18776795fdf693c855edd3f629d674089daaaebd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666098"
---
# <a name="generating-files-with-the-texttransform-utility"></a>使用 TextTransform 实用工具生成文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TextTransform 是一个命令行工具，可用于转换文本模板。 调用 TextTransform 时，请将文本模板文件的名称指定为参数。 TextTransform 调用文本转换引擎，并处理文本模板。 TextTransform 通常是从脚本中调用的。 不过，通常不需要这样做，因为您可以在 Visual Studio 中或在生成过程中执行文本转换。

> [!NOTE]
> 如果要在生成过程中执行文本转换，请考虑使用 "MSBuild 文本转换" 任务。 有关详细信息，请参阅[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。 在安装了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的计算机上，还可以编写可转换文本模板的应用程序或 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展。 有关详细信息，请参阅[使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)。

 TextTransform 位于以下目录中：

 **\Program Files\Common Files\Microsoft Shared\TextTemplating\11。0**

## <a name="syntax"></a>语法

```
TextTransform [<options>] <templateName>
```

#### <a name="parameters"></a>参数

|**参数**|**描述**|
|------------------|---------------------|
|`templateName`|标识要转换的模板文件的名称。|

|**选项**|**描述**|
|----------------|---------------------|
|**-out** \<filename >|转换的输出将写入的文件。|
|**-r** \<assembly >|用于编译和运行文本模板的程序集。|
|**-u** \<namespace >|用于编译模板的命名空间。|
|**-I** \<includedirectory >|包含指定文本模板中包含的文本模板的目录。|
|**-P** \<referencepath >|搜索在文本模板中指定的程序集或使用 **-r**选项的目录。<br /><br /> 例如，若要包括用于 Visual Studio API 的程序集，请使用<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName >！\<className >！\<assemblyName&#124;基本代码 >|指令处理器的名称、完整类型名称和程序集，可用于处理文本模板中的自定义指令。|
|**-a** [processorName]！[directiveName]!\<parameterName >！\<parameterValue >|指定指令处理器的参数值。 如果只指定参数名称和值，则参数将可用于所有指令处理器。 如果指定指令处理器，参数仅可用于指定的处理器。 如果指定指令名称，则只有在处理指定的指令时，此参数才可用。<br /><br />  在文本模板中，将 `hostspecific` 包含在模板指令中，并调用 `this.Host` 上的消息。 例如:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`<br /><br /> 始终键入 "！" 标记，即使省略可选的处理器和指令名称也是如此。 例如:<br /><br /> `-a !!param!value`|
|**-h**|提供帮助。|

## <a name="related-topics"></a>相关主题

|任务|主题|
|----------|-----------|
|在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中生成文件。|[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|编写指令处理器转换自己的数据源。|[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)|
|编写允许您从自己的应用程序调用文本模板的文本模板化主机。|[使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)|
