---
title: Visual Studio 调试器扩展性 |Microsoft Docs
description: 本文介绍 Visual Studio 调试器扩展性，并提供指向有关 Visual Studio 调试的文章的链接。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a072373ce0cf7633c595eb549455e6ecd62df887
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995988"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio 调试器扩展性
Visual Studio 包括一个完全交互式的源代码调试器，它提供了功能强大且易于使用的工具，用于跟踪程序中的 bug。 调试器对 Visual Basic、c #、C/c + + 和 JavaScript 提供完全支持。 但对于，通过 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=21835)提供的，在具有相同功能的调试器中可以支持其他编程语言。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器是公共前端 (即，用户界面) 调试组件，后者又特定于正在调试的语言。 对于新语言，调试程序所需的全部工作 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 就是创建必要的后端组件，例如调试引擎 (DE) 。 这一点就是进入的位置 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]包含 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 创建新的 DE 所需的所有元素的完整引用。 此外，还有一些示例和教程可帮助您入门。

 有关支持调试的语言项目系统的完整示例，请参阅 [IronPython 示例](https://www.microsoft.com/download/details.aspx?id=55984)。

 以下各节介绍如何使用扩展调试器 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。

## <a name="in-this-section"></a>在本节中
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) 介绍 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 如何提供调试功能以及如何安装 SDK。

 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md) 记录自定义的 DE 过程，从准备您的程序进行 DE 以分离解除。

 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md) 说明您是否必须编写表达式计算器。

 [选择调试引擎实现策略](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md) 讨论如何实现您的 DE。

 [参考](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md) 记录 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试 API。

 [示例](../../extensibility/debugger/visual-studio-debugging-samples.md) 包含指向公共语言运行时表达式计算器示例和调试引擎示例的链接。
