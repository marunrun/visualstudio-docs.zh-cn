---
title: IApplicationDebugger 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IApplicationDebugger interface
ms.assetid: 27f6f8f5-2bf3-49bc-8abb-dfca98935aba
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a1c0cc89c61665ce468457b64bbdd4b5d293649b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991456"
---
# <a name="iapplicationdebugger-interface"></a>IApplicationDebugger 接口
由调试器所公开的主接口。 除了继承的方法之外`IUnknown`，则`IApplicationDebugger`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IApplicationDebugger::QueryAlive](../../winscript/reference/iapplicationdebugger-queryalive.md)|指示调试器是否响应。|  
|[IApplicationDebugger::CreateInstanceAtDebugger](../../winscript/reference/iapplicationdebugger-createinstanceatdebugger.md)|通过代码在调试器进程中允许创建的对象，它是-进程外调试器。|  
|[IApplicationDebugger::onDebugOutput](../../winscript/reference/iapplicationdebugger-ondebugoutput.md)|处理调试输出事件。|  
|[IApplicationDebugger::onHandleBreakPoint](../../winscript/reference/iapplicationdebugger-onhandlebreakpoint.md)|处理断点事件。|  
|[IApplicationDebugger::onClose](../../winscript/reference/iapplicationdebugger-onclose.md)|处理调试应用程序关闭事件。|  
|[IApplicationDebugger::onDebuggerEvent](../../winscript/reference/iapplicationdebugger-ondebuggerevent.md)|处理自定义应用程序事件。|