---
title: 调试器可扩展性入门 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 99e2dabf18d3d00034d65a94c41f2e435ad64114
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350012"
---
# <a name="get-started-with-debugger-extensibility"></a>开始使用调试器可扩展性
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]提供了您需要创建和自定义用于调试程序中的调试器组件的信息[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试已添加派生自上以前执行的测试的广泛可用性改进[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器。 可以使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试单步执行的多语言应用程序，也可以实现实时上调试应用程序和多语言解决方案时编辑的变量。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试是执行的进程外与正在调试的程序，因此在应用程序的进程空间中较少受侵入。 因此，它是更轻松地编写与调试器的交互的组件，而不会影响调试程序。

 最大效用[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]，您应熟悉以下各项：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE)

- C++编程语言

- ATL COM

## <a name="in-this-section"></a>本节内容
 [扩展调试器的路线图](../../extensibility/debugger/roadmap-for-extending-the-debugger.md)概述了实现在您的产品，具体取决于您的编译器和其输出中进行调试的过程。

 [调试器组件](../../extensibility/debugger/debugger-components.md)概述的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试组件，包括调试引擎 (DE)、 表达式计算器 (EE) 和符号处理程序 (SH)。

 [调试器概念](../../extensibility/debugger/debugger-concepts.md)介绍了调试的主要体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)介绍了调试引擎 (DE) 的运行方式同时代码、 文档和表达式计算上下文。 介绍的三个上下文、 位置、 位置或与它相关评估每个。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务，如启动程序和计算表达式。