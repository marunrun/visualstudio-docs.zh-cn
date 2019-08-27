---
title: 创建自定义 T4 文本模板指令处理器
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f9d514178e4b899ca727e17ead260719697b562
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476639"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>创建自定义 T4 文本模板指令处理器

*文本模板转换过程*采用*文本模板*文件作为输入并生成一个文本文件作为输出。 *文本模板转换引擎*控件与文本模板转换主机和一个或多个文本模板过程中和引擎进行交互*指令处理器*完成过程。 有关详细信息，请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

若要创建自定义指令处理器，需要创建一个从 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 继承的类。

这两个区别在于<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor>实现最小值是从用户获取参数以及生成的代码，将生成模板输出文件所必需的接口。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 实现要求/提供设计模式。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 处理两个特殊参数`requires`和`provides`。  例如，自定义指令处理器可能会接受来自用户打开的文件名称和读取该文件，，然后将该文件的文本存储在变量中，名为`fileText`。 子类<xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>类可能的值作为用户需要文件名称`requires`参数，并在其中将文本存储的值为变量的名称`provides`参数。 此处理器将打开并读取该文件，然后将该文件的文本存储在指定的变量。

从 Visual Studio 中的文本模板调用自定义指令处理器之前，必须注册它。

有关如何添加注册表项的详细信息，请参阅[部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)。

## <a name="custom-directives"></a>自定义指令

自定义的指令如下所示：

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

当你想要从文本模板访问外部数据或资源时，可以使用自定义指令处理器。

不同的文本模板可以共享单个指令处理器提供的功能，因此指令处理器提供一种方法来分解代码以供重复使用。 内置`include`指令非常相似，因为可以使用它来分解代码，并在不同的文本模板之间进行共享。 不同之处在于任何功能的`include`指令提供固定的不接受参数。 如果你想要提供文本模板的常用功能，并允许将参数传递的模板，则必须创建自定义指令处理器。

可以自定义指令处理器的一些示例：

- 若要从作为参数接受用户名和密码的数据库中返回的数据指令处理器。

- 打开和读取文件的指令处理器作为参数接受的文件的名称。

### <a name="principal-parts-of-a-custom-directive-processor"></a>自定义指令处理器的主体部分

若要开发指令处理器，必须创建从继承的类<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor>或<xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>。

最重要`DirectiveProcessor`必须实现的方法如下所示。

- `bool IsDirectiveSupported(string directiveName)` -返回`true`如果指令处理器可以处理通过命名指令。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` 模板引擎调用此方法对每个模板中的指令。 您的处理器应该保存结果。

之后所有调用了 Processdirective 的模板化引擎将调用这些方法：

- `string[] GetReferencesForProcessingRun()` -返回的模板代码需要的程序集的名称。

- `string[] GetImportsForProcessingRun()` -返回可用的命名空间中的模板代码。

- `string GetClassCodeForProcessingRun()` -返回代码的方法、 属性和模板代码可以使用其他声明。 若要执行此操作的最简单方法是构建包含 C# 或 Visual Basic 代码的字符串。 若要使能够从使用任何 CLR 语言的模板调用指令处理器，您可以将语句构造为 CodeDom 树，然后返回序列化该模板使用的语言中的树的结果。

- 有关详细信息，请参见[演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)。

## <a name="see-also"></a>请参阅

- [部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)说明如何注册自定义指令处理器。
- [演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)介绍如何创建自定义指令处理器、 如何注册和测试指令处理器，以及如何将输出文件格式化为 HTML。