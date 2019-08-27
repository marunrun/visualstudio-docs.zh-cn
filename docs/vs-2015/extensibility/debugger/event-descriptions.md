---
title: 事件说明 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 09f61652-7e16-4bb0-8055-f61a84bf384e
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5aff88047d6b1f79544af927751d7a053eeda218
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152825"
---
# <a name="event-descriptions"></a>事件说明
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

每种类型的事件有特定用途。  
  
## <a name="events-and-the-reasons-for-their-use"></a>事件和供其使用的原因  
  
|Event|描述|  
|-----------|-----------------|  
|激活文档事件|调试引擎 (DE) 想要打开或将文档置于前台 IDE 时发生。|  
|断点绑定或断点错误事件|绑定断点或当无法绑定断点，并返回一个错误时发送。|  
|未绑定断点事件|从代码取消绑定的断点的绑定时发生。|  
|可以停止事件|发送到 IDE 以确定用户是否要在代码中的指定点处停止。|  
|断点事件|代码或数据断点命中时，发生。|  
|文档文本事件|在文档中的文本更改时发生。 这些事件不会发送通过`IDebugEventCallBack2::Event`方法。|  
|引擎创建的事件|当首次创建一个引擎时发送。|  
|入口点事件|当正在调试的程序已运行其初始化代码并达到其第一个用户入口点时发送。|  
|异常事件|发送时遇到异常时正在运行的程序。|  
|表达式评估完成事件数|异步表达式计算完成时发送。|  
|查找符号事件|只要 DE 需要要求用户查找符号的模块发送。|  
|加载完成事件数|仅当初始程序加载已完成和第一个代码是要运行的程序中发送。|  
|消息事件|向用户发送消息时发送。|  
|模块加载事件|当加载或卸载新模块时发送。|  
|输出字符串事件|当程序写入调试输出时发送。|  
|创建和销毁事件|发送以宣布的创建或销毁的进程、 程序、 属性、 会话和线程，以便在 Visual Studio IDE 可以跟踪正在调试的程序的状态。|  
|步骤完成事件数|步骤已完成时发送。|  
|线程名称更改事件|当用户更改线程的名称时发送。|  
|程序名称更改事件|当用户更改程序的名称时发送。|  
  
## <a name="see-also"></a>请参阅  
 [发送事件](../../extensibility/debugger/sending-events.md)
