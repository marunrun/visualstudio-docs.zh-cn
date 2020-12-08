---
title: 发送事件 |Microsoft Docs
description: 了解调试器和调试引擎如何使用基于 DCOM 的事件模型。 事件作为 COM 对象发送。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 0262868ae442bfdd8b99c16f59e000f4ebfc35c5
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847905"
---
# <a name="send-events"></a>发送事件
调试器和调试引擎之间通信的机制 (DE) 是基于 DCOM 的事件模型。 事件作为 COM 对象发送，并且每个事件都有指定以下各项的参数：

- 调用事件的 DE。

- 发生了什么情况的说明。

- 标识发生事件的上下文的进程、程序和线程信息。 对于从 DE 发送的事件，不会发送此进程。

- 指示事件是同步事件还是异步事件的事件类型。

  所有调试事件都是使用 [IDebugEventCallback2：： Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法发送的。

## <a name="in-this-section"></a>在本节中
 [事件源](../../extensibility/debugger/event-sources-visual-studio-sdk.md) 说明两个事件源：调试引擎 (DE) 和会话调试管理器 (SDM) 。

 [支持的事件类型](../../extensibility/debugger/supported-event-types.md) 讨论当前支持的事件类型：异步和同步。

 [事件说明](../../extensibility/debugger/event-descriptions.md) 定义事件及其使用原因。

## <a name="related-sections"></a>相关章节
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md) 介绍如何使用解释器或操作系统来提供调试服务。
