---
title: 发送事件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2a2c87b2e05e4ffe94d77333095438f43b644976
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311345"
---
# <a name="send-events"></a>发送事件
调试器与调试引擎 (DE) 之间的通信的机制是基于 DCOM 的事件模型。 为 COM 对象，发送事件和每个事件具有指定的参数：

- DE 调用该事件。

- 发生了什么情况的说明。

- 进程、 程序和线程标识的事件发生的上下文的信息。 该过程不会发送从设备发送的事件。

- 事件类型，该值指示事件是否是同步还是异步。

  使用该方法发送所有调试事件[IDebugEventCallback2::Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)。

## <a name="in-this-section"></a>本节内容
 [事件源](../../extensibility/debugger/event-sources-visual-studio-sdk.md)介绍两个源的事件： 调试引擎 (DE) 和会话调试管理器 (SDM)。

 [支持的事件类型](../../extensibility/debugger/supported-event-types.md)讨论了目前支持的事件类型： 异步和同步。

 [事件描述](../../extensibility/debugger/event-descriptions.md)定义事件和供其使用的原因。

## <a name="related-sections"></a>相关章节
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)介绍 DE 使用解释程序或操作系统提供调试服务的工作方式。