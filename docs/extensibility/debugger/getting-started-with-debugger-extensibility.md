---
title: 开始使用调试器扩展性 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 153db8889c78890a31a2e8003e6aa95ed24a02eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738590"
---
# <a name="get-started-with-debugger-extensibility"></a>开始使用调试器扩展性
提供了[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]创建和自定义调试器组件所需的信息，这些组件用于从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境中调试程序。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试添加了从以前[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器执行的广泛可用性测试派生的改进。 您可以使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试来逐步完成多语言应用程序，也可以在调试应用程序和多语言解决方案时实现变量的即时编辑。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试在进程外执行，程序正在调试，因此在应用程序的进程空间中的侵入性较小。 因此，编写与调试器交互的组件会更容易，而不会影响调试程序。

 为了最好地使用[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]， 您应该熟悉以下项：

- 集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]开发环境

- C++编程语言

- ATL COM

## <a name="in-this-section"></a>在本节中
 [扩展调试器的路线图](../../extensibility/debugger/roadmap-for-extending-the-debugger.md)概述在产品中实现调试的过程，具体取决于编译器及其输出。

 [调试器组件](../../extensibility/debugger/debugger-components.md)提供[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试组件的概述，包括调试引擎 （DE）、表达式赋值器 （EE） 和符号处理程序 （SH）。

 [调试器概念](../../extensibility/debugger/debugger-concepts.md)描述主要的调试体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)说明调试引擎 （DE） 如何在代码、文档和表达式评估上下文中同时运行。 描述三个上下文中的每一个与它相关的位置、位置或评估。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务的链接，例如启动程序和评估表达式。
