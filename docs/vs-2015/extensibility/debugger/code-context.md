---
title: 代码上下文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d59a4c79cb21386fa6f6e7031404aeb0b435b3b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197375"
---
# <a name="code-context"></a>代码上下文
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试中， **代码上下文**：  
  
- 在代码中提供对调试引擎已知的位置的抽象 (DE) 。 对于今天的大多数运行时结构，可以将代码上下文视为程序的指令流中的地址。 对于 nontraditional 语言，其中的代码不能通过说明进行表示，代码上下文可以用其他方式表示。  
  
- 描述正在调试的程序的执行流中的当前位置。  
  
- 仅当程序在断点处停止时才存在。  
  
- 具有关联的文档上下文。  
  
- 由 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) 接口实现。  
  
## <a name="see-also"></a>另请参阅  
 [文档上下文](../../extensibility/debugger/document-context.md)   
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
