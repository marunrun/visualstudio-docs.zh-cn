---
title: 可视化工作室调试器可扩展性 |微软文档
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
ms.openlocfilehash: ff4222b555fab73914776725fc79581f29fa5e53
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712499"
---
# <a name="visual-studio-debugger-extensibility"></a>可视化工作室调试器可扩展性
Visual Studio 包括一个完全交互式的源代码调试器，提供了一个功能强大且易于使用的工具，用于跟踪程序中的 Bug。 调试器完全支持可视基本版、C#、C/C++ 和 JavaScript。 但是，使用可从[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=21835)获取 的 ，调试器中可以支持其他编程语言，并具有相同的丰富功能。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器是调试组件的通用前端（即用户界面），而调试组件又特定于正在调试的语言。 对于新语言，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器支持所需的只是创建必要的后端组件，如调试引擎 （DE）。 这一[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]点是进来的地方。

 包括[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]对创建新 DE 所需的所有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]元素的完整引用。 此外，还有一些示例和教程将帮助您入门。

 有关支持调试的语言项目系统的完整示例，请参阅[IronPython 示例](https://www.microsoft.com/download/details.aspx?id=55984)。

 以下各节介绍如何使用 扩展[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]调试器。

## <a name="in-this-section"></a>在本节中
 [开始](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)描述调试[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供的内容以及如何安装 SDK。

 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)记录自定义 DE 过程，从为 DE 准备程序到分离 DE。

 [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)说明是否必须编写表达式赋值器。

 [选择调试引擎实施策略](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)讨论如何实现 DE。

 [参考文献](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)记录[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试 API。

 [样品](../../extensibility/debugger/visual-studio-debugging-samples.md)包含指向通用语言运行时表达式赋值器示例和调试引擎示例的链接。
