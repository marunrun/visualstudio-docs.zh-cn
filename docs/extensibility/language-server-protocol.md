---
title: 语言服务器协议概述 |Microsoft Docs
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 6a7d93c2-31ea-4bae-8b29-6988a567ddf2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8f6f114d7165b85051092234ea33dfc7f73e1487
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309623"
---
# <a name="language-server-protocol"></a>语言服务器协议

## <a name="what-is-the-language-server-protocol"></a>什么是语言服务器协议？

支持丰富的编辑功能等源的代码自动完成或**转到定义**编辑器或 IDE 中的编程语言是传统上非常困难并花费较长时间。 通常需要编写编程语言的编辑器或 IDE 中的域模型 （扫描器、 分析器、 类型检查器、 生成器和的详细信息）。 例如，Eclipse CDT 插件，它提供对 C /C++在 Eclipse IDE 中用 Java 编写由于 Eclipse IDE 本身用 Java 编写。 按照此方法，则意味着实现 C /C++用于 Visual Studio Code，TypeScript 中的域模型和中的单独的域模型C#用于 Visual Studio。

创建特定于语言的域模型也是容易得多，如果一个开发工具，可以重复使用现有的特定于语言的库。 但是，这些库通常实现本身的编程语言 (例如，良好的 C /C++在 C 中实现域模型 /C++)。 集成了 C /C++到编辑器中编写的 TypeScript 库从技术上讲是可行的但艰巨的任务。

### <a name="language-servers"></a>语言服务器

另一种方法是在其自己的进程中运行库并使用进程间通信与它交互。 来回发送的消息形成一种协议。 语言服务器协议 (LSP) 是为标准的开发工具和语言服务器进程之间交换的消息的产品。 使用语言服务器或恶魔不是一个新的或新的想法。 编辑器，如 Vim 和 Emacs 一直在做这段时间，以提供语义的自动完成功能支持。 LSP 的目标是简化这种集成，并为公开的各种工具的语言功能提供了有用的框架。

具有一种常见协议允许到有条不紊地开发工具通过重复使用现有语言的域模型的实施，编程语言功能的集成。 语言服务器后端可以用 PHP、 Python 或 Java 编写并 LSP 允许它很容易集成到各种工具。 以便工具可以提供丰富的语言服务，而无需完全了解特定于底层的域模型的细微差别，常见的抽象级别工作原理协议。

## <a name="how-work-on-the-lsp-started"></a>启动的 LSP 上的工作方式

LSP 不断发展变化，并且立即在 3.0 版。 它启动时的语言服务器概念选取由 OmniSharp 提供丰富的编辑功能适用于 C#。 最初，OmniSharp HTTP 协议与 JSON 有效负载和使用已集成到多个编辑器包括[Visual Studio Code](https://code.visualstudio.com)。

大约在同一时间，Microsoft 开始适用于 TypeScript 语言，例如 Emacs 和 Sublime Text 的编辑器中支持 TypeScript 的想法。 在此实现中，编辑器通过 stdin/stdout 与 TypeScript 服务器进程进行通信，并将 JSON 有效负载灵感 V8 调试器协议的的请求和响应。 TypeScript 服务器已到 TypeScript Sublime 插件和 VS Code 集成的丰富的 TypeScript 编辑操作。

具有集成不同的语言的两个服务器之后, VS Code 团队开始进行探索编辑器和 Ide 中的一种常见语言服务器协议。 一种常见协议，若要创建的单语言版服务器，可以使用不同 ide 语言提供程序。 语言 server 使用者仅有一次实现协议的客户端。 这会导致双赢局面语言提供程序和语言使用者。

语言服务器协议开始使用 TypeScript 服务器，展开与灵感的 VS Code 语言 API 的更多语言功能使用的协议。 协议与 JSON RPC 提供支持远程调用由于其简单性和现有的库。

在 VS 代码文件的团队构建出原型通过实现多个响应 linter 语言服务器协议请求到要 lint （扫描），并返回检测到的警告和错误的一组。 目标是到要 lint 文件以在文档中，这意味着在编辑器会话期间，有许多语法检查请求的用户编辑。 若要使注册的服务器和运行，以便新的 linting 进程不需要为每个用户编辑启动道理。 实现多个 linter 服务器，包括 VS Code ESLint 和 TSLint 扩展。 这两个 linter 服务器同时在 TypeScript/JavaScript 中实现并在 Node.js 上运行。 它们共享一个库，实现协议的客户端和服务器的一部分。

## <a name="how-the-lsp-works"></a>LSP 的工作原理

