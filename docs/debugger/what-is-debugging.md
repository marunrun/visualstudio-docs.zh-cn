---
title: 什么是调试？
description: 了解调试应用的含义
ms.custom: debug-experiment
ms.date: 10/17/2018
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c01317f3b8fa92cf1bc17c3745f708e0d3f26e5b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901211"
---
# <a name="what-is-debugging"></a>什么是调试？

Visual Studio 调试器是一个功能强大的工具。 在演示如何使用它之前，我们想要讨论一些术语，例如“调试器”、“调试”和“调试模式”。 这样一来，在我们稍后讨论查找和修复 bug 时，我们对相关内容会有相同的理解。

## <a name="debugger-vs-debugging"></a>调试器与调试

“调试”这一术语可能有很多不同的含义，但从字面上看，它指从代码中删除 bug。 现在，可通过多种方法实现此目的。 例如，你可以通过扫描代码以查找拼写错误来进行调试，也可以使用代码分析器进行调试。 你可以使用性能探查器来调试代码， 也可以使用“调试器”进行调试。

调试器是一种非常专业的开发人员工具，它可附加到正在运行的应用，并允许你检查代码。 在 Visual Studio 调试文档中，这通常指我们所说的“调试”。

## <a name="debug-mode-vs-running-your-app"></a>调试模式与运行应用

第一次在 Visual Studio 中运行应用时，可以通过在工具栏中按下绿色箭头按钮 ![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")（或按 F5）来启动它。 默认情况下，“调试”值在左侧下拉菜单中显示。 如果你不熟悉 Visual Studio，这可能给你留下调试应用与运行应用有关的印象，而实际上也确实如此，但从根本上讲，这是两个差异很大的任务。

![选择调试生成](../debugger/media/what-is-debugging-debug-build.png)

“调试”值指示调试配置。 在调试配置中启动应用（按绿色箭头或 F5）时，你将在“调试模式”下启动应用，这意味着你要运行连接了调试器的应用。 此操作会启用一整套调试功能，你可使用这些功能帮助查找应用中的 bug。

如果你有一个打开的项目，请选择显示“调试”的下拉选项，然后改为选择“发布”。

![选择发布生成](../debugger/media/what-is-debugging-release-build.png)

切换此设置时，可以将项目从调试配置更改为发布配置。 Visual Studio 项目具有针对你的程序的单独发布和调试配置。 生成调试版本的目的是用于调试，而生成发布版本的目的是用于最终发布分发。 发布生成针对性能进行了优化，而调试生成则更适合调试。

## <a name="when-to-use-a-debugger"></a>何时使用调试器

调试器是查找和修复应用中的 bug 的重要工具。 但是，上下文是关键所在，请务必充分利用可以使用的所有工具，以帮助快速消除 bug 或错误。 有时候，合适的“工具”可能指更好的编码做法。 通过学习何时使用调试器和一些其他工具，你还将了解如何更有效地使用调试器。

## <a name="next-steps"></a>后续步骤

在本文中，你已了解一些常规的调试概念。 接下来，你可以开始学习如何使用 Visual Studio 进行调试以及如何在编写代码时减少 bug。 以下文章演示 C# 代码示例，但这些概念适用于 Visual Studio 支持的所有语言。

> [!div class="nextstepaction"]
> [零基础调试](../debugger/debugging-absolute-beginners.md)

> [!div class="nextstepaction"]
> [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
