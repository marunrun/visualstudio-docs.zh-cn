---
title: 工作区和 Visual Studio 中的语言服务 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 2893ae2bcd70ff317ba799fea6cfd2751c685731
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952687"
---
# <a name="workspaces-and-language-services"></a>工作区和语言服务

语言服务可以提供[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)用户相同的丰富的语言功能它们是用于在使用解决方案和项目。 自激活语言服务，可能会根据文件扩展名或打开文档的内容，但此"松散文件"语言服务仅限于语法突出显示。 所需的其他信息以编辑/查看源代码时提供更丰富的体验。 每个语言服务已初始化为其自身 API 文档的此额外的上下文数据。 这通常是由紧密耦合到语言服务和生成系统的项目系统进行管理。

## <a name="initialization"></a>初始化

在中[工作区](workspaces.md)，语言服务由初始化<xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider>扩展点，仅在该语言服务中专门一无所知生成创作。 在这种方式，语言服务所有者可以维护单个打开文件夹 （例如 MSBuild，生成文件等） 在生成期间运行其编译器的文件夹和文件中存在任何多少模式扩展。 当磁盘上更改了的文件从其创建的文件上下文并刷新文件上下文时，语言服务提供程序将通知的更新的文件上下文集。 语言服务提供商然后可以更新其模型。

当在编辑器中打开文档时，Visual Studio 只考虑语言需要可以为其找到匹配的文件上下文提供程序的文件上下文类型的服务提供程序。 它然后将传递的文件上下文从匹配的提供程序到所选的语言服务提供商通过`ILanguageServiceProvider.InitializeAsync`。 语言服务提供程序文件的上下文数据是语言服务提供程序的实现细节，但预期的用户体验是为此提供更丰富的语言服务的对待打开的文档。

## <a name="using-ilanguageserviceprovider"></a>使用 ILanguageServiceProvider

使用创建的文件上下文时，将会通知语言服务`ContextType`相匹配的一个`SupportedContextTypes`语言 server 的值将导出的属性。

若要支持的语言服务，将需要一个扩展：

- 一个唯一`Guid`。 这将用于`SupportedContextTypes`属性的参数并在`FileContext`对象。
- 语言文件上下文
  - 提供程序工厂
    - `ExportFileContextProviderAttribute` 与上述属性生成的唯一`Guid`中 `SupportedContextTypes`
    - 实现 `IWorkspaceProviderFactory<IFileContextProvider>`
  - 提供程序实现 `IFileContextProvider.GetContextsForFileAsync`
    - 构造一个新`FileContext`与`contextType`作为唯一生成的构造函数参数 `Guid`
    - 使用`Context`属性的`FileContext`为提供的其他数据 `ILanguageServiceProvider`
- 语言服务
  - 提供程序工厂
    - `ExportLanguageServiceProvider` 与上述属性生成的唯一`Guid`中 `SupportedContextTypes`
    - 实现 `IWorkspaceProviderFactory<ILanguageServiceProvider>`
  - 提供程序
    - 实现 `ILanguageServiceProvider`
    - 使用`ILanguageServiceProvider.InitializeAsync`以便在打开文件时提供的参数的语言服务
    - 使用`ILanguageServiceProvider.UninitializeAsync`若要禁用文件关闭时提供的参数的语言服务

>[!WARNING]
>`ILanguageServiceProvider`可能由工作区在主线程上调用方法。 请考虑将安排在另一个线程以避免引入 UI 将延迟的工作。

## <a name="language-server-protocol"></a>语言服务器协议

`Microsoft.VisualStudio.Workspace.*` Api 不使语言服务中打开文件夹的唯一方法。 另一种方法是使用语言服务器。 详细信息，请阅读有关[语言服务器协议](language-server-protocol.md)。

## <a name="related-interfaces"></a>相关的接口

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> 打开或关闭以进行编辑文件类型匹配的文件时调用。

## <a name="next-steps"></a>后续步骤

* [工作区生成](workspace-build.md)-打开文件夹支持构建如 MSBuild 和生成文件系统。