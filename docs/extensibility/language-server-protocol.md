---
title: 语言服务器协议概述 |微软文档
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 6a7d93c2-31ea-4bae-8b29-6988a567ddf2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3bd5dce3cfb7022a8abb6397dc87b418144cbe1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703105"
---
# <a name="language-server-protocol"></a>语言服务器协议

## <a name="what-is-the-language-server-protocol"></a>什么是语言服务器协议？

支持丰富的编辑功能，如源代码自动完成或**进入定义**编程语言在编辑器或IDE传统上是非常具有挑战性的和耗时的。 通常，它需要用编辑器或 IDE 的编程语言编写域模型（扫描仪、解析器、类型检查器、生成器等）。 例如，Eclipse CDT 插件（在 Eclipse IDE 中支持 C/C++）是用 Java 编写的，因为 Eclipse IDE 本身是用 Java 编写的。 按照此方法，这意味着在 Visual Studio 代码的 TypeScript 中实现 C/C++ 域模型，在 Visual Studio 的 C# 中实现单独的域模型。

如果开发工具可以重用现有的特定于语言的库，则创建特定于语言的域模型也容易得多。 但是，这些库通常在编程语言本身中实现（例如，好的 C/C++域模型在 C/C++中实现）。 将 C/C++ 库集成到用 TypeScript 编写的编辑器中，在技术上是可能的，但很难做到。

### <a name="language-servers"></a>语言服务器

另一种方法是在自己的进程中运行库，并使用进程间通信与它通信。 来回发送的消息形成协议。 语言服务器协议 （LSP） 是标准化开发工具和语言服务器进程之间交换的消息的标准。 使用语言服务器或恶魔并不是一个新的或新颖的想法。 像 Vim 和 Emacs 这样的编辑器已经这样做了一段时间，以提供语义自动完成支持。 LSP 的目标是简化这些类型的集成，并为将语言功能公开为各种工具提供了一个有用的框架。

拥有通用协议可以重用语言域模型的现有实现，以最小的大惊小怪将编程语言功能集成到开发工具中。 语言服务器后端可以用PHP、Python或Java编写，LSP 可以轻松地将其集成到各种工具中。 该协议在通用抽象级别工作，以便工具可以提供丰富的语言服务，而无需完全理解特定于底层域模型的细微差别。

## <a name="how-work-on-the-lsp-started"></a>LSP 工作如何开始

LSP 随着时间的推移而演变，而今天它位于版本 3.0。 它开始于 OmniSharp 拾取语言服务器的概念，为 C# 提供丰富的编辑功能。 最初，OmniSharp 使用带有 JSON 有效负载的 HTTP 协议，并已集成到包括[Visual Studio 代码](https://code.visualstudio.com)在内的多个编辑器中。

大约在同一时间，Microsoft 开始在 TypeScript 语言服务器上工作，其理念是在 Emacs 和 Sublime Text 等编辑器中支持 TypeScript。 在此实现中，编辑器通过 stdin/stdout 与 TypeScript 服务器进程进行通信，并使用受 V8 调试器协议启发的 JSON 负载来访问请求和响应。 TypeScript 服务器已集成到 TypeScript 崇高插件和 VS 代码中，以便进行丰富的 TypeScript 编辑。

集成了两个不同的语言服务器后，VS Code 团队开始探索编辑器和 IDE 的通用语言服务器协议。 公共协议使语言提供程序能够创建可由不同 IDE 使用的单个语言服务器。 语言服务器使用者只需实现协议的客户端一次。 这会导致语言提供者和语言使用者的双赢。

语言服务器协议从 TypeScript 服务器使用的协议开始，通过更多受 VS Code 语言 API 启发的语言功能扩展它。 该协议具有 JSON-RPC 的支持，用于远程调用，由于其简单性和现有库。

VS Code 团队通过实现多个 linter 语言服务器对协议进行了原型设计，这些服务器响应对文件进行（扫描）的请求，并返回一组检测到的警告和错误。 目标是在用户在文档中编辑时对文件进行点皮，这意味着在编辑器会话期间将有许多林点请求。 保持服务器正常运行是有意义的，这样不需要为每个用户编辑启动新的林点进程。 实现了多个 linter 服务器，包括 VS 代码的 ESLint 和 TSLint 扩展。 这两个 linter 服务器都在 TypeScript/JavaScript 中实现，并在 Node.js 上运行。 它们共享一个库，用于实现协议的客户端和服务器部分。

