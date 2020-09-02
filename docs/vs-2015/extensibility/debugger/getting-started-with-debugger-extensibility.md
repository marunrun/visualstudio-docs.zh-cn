---
title: 与调试器扩展性入门 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d1c616c7cf8ed90ec3d76046892167b9b742a1b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152709"
---
# <a name="getting-started-with-debugger-extensibility"></a>调试器可扩展性入门
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]提供在环境中创建和自定义用于调试程序的调试器组件所需的信息 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试添加了从对以前的调试程序执行的广泛可用性测试派生的改进 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 您可以使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试来单步执行多语言应用程序，也可以在调试应用程序和多语言解决方案时，动态地编辑变量。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试由正在调试的程序在进程外执行，因此在应用程序的进程空间中的干扰性较低。 因此，可以更轻松地编写与调试器交互的组件，而不会影响调试程序。  
  
 若要充分利用 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] ，应熟悉以下内容：  
  
- [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成开发环境 (IDE)   
  
- C + + 编程语言  
  
- ATL COM  
  
## <a name="in-this-section"></a>本节内容  
 [扩展调试器的路线图](../../extensibility/debugger/roadmap-for-extending-the-debugger.md)  
 概述在您的产品中实现调试的过程，具体取决于您的编译器及其输出。  
  
 [调试器组件](../../extensibility/debugger/debugger-components.md)  
 概述 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试组件，其中包括调试引擎 (DE) 、expression 计算器 (EE) 以及符号处理程序 (SH) 。  
  
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)  
 介绍主要调试体系结构概念。  
  
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)  
 说明调试引擎 (DE) 如何在代码、文档和表达式计算上下文中同时运行。 描述每个上下文的位置、位置或与之相关的计算。  
  
 [调试任务](../../extensibility/debugger/debugging-tasks.md)  
 包含指向各种调试任务的链接，如启动程序和计算表达式。
