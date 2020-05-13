---
title: 删除断点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a77be200a11eb7b3985a4c1a47e4cddaa543f900
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738949"
---
# <a name="deleting-a-breakpoint"></a>删除断点
下面描述了删除挂起的断点时的过程：

## <a name="deletion-process"></a>删除过程
 会话调试管理器 （SDM） 调用[IDebugPendingBreakpoint2：:Delete](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)方法，以删除挂起的断点和所有绑定断点。

> [!NOTE]
> 单个绑定断点也可以通过调用[IDebugBoundBreakpoint2：:Delete](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)删除。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
