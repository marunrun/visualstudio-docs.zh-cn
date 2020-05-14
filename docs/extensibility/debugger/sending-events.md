---
title: 发送事件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5ec0d3aa29da562147b71b8efde49baf07d8ae0b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713032"
---
# <a name="send-events"></a>发送事件
调试器和调试引擎 （DE） 之间的通信机制是基于 DCOM 的事件模型。 事件作为 COM 对象发送，每个事件都有指定：

- 调用事件的 DE。

- 所发生的事情的描述。

- 标识事件发生地上下文的进程、程序和线程信息。 不会为从 DE 发送的事件发送进程。

- 指示事件是同步事件还是异步的事件类型。

  所有调试事件都使用[IDebugEvent 回调2：：事件](../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送。

## <a name="in-this-section"></a>在本节中
 [事件源](../../extensibility/debugger/event-sources-visual-studio-sdk.md)解释两个事件源：调试引擎 （DE） 和会话调试管理器 （SDM）。

 [受支持的事件类型](../../extensibility/debugger/supported-event-types.md)讨论当前支持的事件类型：异步和同步。

 [事件描述](../../extensibility/debugger/event-descriptions.md)定义事件及其使用原因。

## <a name="related-sections"></a>相关章节
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)描述 DE 如何与解释器或操作系统一起提供调试服务。
