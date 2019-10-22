---
title: 使用自定义宿主处理文本模板
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 171eb8810d74df5c1058ba055e598d04f9164633
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658288"
---
# <a name="process-text-templates-by-using-a-custom-host"></a>使用自定义主机处理文本模板

*文本模板转换*过程会将*文本模板*文件作为输入，并生成一个文本文件作为输出。 你可以从 Visual Studio 扩展或在安装了 Visual Studio 的计算机上运行的独立应用程序调用文本转换引擎。 但是，必须提供*文本模板化宿主*。 该类将模板连接到环境，查找资源（如程序集和包含文件），并处理输出和错误消息。

> [!TIP]
> 如果正在编写将在 Visual Studio 中运行的包或扩展，请考虑使用文本模板化服务，而不是编写自己的主机。 有关详细信息，请参阅[在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

> [!NOTE]
> 不建议在服务器应用程序中使用文本模板转换。 除非是在单个线程中，否则不建议使用文本模板转换。 这是因为文本模板化引擎可以重用单个 AppDomain，以便转换、编译和执行模板。 转换的代码未被设计为线程安全的。 引擎旨在按顺序处理文件，因为这些文件在设计时位于 Visual Studio 项目中。
>
> 对于运行时应用程序，请考虑使用预处理文本模板：请参阅使用[T4 文本模板生成运行时文本](../modeling/run-time-text-generation-with-t4-text-templates.md)。

如果应用程序使用一组在编译时固定的模板，使用预处理文本模板会更为简单。 如果你的应用程序将在未安装 Visual Studio 的计算机上运行，你还可以使用该方法。 有关详细信息，请参阅[带有 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

## <a name="execute-a-text-template-in-your-application"></a>在应用程序中执行文本模板

若要执行文本模板，可以调用 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> 的 ProcessTemplate 方法。

```csharp
using Microsoft.VisualStudio.TextTemplating;
...
Engine engine = new Engine();
string output = engine.ProcessTemplate(templateString, host);
```

 应用程序必须找到并提供模板，并且必须处理输出。

 在 `host` 参数中，必须提供实现[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))的类。 这是由引擎回调的。

 宿主必须能记录错误、解析对程序集和包含文件的引用、提供可在其中执行模板的应用程序域并为每条指令调用相应的处理器。

 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> 是在 **Microsoft.VisualStudio.TextTemplating.\*0.dll 中定义的。** [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) 是在 **Microsoft.VisualStudio.TextTemplating.Interfaces\*0.dll**中定义的。

## <a name="in-this-section"></a>本节内容
 [演练：创建自定义文本模板宿主](../modeling/walkthrough-creating-a-custom-text-template-host.md)说明如何创建自定义文本模板宿主，使文本模板功能在 Visual Studio 外部可用。

## <a name="reference"></a>参考
 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))

## <a name="related-sections"></a>相关章节

- [文本模板转换过程](../modeling/the-text-template-transformation-process.md)描述文本转换的工作方式，以及可以自定义的部分。
- [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)提供文本模板指令处理器的概述。