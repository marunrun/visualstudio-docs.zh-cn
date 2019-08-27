---
title: 如何使用文本模板...|Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: d1ac2509-0479-47eb-809c-1f171245d0b6
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9c31e1d17137fd0e801bb506c280a83285c311b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68181577"
---
# <a name="how-to--with-text-templates"></a>如何：使用文本模板 ...
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

中的文本模板[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]有用的方式生成任何类型的文本。 可以使用文本模板生成文本，在你的应用程序的一部分运行时和在设计时生成的某些项目代码。 本主题总结了最常要求"如何实现...？" 问题。  
  
 本主题中的前面使用项目符号的多个答案是替代建议。  
  
 有关文本模板的常规介绍，请阅读[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。  
  
## <a name="how-to-"></a>如何。  
  
### <a name="generate-part-of-my-application-code"></a>生成我的应用程序代码的一部分  
 我有一个配置或*模型*文件或数据库中。 我的代码的一个或多个部件依赖于该模型。  
  
- 从文本模板生成的某些代码文件。 有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)并[若要开始编写模板的最佳方法是什么？](#starting)。  
  
### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>在运行时，将数据传递到模板生成文件  
 在运行时，我的应用程序生成文本文件，例如包含混合使用标准文本和数据的报表。 我想要避免编写数百个`write`语句。  
  
- 将运行时文本模板添加到你的项目。 此模板创建在代码中，可以实例化和用于生成文本的类。 在构造函数参数，可以将数据传递给它。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。  
  
- 如果你想要从仅在运行时提供的模板生成，可以使用标准文本模板。 如果你正在编写[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展，可以调用文本模板化服务。 有关详细信息，请参阅[VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。 在其他上下文中，可以使用文本模板化引擎。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> 。  
  
     使用\<#@parameter#> 指令将参数传递给这些模板。 有关详细信息，请参阅[T4 参数指令](../modeling/t4-parameter-directive.md)。  
  
### <a name="read-another-project-file-from-a-template"></a>从模板中读取另一个项目文件  
 若要读取从同一个文件[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]作为模板的项目：  
  
- 将 `hostSpecific="true"` 插入 `<#@template#>` 指令。  
  
     在代码中，使用`this.Host.ResolvePath(filename)`来获取该文件的完整路径。  
  
### <a name="invoke-methods-from-a-template"></a>调用模板中的方法  
 如果方法中已存在，例如，标准[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]类：  
  
- 使用\<#@assembly#> 指令来加载该程序集，并使用\<#@import#> 若要设置的命名空间上下文。 有关详细信息，请参阅[T4 导入指令](../modeling/t4-import-directive.md)。  
  
   如果您经常使用一组相同的程序集并导入指令，应考虑编写指令处理器。 在每个模板，可以调用指令处理器，它可以加载这些程序集和模型文件和设置的命名空间上下文。 有关详细信息，请参阅[创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)。  
  
  如果你要自行编写方法：  
  
- 如果你正在编写运行时文本模板，编写一个具有与运行时文本模板相同的名称的分部类定义。 添加到此类的其他方法。  
  
- 编写类功能控制块`<#+ ... #>`在方法、 属性和私有类可以声明的其中。 编译时文本模板，它将转换为一个类。 标准控制块`<#...#>`和文本转换为单个的方法和类功能块插入作为单独的成员。 有关详细信息，请参阅[文本模板控制块](../modeling/text-template-control-blocks.md)。  
  
   定义为类功能还可以包含嵌入的文本块的方法。  
  
   请考虑将类功能放在单独的文件，您可以`<#@include#>`到一个或多个模板文件。  
  
- 在单独的程序集 （类库） 中编写方法，并从你的模板调用它们。 使用`<#@assembly#>`加载的程序集的指令和`<#@import#>`设置命名空间上下文。 请注意，以便在调试时，重新生成程序集，可能必须停止并重新启动[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 有关详细信息，请参阅[T4 文本模板指令](../modeling/t4-text-template-directives.md)。  
  
### <a name="generate-many-files-from-one-model-schema"></a>从一个模型架构生成多个文件  
 如果您经常从具有相同的 XML 或数据库架构的模型生成文件：  
  
- 应考虑编写指令处理器。 这使您以将程序集的多个语句和导入语句中使用单个自定义指令的每个模板。 指令处理器还可以加载和分析的模型文件。 有关详细信息，请参阅[创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)。  
  
### <a name="generate-files-from-a-complex-model"></a>从复杂的模型生成文件  
  
- 请考虑创建域特定语言 (DSL) 来表示该模型。 这使得它更容易编写模板，因为你使用类型和属性，以反映您的模型中的元素的名称。 无需分析文件或导航 XML 节点。 例如：  
  
     `foreach (Book book in this.Library) { ... }`  
  
     有关详细信息，请参阅[域特定语言入门](../modeling/getting-started-with-domain-specific-languages.md)并[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。  
  
- 请考虑从 UML 模型生成代码。 代码无需直接反映 UML。 例如，无需在 UML 模型中生成的每个类的类。 相反，可以使用 UML 类图来表示一个网站，并从每个 UML 类生成一个网页。 选择最符合您需要的关系图类型。 例如，选择活动图来表示任何类型的工作流。 您可以定义构造型来添加适合于每种类型的元素为应用程序的信息。  
  
     从 UML 模型生成，可绘制和编辑图表形式，但无需设计自己的关系图类型，就像使用 DSL 的模型。  
  
     有关详细信息，请参阅[为您的应用程序创建模型](../modeling/create-models-for-your-app.md)并[从 UML 模型生成文件](../modeling/generate-files-from-a-uml-model.md)。  
  
### <a name="get-data-from-includevsprvsincludesvsprvs-mdmd"></a>从中获取数据 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  
 若要使用中提供的服务[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，由组`hostSpecific`特性并加载`EnvDTE`程序集。 例如:  
  
```csharp  
<#@ template hostspecific="true" language="C#" #>  
<#@ output extension=".txt" #>  
<#@ assembly name="EnvDTE" #>  
<#  
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;  
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetService(typeof(EnvDTE.DTE));  
#>  
  
Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>  
  
```  
  
### <a name="execute-text-templates-in-the-build-process"></a>在生成过程中执行文本模板  
  
- 有关详细信息，请参阅[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。  
  
## <a name="more-general-questions"></a>更多常规问题  
  
### <a name="starting"></a> 若要开始编写文本模板的最佳方法是什么？  
  
1. 写入生成的文件的具体示例。  
  
2. 将其转换文本模板的方法是插入`<#@template #>`指令，和的指令和代码所需加载模型的输入的文件。  
  
3. 渐进式文件的部分将替换为表达式和代码块。  
  
### <a name="what-is-a-model"></a>"模型"是什么？  
  
- 通过在模板读取的输入。 它可能是在文件中或在数据库中。 XML 或 Visio 绘图，或特定于域的语言 (DSL) 或 UML 模型中，可能会也可能是纯文本。 它可以分布在多个文件。 通常，多个模板读取一个模型。  
  
     "模型"一词的含义是业务的，它表示您更直接地比生成的程序代码或其他文件的某些方面。 例如，它可能表示你生成的软件将监督通信网络的计划。  
  
### <a name="what-is-the-benefit-of-using-text-templates"></a>使用文本模板的优点是什么？  
 通常情况下，您从一个模型生成多个代码或其他文件。 模型比生成的代码更能直接表示要求。 它省略实现详细信息，并以要求，而不是代码形式编写。 在需求变化 – 它们通常所执行的操作 – 时可以更新的模型，更轻松、 更可靠地就比程序代码的不同部分。  
  
 代码生成，因此从敏捷开发方法的角度来看一个重要的工具。  
  
### <a name="what-best-practices-are-there-for-text-templates"></a>"最佳实践"还有哪些文本模板的？  
  
- 有关详细信息，请参阅[T4 文本模板编写准则](../modeling/guidelines-for-writing-t4-text-templates.md)。  
  
### <a name="what-is-t4"></a>什么是"T4"？  
  
- 另一个名称[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]此处所述的文本模板功能。 未发布的上一个版本是"文本模板转换"的缩写词。
