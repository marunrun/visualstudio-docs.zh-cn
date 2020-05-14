---
title: 调试器组件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03c400fd03c5ee0f2629e9f436b65f53f8f2ac8b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739011"
---
# <a name="debugger-components"></a>调试器组件
调试[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]器作为 VSPackage 实现，并管理整个调试会话。 调试会话包括以下元素：

- **调试包：**[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器提供相同的用户界面，无论正在调试什么。

- **会话调试管理器 （SDM）：** 为调试器提供一致的编程[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]接口，用于管理各种调试引擎。 它由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实现。

- **过程调试管理器 （PDM）：** 管理 所有正在运行的实例[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，可以调试或正在调试的所有程序的列表。 它由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实现。

- **调试引擎 （DE）：** 负责监视正在调试的程序，将正在运行的程序的状态传达给 SDM 和 PDM，并与表达式赋值器和符号提供程序进行交互，以便对程序内存和变量的状态提供实时分析。 它由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]（对于它支持的语言）和第三方供应商实现，他们希望支持自己的运行时。

- **表达式赋值器 （EE）：** 支持在程序在特定点停止时动态计算用户提供的变量和表达式。 它由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]（对于它支持的语言）和第三方供应商（希望支持自己的语言）实现。

- **符号提供程序 （SP）：** 也称为符号处理程序，将程序的调试符号映射到程序的运行实例，以便提供有意义的信息（如源代码级调试和表达式计算）。 它由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]（对于通用语言运行时 [CLR] 符号和程序数据库 [PDB] 符号文件格式）和具有自己专有存储调试信息方法的第三方供应商实现。

  下图显示了可视化工作室调试器的这些元素之间的关系。

  ![调试组件概述](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")

## <a name="in-this-section"></a>在本节中
 [调试包](../../extensibility/debugger/debug-package.md)讨论调试包，该包在 shell[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中运行并处理所有 UI。

 [过程调试管理器](../../extensibility/debugger/process-debug-manager.md)提供 PDM 功能的概述，PDM 是可调试的进程的经理。

 [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)定义 SDM，它向 IDE 提供调试会话的统一视图。 SDM 管理 DE。

 [调试引擎](../../extensibility/debugger/debug-engine.md)记录 DE 提供的调试服务。

 [操作模式](../../extensibility/debugger/operational-modes.md)概述了 IDE 可以操作的三种模式：设计模式、运行模式和中断模式。 还讨论了过渡机制。

 [表达式赋值器](../../extensibility/debugger/expression-evaluator.md)解释 EE 在运行时的用途。

 [符号提供程序](../../extensibility/debugger/symbol-provider.md)讨论符号提供程序在实现时如何计算变量和表达式。

 [类型可视化器和自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)讨论什么是类型可视化器和自定义查看器，以及表达式评估器在支持两者方面扮演什么角色。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)描述主要的调试体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)说明 DE 如何在代码、文档和表达式计算上下文中同时运行。 描述三个上下文中的每一个与它相关的位置、位置或评估。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务的链接，例如启动程序和评估表达式。

## <a name="see-also"></a>请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
