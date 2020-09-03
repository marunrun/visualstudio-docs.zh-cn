---
title: 语言服务器协议概述 |Microsoft Docs
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 6a7d93c2-31ea-4bae-8b29-6988a567ddf2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3bd5dce3cfb7022a8abb6397dc87b418144cbe1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80703105"
---
# <a name="language-server-protocol"></a>语言服务器协议

## <a name="what-is-the-language-server-protocol"></a>什么是语言服务器协议？

通常，支持丰富的编辑功能，如编辑器或 IDE 中的编程语言的源代码自动完成或 " **中转到定义** "。 通常需要在编辑器或 IDE 的编程语言中 (扫描器、分析器、类型检查器、生成器和更多) 编写域模型。 例如，在 Eclipse IDE 中提供对 C/c + + 的支持的 Eclipse CDT 插件是以 Java 编写的，因为 Eclipse IDE 本身是用 Java 编写的。 按照此方法，这意味着在 TypeScript for Visual Studio 代码中实现 C/c + + 域模型，并在 c # 中为 Visual Studio 实现一个单独的域模型。

如果开发工具可以重复使用现有的特定于语言的库，则创建语言特定的域模型还会容易得多。 不过，这些库通常在编程语言本身中实现 (例如，在 C/c + +) 中实现良好的 C/c + + 域模型。 从技术上讲，将 C/c + + 库集成到用 TypeScript 编写的编辑器中是可行的，但却很难。

### <a name="language-servers"></a>语言服务器

另一种方法是在库自身的进程中运行库，并使用进程间通信与之通信。 来回发送的消息形成了一个协议。 语言服务器协议 (LSP) 是标准化开发工具和语言服务器进程之间交换的消息的产品。 使用语言服务器或恶魔不是一种新的或 novel 的理念。 诸如 Vim 和 Emacs 之类的编辑已在一段时间中执行此操作，以提供语义自动完成支持。 LSP 的目标是简化这些集成，并提供一个有用的框架，用于将语言功能公开给各种工具。

使用通用协议，可以通过重复使用语言的域模型的现有实现，将编程语言功能集成到具有最小误差的开发工具中。 可以使用 PHP、Python 或 Java 编写语言服务器后端，并且可以轻松地将其集成到各种工具中。 协议适用于通用的抽象级别，因此，工具可以提供丰富的语言服务，而无需完全理解特定于基础域模型的细微差别。

## <a name="how-work-on-the-lsp-started"></a>如何开始使用 LSP

LSP 随着时间的推移而发展，今天在3.0 版。 它在 OmniSharp 选择语言服务器的概念时开始，以便为 c # 提供丰富的编辑功能。 最初，OmniSharp 使用 HTTP 协议和 JSON 有效负载，并已集成到多个编辑器中，其中包括 [Visual Studio Code](https://code.visualstudio.com)。

在同一时间，Microsoft 开始处理 TypeScript 语言服务器，并在编辑器中支持 TypeScript，如 Emacs 和 Sublime 文本。 在此实现中，编辑器通过包含 TypeScript 服务器进程的 stdin/stdout 进行通信，并使用 V8 调试器协议为请求和响应提供的 JSON 有效负载。 TypeScript 服务器已集成到 TypeScript Sublime 插件中，并 VS Code 丰富的 TypeScript 编辑。

在集成了两种不同的语言服务器后，VS Code 团队开始探索用于编辑器和 Ide 的公共语言服务器协议。 通用协议允许语言提供程序创建可由不同 Ide 使用的单一语言服务器。 语言服务器使用者只需要实现一次协议的客户端。 这为语言提供商和语言使用者带来了 win 胜利的情况。

语言服务器协议以 TypeScript 服务器使用的协议开头，并使用 VS Code 语言 API 的更多语言功能对其进行扩展。 由于其简易性和现有库的原因，该协议支持 JSON-RPC 进行远程调用。

VS Code 团队通过实现几个 linter 语言服务器来对协议进行原型处理，这些服务器会响应不起毛的 (扫描的请求) 文件，并返回一组检测到的警告和错误。 其目标是在用户编辑文档时将文件不被修改，这意味着在编辑器会话期间将有许多 linting 请求。 使服务器保持正常运行是有意义的，以便不需要为每个用户编辑都启动新的 linting 进程。 实现了多个 linter 服务器，包括 VS Code 的 ESLint 和 TSLint 扩展。 这两个 linter 服务器都在 TypeScript/JavaScript 中实现并在 Node.js 上运行。 它们共享用于实现协议的客户端和服务器部分的库。

