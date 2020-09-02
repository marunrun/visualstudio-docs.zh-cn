---
title: Visual Studio 中的工作区和语言服务 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 2893ae2bcd70ff317ba799fea6cfd2751c685731
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952687"
---
# <a name="workspaces-and-language-services"></a>工作区和语言服务

语言服务可以为 [打开的文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) 用户提供使用解决方案和项目时所用的相同丰富的语言功能。 尽管此 "松散文件" 语言服务仅限于语法突出显示，但语言服务可能基于打开文档的文件扩展名或内容自行激活。 若要在编辑/检查源代码时提供更丰富的体验，需要额外的信息。 每个语言服务都有自己的 API，用于使用文档的这一额外的上下文数据进行初始化。 这通常由项目系统管理，该系统与语言服务和生成系统紧密耦合。

## <a name="initialization"></a>初始化

在 [工作区](workspaces.md)中，语言服务由 <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> 仅在该语言服务中专用化的扩展点进行初始化，并且不知道生成创作的内容。 通过这种方式，语言服务所有者可以维护单个打开的文件夹扩展，无论文件夹和文件中有多少个模式，在生成 (例如 MSBuild、生成文件等 ) 中。 在磁盘上更改从中创建文件上下文的文件并刷新文件上下文时，语言服务提供程序将收到更新的文件上下文集的通知。 然后，语言服务提供程序可以更新其模型。

当在编辑器中打开文档时，Visual Studio 只会考虑需要文件上下文类型的语言服务提供程序，可以为其找到匹配的文件上下文提供程序。 然后，它会通过从匹配提供程序 (s) 将) 的文件 (上下文传递到选定的语言服务提供程序 `ILanguageServiceProvider.InitializeAsync` 。 语言服务提供程序对该文件上下文数据所做的操作是语言服务提供程序的实现细节，但预期的用户体验是该文档的更丰富的语言服务。

## <a name="using-ilanguageserviceprovider"></a>使用 ILanguageServiceProvider

当创建的文件上下文与 `ContextType` `SupportedContextTypes` 语言服务器导出属性的值之一匹配时，将通知语言服务。

若要支持语言服务，扩展将需要：

- 唯一的 `Guid` 。 这将用于 `SupportedContextTypes` 属性参数和 `FileContext` 对象中。
- 语言文件上下文
  - 提供程序工厂
    - `ExportFileContextProviderAttribute`具有以上唯一生成的属性 `Guid``SupportedContextTypes`
    - 实现 `IWorkspaceProviderFactory<IFileContextProvider>`
  - 的提供程序实现 `IFileContextProvider.GetContextsForFileAsync`
    - `FileContext`使用构造函数参数构造一个新生成的新 `contextType``Guid`
    - 使用 `Context` 的属性将 `FileContext` 其他数据添加到 `ILanguageServiceProvider`
- 语言服务
  - 提供程序工厂
    - `ExportLanguageServiceProvider`具有以上唯一生成的属性 `Guid``SupportedContextTypes`
    - 实现 `IWorkspaceProviderFactory<ILanguageServiceProvider>`
  - 提供程序
    - 实现 `ILanguageServiceProvider`
    - 用于在 `ILanguageServiceProvider.InitializeAsync` 打开文件时为提供的参数启用语言服务
    - `ILanguageServiceProvider.UninitializeAsync`当文件关闭时，使用为提供的参数禁用语言服务

>[!WARNING]
>此 `ILanguageServiceProvider` 方法可能会由主线程上的工作区调用。 请考虑在不同的线程上计划工作，以避免引入 UI 延迟。

## <a name="language-server-protocol"></a>语言服务器协议

`Microsoft.VisualStudio.Workspace.*`Api 不是在打开的文件夹中启用您的语言服务的唯一方法。 另一种方法是使用语言服务器。 有关详细信息，请参阅 [语言服务器协议](language-server-protocol.md)。

## <a name="related-interfaces"></a>相关接口

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> 当打开或关闭匹配文件类型的文件进行编辑时，将调用。

## <a name="next-steps"></a>后续步骤

* [工作区生成](workspace-build.md) -打开文件夹支持 MSBuild 和生成文件等生成系统。