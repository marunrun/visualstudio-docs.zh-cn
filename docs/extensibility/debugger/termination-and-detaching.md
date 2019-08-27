---
title: 终止和分离 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8aafb94e0a07462d93cc77a34f7199f61f944d0f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333726"
---
# <a name="termination-and-detaching"></a>终止和分离
以下部分介绍正常终止。

## <a name="discussion"></a>讨论
 之后[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)或[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)接口仍然存在，如果没有任何断点、 异常、 运行时错误或要进行调试的应用程序中的无限循环正在调试的程序运行完成。 此过程是正常终止。

 必须在发送[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)实现正常终止。 正常终止需要运行[IDebugProgramDestroyEvent2::GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)方法。

## <a name="see-also"></a>请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)