## <a name="how-the-lsp-works"></a>LSP 的工作方式

语言服务器在其自身的进程中运行，Visual Studio 或 VS Code 的工具通过 JSON-RPC 与使用语言协议的服务器进行通信。 在专用流程中运行的语言服务器的另一个优点是避免了与单个进程模型相关的性能问题。 如果客户端和服务器都 Node.js 中编写，则实际传输通道可以是 stdio.h、套接字、命名管道或节点 ipc。

下面是在日常编辑会话期间，工具和语言服务器的通信方式的示例：

![lsp 流程图](media/lsp-flow-diagram.png)

* **用户在工具中打开 (称为文档) 的文件**：该工具通知语言服务器文档已打开 ( "TextDocument/didOpen" ) 。 从现在开始，文档内容的真实情况不再在文件系统上，而是在内存中。

* **用户进行编辑**：此工具会将文档更改通知服务器 ( "TextDocument/didChange" ) ，并由语言服务器更新程序的语义信息。 如此一来，语言服务器会分析此信息，并在检测到的错误和警告 ( "textDocument/publishDiagnostics" ) 时通知工具。

* **用户在编辑器中的符号上执行 "跳到定义"**：该工具将发送带有两个参数的 "textDocument/definition" 请求： (1) 文档 URI， (2) 从其启动到定义请求的文本位置到服务器。 服务器在文档中以文档 URI 和符号定义的位置进行响应。

* **用户关闭文档 (文件) **：从工具发送 "TextDocument/didClose" 通知，告知语言服务器文档现在不再处于内存中，并且当前内容现已在文件系统上保持最新状态。

此示例演示了协议在编辑器功能（如 "中转到定义"、"查找所有引用"）级别上与语言服务器进行通信的方式。 协议使用的数据类型是编辑器或 IDE "数据类型"，如当前打开的文本文档和光标位置。 数据类型不是编程语言域模型的级别，通常会提供抽象语法树和编译器符号 (例如，解析类型、命名空间 ) 。这大大简化了协议。

现在，让我们更详细地查看 "textDocument/definition" 请求。 下面是在 c + + 文档中的 "转向定义" 请求的客户端工具和语言服务器之间执行的负载。

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

响应如下：

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

在 retrospect 中，在编辑器级别（而不是编程语言模型的级别）描述数据类型是语言服务器协议成功的原因之一。 与标准化抽象语法树和不同编程语言的编译器符号相比，将文本文档 URI 或游标位置标准化更为简单。

当用户使用不同语言时，VS Code 通常会为每种编程语言启动语言服务器。 下面的示例显示了一个会话，其中用户在 Java 和 SASS 文件上运行。

![java 和 sass](media/lsp-java-and-sass.png)

### <a name="capabilities"></a>功能

并非每个语言服务器都能支持协议定义的所有功能。 因此，客户端和服务器通过 "功能" 公布其支持的功能集。 例如，服务器宣布它可以处理 "textDocument/definition" 请求，但它可能不处理 "工作区/符号" 请求。 同样，客户端可以宣布它们能够在保存文档之前提供 "即将保存" 通知，使服务器能够计算文本编辑以自动设置编辑后的文档的格式。

## <a name="integrating-a-language-server"></a>集成语言服务器

语言服务器与特定工具的实际集成不是由语言服务器协议定义的，并留给工具实现者。 某些工具通过具有可开始与任何类型语言服务器的扩展来对语言服务器进行一般集成。 其他人（如 VS Code）为每个语言服务器创建一个自定义扩展，以便扩展仍可提供一些自定义语言功能。

为了简化语言服务器和客户端的实现，客户端和服务器部分有库或 Sdk。 这些库是针对不同语言提供的。 例如，有一种 [语言客户端 npm 模块](https://www.npmjs.com/package/vscode-languageclient) ，可以轻松地将语言服务器集成到 VS Code 扩展，并使用另一种 [语言服务器 npm 模块](https://www.npmjs.com/package/vscode-languageserver) 来编写使用 Node.js 的语言服务器。 这是当前支持库的 [列表](https://github.com/Microsoft/language-server-protocol/wiki/Protocol-Implementations) 。

## <a name="using-the-language-server-protocol-in-visual-studio"></a>在 Visual Studio 中使用语言服务器协议

* [添加语言服务器协议扩展](adding-an-lsp-extension.md) -了解有关将语言服务器集成到 Visual Studio 的信息。
