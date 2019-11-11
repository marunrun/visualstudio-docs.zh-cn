---
title: Visual Studio 调试器扩展性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 58bfec6fa09f6450afb8170d60acad39edacd590
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72982455"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio 调试器扩展性
Visual Studio 包括一个完全交互式的源代码调试器，它提供了功能强大且易于使用的工具，用于跟踪程序中的 bug。 调试器对 Visual Basic、 C#、C/C++和 JavaScript 提供完全支持。 但是，通过[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=21835)提供的 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]，可以在具有相同功能的调试器中支持其他编程语言。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试程序是调试组件的公共前端（即用户界面），后者又特定于正在调试的语言。 对于新语言，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试程序所需的全部工作就是创建必要的后端组件，例如调试引擎（DE）。 这就是 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 进入的地方。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 包括对创建新 DE 所需的所有 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 元素的完整引用。 此外，还有一些示例和教程可帮助您入门。

 有关支持调试的语言项目系统的完整示例，请参阅[IronPython 示例](https://www.microsoft.com/download/details.aspx?id=55984)。

 以下各节介绍如何使用 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]扩展调试器。

## <a name="in-this-section"></a>本节内容
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)介绍 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试的功能以及如何安装 SDK。

 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)记录自定义的 DE 过程，从准备您的程序进行 DE 以分离解除。

 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)说明您是否必须编写表达式计算器。

 [选择调试引擎实现策略](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)讨论如何实现您的 DE。

 [参考](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)记录 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试 API。

 [示例](../../extensibility/debugger/visual-studio-debugging-samples.md)包含指向公共语言运行时表达式计算器示例和调试引擎示例的链接。
