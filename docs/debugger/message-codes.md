---
title: 消息代码 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- message codes
ms.assetid: 9f91f4e2-c1f1-4349-9f11-2fbbf59654be
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c09245056bf7e947985bfa55dc9cc4a3a96b8cf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62846268"
---
# <a name="message-codes"></a>消息代码
[消息视图](../debugger/messages-view.md)中显示的每行消息均包含“P”、“S”、“s”或“R”代码。 这些代码具有以下含义：

|代码|含义|
|----------|-------------|
|P|该消息已通过 PostMessage 函数发布到队列中。 没有关于该消息的最终处置的可用信息。|
|S|已通过 SendMessage 函数发送该消息。 这意味着，在接收方处理并返回该消息之前，发送方不会重新获得控制权。 因此，接收方可以将返回值传递回发送方。|
|s|已发送该消息，但安全性阻止了对返回值的访问。|
|R|每个“S”行都有对应的“R”（返回）行，后者列出了消息返回值。 有时，消息调用是嵌套的，这意味着一个消息处理程序会发送另一条消息。|