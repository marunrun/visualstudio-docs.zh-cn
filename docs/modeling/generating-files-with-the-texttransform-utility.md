---
title: 使用 TextTransform 实用工具生成文件
ms.date: 07/26/2019
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ec659bfee9253dfb198c2747e1b5d7fb6b78f2b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596549"
---
# <a name="generate-files-with-the-texttransform-utility"></a>使用 TextTransform 实用工具生成文件

TextTransform.exe 是一个命令行工具，可用于转换文本模板。 当调用 TextTransform.exe 时，作为自变量指定的文本模板文件的名称。 TextTransform.exe 调用文本转换引擎，并处理文本模板。 TextTransform.exe 通常通过脚本调用。 但是，它不通常必需的因为您可以在 Visual Studio 中或在生成过程中执行文本转换。

> [!NOTE]
> 如果你想要将文本转换作为生成过程的一部分，请考虑使用 MSBuild 文本转换任务。 有关详细信息，请参阅[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。 在计算机中安装了 Visual Studio，还可以编写的应用程序或可以转换文本模板的 Visual Studio 扩展。 有关详细信息，请参阅[通过使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)。

TextTransform.exe 位于以下目录中：

::: moniker range=">=vs-2019"

**\Program Files （x86） \Microsoft Visual Studio\2019\Professional\Common7\IDE**

对于专业版，或

**\Program Files （x86） \Microsoft Visual Studio\2019\Enterprise\Common7\IDE**

适用于 Enterprise edition。

::: moniker-end

::: moniker range="vs-2017"

**\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\IDE**

对于专业版，或

**\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE**

适用于 Enterprise edition。

在以前版本的 Visual Studio 中，在以下位置找到该文件：

**\Program Files (x86)\Common Files\Microsoft Shared\TextTemplating\{version}**

其中 {version} 取决于安装以前版本。

::: moniker-end

## <a name="syntax"></a>语法

```
TextTransform [<options>] <templateName>
```

### <a name="parameters"></a>参数

|**参数**|**描述**|
|-|-|
|`templateName`|标识你想要转换的模板文件的名称。|

|**选项**|**描述**|
|-|-|
|**-out** \<filename>|转换的输出写入到该文件。|
|**-r** \<assembly>|用于编译和运行文本模板使用的程序集。|
|**-u** \<namespace>|用于编译模板命名空间。|
|**-I** \<includedirectory>|包含指定的文本模板中包括的文本模板的目录。|
|**-P** \<referencepath >|一个目录来搜索的文本模板中指定的程序集或使用 **-r**选项。<br /><br /> 例如，若要包括用于 Visual Studio API 的程序集，使用<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName>!\<className>!\<assemblyName&#124;codeBase>|名称、 完整类型名称和程序集可用于处理文本模板中的自定义指令的指令处理器。|
|**-a** [processorName]![directiveName]!\<parameterName>!\<parameterValue>|指定参数值为指令处理器。 如果指定只是参数名称和值，该参数将可供所有指令处理器。 如果指定的指令处理器，该参数是仅供在指定的处理器。 如果指定指令的名称，仅当正在处理在指定的指令参数才可用。<br /><br /> 若要访问指令处理器或文本模板的参数值，使用[ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\))。 在文本模板中，包括`hostspecific`模板指令中，并在调用消息`this.Host`。 例如：<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`。<br /><br /> 始终键入 ！ 标记，即使省略可选的处理器和指令的名称。 例如：<br /><br /> `-a !!param!value`|
|**-h**|提供帮助。|

## <a name="related-topics"></a>相关主题

|任务|主题|
|-|-|
|在 Visual Studio 解决方案中生成文件。|[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|编写指令处理器转换自己的数据源。|[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)|
|编写文本模板化主机，您可以调用自己的应用程序从文本模板。|[使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)|