## <a name="how-the-lsp-works"></a>LSP 的工作原理

语言服务器在其自己的进程中运行，Visual Studio 或 VS 代码等工具通过 JSON-RPC 使用语言协议与服务器通信。 在专用进程中运行的语言服务器的另一个优点是避免了与单个进程模型相关的性能问题。 如果客户端和服务器都写入 Node.js，则实际传输通道可以是 stdio、套接字、命名管道或节点 ipc。

下面是工具和语言服务器在常规编辑会话期间如何通信的示例：

![lsp 流程图](media/lsp-flow-diagram.png)

* **用户在工具中打开文件（称为文档）：** 该工具通知语言服务器文档已打开（"文本文档/已打开"。）。 从现在起，文档内容的真相不再在文件系统上，而由工具保存在内存中。

* **用户进行编辑**：该工具通知服务器文档更改（"文本文档/didChange"），并且程序的语义信息由语言服务器更新。 发生这种情况时，语言服务器会分析此信息，并将检测到的错误和警告（"文本文档/发布诊断"）通知工具。

* **用户对编辑器中的符号执行"转到定义"：** 该工具发送包含两个参数的"文本文档/定义"请求：（1） 文档 URI 和 （2） 从"转到定义"请求启动到服务器的文本位置。 服务器使用文档 URI 和符号定义在文档中的位置进行响应。

* **用户关闭文档（文件）：** 从该工具发送"文本文档/didClose"通知，通知语言服务器文档现在不再内存，并且文件系统上的当前内容是最新的。

此示例说明了协议如何在编辑器功能（如"转到定义"、"查找所有引用"）级别与语言服务器通信。 协议使用的数据类型是编辑器或 IDE"数据类型"，如当前打开的文本文档和游标的位置。 数据类型不在通常提供抽象语法树和编译器符号（例如，解析类型、命名空间等）的编程语言域模型的级别。这大大简化了协议。

现在，让我们更详细地查看"文本文档/定义"请求。 下面是客户端工具和C++文档中"转到定义"请求的语言服务器之间的有效负载。

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

回顾过去，在编辑器级别而不是编程语言模型级别描述数据类型是语言服务器协议成功的原因之一。 与标准化不同编程语言的抽象语法树和编译器符号相比，标准化文本文档 URI 或游标位置要简单得多。

当用户使用不同的语言时，VS 代码通常会为每个编程语言启动一个语言服务器。 下面的示例显示了用户在 Java 和 SASS 文件上工作的会话。

![贾瓦和萨斯](media/lsp-java-and-sass.png)

### <a name="capabilities"></a>功能

并非所有语言服务器都可以支持协议定义的所有功能。 因此，客户端和服务器通过"功能"宣布其支持的功能集。 例如，服务器宣布可以处理"文本文档/定义"请求，但可能无法处理"工作区/符号"请求。 同样，客户端可以宣布，在保存文档之前，他们可以提供"即将保存"的通知，以便服务器可以计算文本编辑以自动格式化编辑的文档。

## <a name="integrating-a-language-server"></a>集成语言服务器

语言服务器实际集成到特定工具时，语言服务器协议不定义，并留给工具实现者。 某些工具通过具有可以启动和与任何类型的语言服务器对话的扩展来一般地集成语言服务器。 其他扩展（如 VS 代码）则创建每个语言服务器的自定义扩展，以便扩展仍然能够提供一些自定义语言功能。

为了简化语言服务器和客户端的实现，客户端和服务器部件有库或 SDK。 这些库提供不同的语言。 例如，有一种语言[客户端 npm 模块](https://www.npmjs.com/package/vscode-languageclient)，用于简化语言服务器与 VS 代码扩展的集成，另一种语言服务器[npm 模块](https://www.npmjs.com/package/vscode-languageserver)使用 Node.js 编写语言服务器。 这是支持库的当前[列表](https://github.com/Microsoft/language-server-protocol/wiki/Protocol-Implementations)。

## <a name="using-the-language-server-protocol-in-visual-studio"></a>在可视化工作室中使用语言服务器协议

* [添加语言服务器协议扩展](adding-an-lsp-extension.md)- 了解如何将语言服务器集成到可视化工作室中。
