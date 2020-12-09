---
title: 删除断点 |Microsoft Docs
description: 了解会话调试管理器如何在删除挂起断点时删除挂起的断点以及从该断点绑定的所有绑定断点。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 061175326a19af1866262421b381eb14267c7efd
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915552"
---
# <a name="deleting-a-breakpoint"></a>删除断点
下面描述了删除挂起断点时的过程：

## <a name="deletion-process"></a>删除过程
 会话调试管理器 (SDM) 调用 [IDebugPendingBreakpoint2：:D e) ](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) 方法来删除挂起的断点以及从该断点绑定的所有绑定断点。

> [!NOTE]
> 还可以通过调用 [IDebugBoundBreakpoint2：:D e) ](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)删除单个绑定断点。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
