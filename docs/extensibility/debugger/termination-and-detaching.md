---
title: 终止和分离 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b88255d618ce42fa55d878f192d31523ba3f83b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712495"
---
# <a name="termination-and-detaching"></a>终止和分离
以下部分介绍了正常终止。

## <a name="discussion"></a>讨论 (Discussion)
 在 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 或 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 接口继续后，如果要调试的应用程序中没有断点、异常、运行时错误或无限循环，则正在调试的程序将运行到完成。 此过程是正常终止。

 必须发送 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 以实现正常终止。 正常终止要求运行 [IDebugProgramDestroyEvent2：： GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) 方法。

## <a name="see-also"></a>另请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