语言服务器运行在其自己的进程，并通过 JSON RPC 使用的语言协议与服务器通信工具，例如 Visual Studio 或 VS Code。 语言服务器操作系统的专用进程中的另一个优点是避免了为单个进程模型相关的性能问题。 实际传输通道可以是 stdio、 套接字、 命名的管道或节点 ipc 如果以 Node.js 编写的客户端和服务器。

下面一个示例，用于一种工具和语言服务器通信的方式在例程期间编辑会话：

![lsp 数据流关系图](media/lsp-flow-diagram.png)

* **用户在该工具中打开文件 （也称为文档）** :该工具将通知语言服务器文档打开时 (textDocument/didOpen)。 从现在起，文档的内容方面的真相不再位于文件系统上，但保留在内存中的工具。

* **用户所做的编辑**:该工具将通知有关文档更改 (textDocument/didChange) 的服务器，该程序的语义信息更新语言服务器。 发生这种情况，如语言服务器分析该信息并通知包含检测到的错误和警告 (textDocument/publishDiagnostics) 的工具。

* **用户执行"转到定义"在编辑器中的符号**:该工具会发送包含两个参数的 textDocument/定义请求：（1） 的文档 URI，请转到定义请求初始化到服务器之前的位置 （2） 的文本位置。 服务器使用的文档 URI 和文档内部的符号的定义的位置做出响应。

* **在用户关闭文档 （文件）** :从工具，通知文档现在不再在内存中的当前内容是现在最新的文件系统上的语言服务器发送 textDocument/didClose 通知。

此示例说明了与编辑器功能，如"转到定义"，"查找所有引用"级别语言服务器协议的通信方式。 协议使用的数据类型是编辑器或 IDE 数据类型，如当前打开的文本文档和光标的位置。 在编程语言域模型通常提供抽象语法树和编译器符号 （例如，解析类型、 命名空间，...） 的级别不是数据类型。这大大简化了该协议。

现在让我们看一下更多详细信息中的 textDocument/定义请求。 下面是客户端工具和语言中的"转到定义"请求服务器之间的负载C++文档。

这是请求：

```json
{
    "jsonrpc": "2.0",
    "id" : 1,
    "method": "textDocument/definition",
    "params": {
        "textDocument": {
            "uri": "file:///p%3A/mseng/VSCode/Playgrounds/cpp/use.cpp"
        },
        "position": {
            "line": 3,
            "character": 12
        }
    }
}
```

这是响应：

```json
{
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
        "uri": "file:///p%3A/mseng/VSCode/Playgrounds/cpp/provide.cpp",
        "range": {
            "start": {
                "line": 0,
                "character": 4
            },
            "end": {
                "line": 0,
                "character": 11
            }
        }
    }
}
```

以前，在编辑器的级别，而不是编程语言模型级别的数据类型进行描述是语言服务器协议成功的原因之一。 要简单得多标准化文本文档 URI 或跨不同的编程语言标准化抽象语法树和编译器符号与光标位置。

当用户使用不同的语言时，VS Code 将通常开始每种编程语言的语言服务器。 下面的示例显示了用户对 Java 和 SASS 文件适用的位置的会话。

![java 和 sass](media/lsp-java-and-sass.png)

### <a name="capabilities"></a>功能

不是每个语言服务器可以支持的协议定义的所有功能。 因此，客户端和服务器宣布其支持的功能的一组通过功能。 例如，服务器公布，它可以处理 textDocument/定义请求，但它可能会处理工作区/symbol 请求。 同样，客户端可以宣布他们可提供即将保存之前保存文档，以便服务器可以计算要编辑的文档时自动设置格式的文本编辑的通知。

## <a name="integrating-a-language-server"></a>将语言 server 集成

与特定工具的语言服务器的实际集成不由语言服务器协议，并且仍为工具实现者。 某些工具以一般方式集成通过让的扩展，可以启动，与任何类型的语言服务器语言服务器。 其他人，例如 VS Code 中，创建每个语言服务器的自定义扩展插件，以便扩展是仍然能够提供一些自定义的语言功能。

若要简化语言服务器和客户端实现，有库或 Sdk 的客户端和服务器部件。 为不同的语言提供了这些库。 例如，没有[语言客户端 npm 模块](https://www.npmjs.com/package/vscode-languageclient)为了便于语言服务器集成到 VS Code 扩展，另一个[语言 server npm 模块](https://www.npmjs.com/package/vscode-languageserver)编写使用 Node.js 的语言服务器。 这是当前[列表](https://github.com/Microsoft/language-server-protocol/wiki/Protocol-Implementations)支持库。

## <a name="using-the-language-server-protocol-in-visual-studio"></a>使用 Visual Studio 中的语言服务器协议

* [添加语言服务器协议扩展](adding-an-lsp-extension.md)-了解如何将语言服务器集成到 Visual Studio。
