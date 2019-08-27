---
title: 启用要进行调试的程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enabling for programs
ms.assetid: 61d24820-0cd9-48b6-8674-6813f7493237
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b0f0331430a1cc625dee2a7029742fd62d67fb56
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155367"
---
# <a name="enabling-a-program-to-be-debugged"></a>启用要进行调试的程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在调试引擎 (DE) 可调试的程序之前，必须先启动 DE 或将其附加到现有的程序。  
  
## <a name="in-this-section"></a>本节内容  
 [获取端口](../../extensibility/debugger/getting-a-port.md)  
 讨论如何为启用要进行调试的程序的第一步中获取一个端口。  
  
 [注册程序](../../extensibility/debugger/registering-the-program.md)  
 介绍启用要进行调试的程序的下一步： 注册该端口。 注册后，可以调试程序通过附加或实时 (JIT) 调试的过程。  
  
 [附加到程序](../../extensibility/debugger/attaching-to-the-program.md)  
 介绍了下一步： 将调试器附加到程序。  
  
 [基于启动的附加](../../extensibility/debugger/launch-based-attachment.md)  
 描述为一个程序，这是 SDM 通过启动时自动基于启动的附件。  
  
 [发送必需事件](../../extensibility/debugger/sending-the-required-events.md)  
 将指导你逐步创建调试引擎 (DE) 时所需的事件并将其附加到的程序。  
  
## <a name="related-sections"></a>相关章节  
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 定义调试引擎 (DE)，并介绍了通过 DE 接口和如何它们可能会导致不同的操作模式之间进行过渡调试器实现的服务。
