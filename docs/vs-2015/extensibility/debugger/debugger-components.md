---
title: 调试器组件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 12f865e7d4c44cfa4002b330ed85ec95f95a8ef9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200664"
---
# <a name="debugger-components"></a>调试器组件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试器作为 VSPackage 实现和管理整个调试会话。 调试会话包括以下元素：  
  
- **调试包：** [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试器提供了相同的用户界面，不论正在调试。  
  
- **会话调试管理器 (SDM):** 提供了一致的编程接口到[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试器的各种的调试引擎管理。 它由实现[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
- **进程调试管理器 (PDM):** 为所有运行的实例管理[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，可以是也正在调试的所有程序的列表。 它由实现[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
- **调试引擎 (DE):** 负责监视正在调试的程序进行通信的 SDM 和 PDM，正在运行的程序状态和与提供程序的内存状态的实时分析的表达式计算器和符号提供程序进行交互和变量。 它由实现[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]（适用于它支持的语言） 和第三方供应商想要支持其自己的运行的时。  
  
- **表达式计算器 (EE):** 提供对动态评估变量和表达式特定点已停止程序时由用户提供支持。 它由实现[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]（适用于它支持的语言） 和第三方供应商想要支持自己的语言。  
  
- **符号提供程序 (SP):** 也称为符号处理程序，将映射程序的调试符号的程序正在运行的实例，以便可以提供有意义的信息 （如代码源代码级调试和表达式计算）。 它由实现[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]（公共语言运行时 [CLR] 符号和程序数据库 [PDB] 符号文件格式） 和由第三方供应商有其自己专有存储调试信息的方法。  
  
  下图显示了 Visual Studio 调试器的这些元素之间的关系。  
  
  ![调试组件概述](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")  
  
## <a name="in-this-section"></a>本节内容  
 [调试包](../../extensibility/debugger/debug-package.md)  
 讨论调试包，在运行[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]shell 并处理所有用户界面。  
  
 [进程调试管理器](../../extensibility/debugger/process-debug-manager.md)  
 概述 PDM，这是可调试的进程管理器的功能。  
  
 [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)  
 定义 SDM，提供对 IDE 的调试会话的统一的视图。 SDM 管理 DE。  
  
 [调试引擎](../../extensibility/debugger/debug-engine.md)  
 介绍 DE 提供调试服务。  
  
 [操作模式](../../extensibility/debugger/operational-modes.md)  
 概述了可在 IDE 的三种模式： 设计模式、 运行模式下和中断模式。 此外讨论了转换机制。  
  
 [表达式计算器](../../extensibility/debugger/expression-evaluator.md)  
 在运行时说明 EE 的用途。  
  
 [符号提供程序](../../extensibility/debugger/symbol-provider.md)  
 讨论如何操作，请在实现中，符号提供程序的计算结果的变量和表达式。  
  
 [类型可视化工具和自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)  
 讨论了类型可视化工具和自定义查看器是，何种角色中同时支持播放的表达式计算器。  
  
## <a name="related-sections"></a>相关章节  
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)  
 描述调试的主要体系结构概念。  
  
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)  
 介绍了 DE 方式同时代码、 文档和表达式计算上下文中。 介绍的三个上下文、 位置、 位置或与它相关评估每个。  
  
 [调试任务](../../extensibility/debugger/debugging-tasks.md)  
 包含指向不同的调试任务，如启动程序和计算表达式。  
  
## <a name="see-also"></a>请参阅  
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
