---
title: 调试包 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dda8b1ac6eaa2cd5352d441600ae720c3aac321c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68181293"
---
# <a name="debug-package"></a>调试包
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试包在 Visual Studio shell 中运行并处理所有 UI。 它使用 Visual Studio 调试接口，并与会话调试管理器 (SDM) 通信。  
  
 中断通过 SDM 发送的事件将调试器从运行模式切换为中断模式，并将焦点更改为发生中断的程序。 调试包跟踪事件发送到的堆栈帧和线程。  
  
 调试包没有语言或运行时环境依赖项。 不需要实现或修改调试包。  
  
 调试包由 vsdebug.dll 实现。  
  
## <a name="see-also"></a>另请参阅  
 [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)   
 [堆栈帧](../../extensibility/debugger/stack-frames.md)   
 [线程](../../extensibility/debugger/threads.md)   
 [调试器组件](../../extensibility/debugger/debugger-components.md)
