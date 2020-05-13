---
title: 终止程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 985b20fe75f8ceee3d434ac681b437c51baf85e8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712512"
---
# <a name="terminating-a-program"></a>终止程序
以下部分介绍使用一个线程终止单个程序。

## <a name="termination-process"></a>终止过程

1. DE 发送一个[IDebugThread破坏事件2，](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)带有一个有效的[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)。

2. DE 发送具有有效[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)的[IDebugProgram破坏事件2。](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

   IDE 进入设计模式。 调试引擎或运行时环境调用[IDebugPortNotify2：：删除程序节点](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)以从端口中删除程序。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
