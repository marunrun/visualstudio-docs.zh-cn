---
title: 什么是调试？
description: 了解这意味着若要调试在应用程序
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901211"
---
# <a name="what-is-debugging"></a>什么是调试？

Visual Studio 调试器是一个功能强大的工具。 我们演示如何使用它之前，我们想要讨论的一些术语如*调试器*，*调试*，并*调试模式下*。 这样一来，当我们谈及更高版本查找并修复 bug，我们将讨论相同的操作。

## <a name="debugger-vs-debugging"></a>调试器与调试

术语*调试*可能意味着很多不同操作，但最按字面意思，这意味着在代码中删除 bug。 现在，有很多方面来执行此操作。 例如，您可以调试扫描代码寻找拼写错误，或使用的代码分析器。 您可以通过使用性能探查器调试代码。 或者，您可以通过使用调试*调试器*。

调试器是一个非常专业开发人员工具，将附加到正在运行的应用，并允许你检查你的代码。 在 Visual Studio 的调试文档，这通常是明白我们的意思这里所说"的调试"。

## <a name="debug-mode-vs-running-your-app"></a>调试与运行您的应用程序模式

在首次在 Visual Studio 中运行您的应用程序，您可能通过按绿色箭头按钮启动它![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")工具栏中 (或**F5**)。 默认情况下**调试**值显示在左侧的下拉列表中。 如果您不熟悉 Visual Studio，这可能使印象，调试您的应用程序具有与运行您的应用程序-它执行-但这些从根本上说是两个非常不同的任务。

![选择调试版本](../debugger/media/what-is-debugging-debug-build.png)

一个**调试**值指示调试配置。 当启动应用程序 (按绿色箭头或**F5**) 在调试配置中，启动应用程序*调试模式下*，这意味着运行的您的应用程序具有附加调试器。 这样一套完整的调试功能可用于帮助发现应用程序中的 bug。

如果您打开一个项目，请选择在那里显示的下拉列表选择器**调试**，然后选择**发行**相反。

![选择发布版本](../debugger/media/what-is-debugging-release-build.png)

切换此设置，请将你的项目的调试配置从更改为发布配置。 Visual Studio 项目具有针对你的程序的单独发布和调试配置。 生成用于调试的调试版本和最终发布分发的版本。 发布版本进行了优化性能，但更好地进行调试的调试版本。

## <a name="when-to-use-a-debugger"></a>何时使用调试程序

调试器是查找并修复您的应用程序中的 bug 的必备工具。 但是，上下文就是一切，并且务必要利用所有工具任您可释放对象，以帮助您快速消除 bug 或错误。 有时，右侧的"工具"可能是更好的编码做法。 通过了解何时使用其他一些工具与调试器，您将了解如何更有效地使用调试器。

## <a name="next-steps"></a>后续步骤

在本文中，你已了解一些常规的调试概念。 接下来，您可以开始学习如何使用 Visual Studio 进行调试以及如何编写更少 bug 的代码。 以下文章显示C#代码示例，但概念适用于 Visual Studio 支持的所有语言。

> [!div class="nextstepaction"]
> [零基础调试](../debugger/debugging-absolute-beginners.md)

> [!div class="nextstepaction"]
> [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
