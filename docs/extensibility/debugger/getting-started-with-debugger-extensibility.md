---
title: 与调试器扩展性入门 |Microsoft Docs
description: 开始创建和自定义用于调试 Visual Studio 环境中的程序的调试器组件。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 6949b9b8a9168915c64bc6183f6b1391a1c79220
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560030"
---
# <a name="get-started-with-debugger-extensibility"></a>调试器扩展性入门
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]提供在环境中创建和自定义用于调试程序的调试器组件所需的信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试添加了从对以前的调试程序执行的广泛可用性测试派生的改进 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 您可以使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试来单步执行多语言应用程序，也可以在调试应用程序和多语言解决方案时，动态地编辑变量。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试由正在调试的程序在进程外执行，因此在应用程序的进程空间中的干扰性较低。 因此，可以更轻松地编写与调试器交互的组件，而不会影响调试程序。

 若要充分利用 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ，应熟悉以下各项：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 

- C + + 编程语言

- ATL COM

## <a name="in-this-section"></a>在本节中
 [扩展调试器的路线图](../../extensibility/debugger/roadmap-for-extending-the-debugger.md) 概述在您的产品中实现调试的过程，具体取决于您的编译器及其输出。

 [调试器组件](../../extensibility/debugger/debugger-components.md) 概述 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试组件，其中包括调试引擎 (DE) 、expression 计算器 (EE) 以及符号处理程序 (SH) 。

 [调试器概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要的调试体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md) 说明调试引擎 (DE) 如何在代码、文档和表达式计算上下文中同时运行。 介绍这三个上下文的位置或相关评估。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务的链接，如启动程序和计算表达式。
