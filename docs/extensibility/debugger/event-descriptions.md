---
title: 活动描述 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 09f61652-7e16-4bb0-8055-f61a84bf384e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3c2582717fd4da3b833da90a951f9b8f72a59f71
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738786"
---
# <a name="event-descriptions"></a>事件描述
每种类型的事件都有特定用途。

## <a name="events-and-the-reasons-for-their-use"></a>事件及其使用原因

|事件|描述|
|-----------|-----------------|
|激活文档事件|当调试引擎 （DE） 希望 IDE 打开或将文档带到前台时发生。|
|断点绑定或断点错误事件|在绑定断点或断点无法绑定并返回错误时发送。|
|断点未绑定事件|当绑定断点从代码中取消绑定时发生。|
|可以停止事件|发送到 IDE 以确定用户是否要在代码中的指定点停止。|
|断点事件|当发生代码或数据断点时发生。|
|文档文本事件|当更改文档中的文本时发生。 这些事件不会通过 方法`IDebugEventCallBack2::Event`发送。|
|引擎创建事件|首次创建引擎时发送。|
|入口点事件|当正在调试的程序已运行其初始化代码并到达其第一个用户入口点时发送。|
|异常事件|当正在运行的程序遇到异常时发送。|
|表达式计算完成事件|异步表达式计算完成后发送。|
|查找符号事件|每当 DE 需要要求用户查找模块的符号时，都会发送。|
|加载完整事件|仅当初始程序加载完成且第一个代码即将在程序中运行时才发送。|
|消息事件|向用户发送消息时发送。|
|模块加载事件|加载或卸载新模块时发送。|
|输出字符串事件|程序写入调试输出时发送。|
|创建和销毁事件|已发送以宣布进程、程序、属性、会话和线程的创建或销毁，以便 Visual Studio IDE 可以跟踪正在调试的程序的状态。|
|步骤完成事件|步骤完成后发送。|
|线程名称更改事件|当用户更改线程的名称时发送。|
|程序名称更改事件|当用户更改程序名称时发送。|

## <a name="see-also"></a>请参阅
- [发送事件](../../extensibility/debugger/sending-events.md)
