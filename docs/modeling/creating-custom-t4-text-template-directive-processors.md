---
title: 创建自定义 T4 文本模板指令处理器
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 836e2c24d9f236c7b87dfff60b934221b7645f1b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654066"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>创建自定义 T4 文本模板指令处理器

*文本模板转换过程*会将*文本模板*文件作为输入，并生成一个文本文件作为输出。 *文本模板转换引擎*控制进程，引擎与文本模板转换主机和一个或多个文本模板*指令处理器*进行交互以完成该过程。 有关详细信息，请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

若要创建自定义指令处理器，需要创建一个从 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 继承的类。

这两者之间的区别在于 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 实现从用户获取参数所必需的最小接口，并生成生成模板输出文件的代码。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 实现 "需要/提供" 设计模式。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 处理两个特殊参数 `requires` 和 `provides`。  例如，自定义指令处理器可能会接受来自用户的文件名称，打开并读取文件，然后将该文件的文本存储在名为 `fileText` 的变量中。 @No__t_0 类的子类可能会将用户的文件名用作 `requires` 参数的值，并将该文本作为 `provides` 参数的值存储在其中的变量的名称。 此处理器将打开并读取文件，然后将该文件的文本存储在指定的变量中。

在 Visual Studio 中从文本模板调用自定义指令处理器之前，必须对其进行注册。

有关如何添加注册表项的详细信息，请参阅[部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)。

## <a name="custom-directives"></a>自定义指令

自定义指令如下所示：

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

如果要从文本模板访问外部数据或资源，则可以使用自定义指令处理器。

不同文本模板可以共享单个指令处理器提供的功能，因此指令处理器提供了一种方法来重新使用代码。 内置 `include` 指令类似，因为可以使用它来分解代码，并在不同的文本模板之间共享代码。 不同之处在于 `include` 指令提供的任何功能都是固定的，不接受参数。 如果要为文本模板提供通用功能并允许模板传递参数，则必须创建自定义指令处理器。

自定义指令处理器的一些示例可以是：

- 指令处理器，用于从接受用户名和密码作为参数的数据库返回数据。

- 指令处理器，用于打开和读取接受文件名称作为参数的文件。

### <a name="principal-parts-of-a-custom-directive-processor"></a>自定义指令处理器的主体部分

若要开发指令处理器，您必须创建一个继承自 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 的类。

必须实现的最重要的 `DirectiveProcessor` 方法如下所示。

- `bool IsDirectiveSupported(string directiveName)`-如果指令处理器可处理命名指令，则返回 `true`。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)`-模板引擎为模板中的指令的每个匹配项调用此方法。 处理器应保存结果。

调用 ProcessDirective （）后，模板化引擎将调用以下方法：

- `string[] GetReferencesForProcessingRun()`-返回模板代码所需的程序集的名称。

- `string[] GetImportsForProcessingRun()`-返回可在模板代码中使用的命名空间。

- `string GetClassCodeForProcessingRun()`-返回模板代码可使用的方法、属性和其他声明的代码。 执行此操作的最简单方法是生成包含C#或 Visual Basic 代码的字符串。 若要使指令处理器能够从使用任意 CLR 语言的模板调用，可以将语句构造为一个 CodeDom 树，然后返回按模板所使用的语言对树进行序列化的结果。

- 有关详细信息，请参阅[演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)。

## <a name="see-also"></a>请参阅

- [部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)介绍了如何注册自定义指令处理器。
- [演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)介绍了如何创建自定义指令处理器，如何注册和测试指令处理器，以及如何将输出文件的格式设置为 HTML。