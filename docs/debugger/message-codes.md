---
title: 消息代码 | Microsoft Docs
description: 了解消息视图的每个消息行上显示的消息代码的含义。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: e4b836a5d4c1faad6b4c0375e2ec51d759816889
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903605"
---
# <a name="message-codes"></a>消息代码
[消息视图](../debugger/messages-view.md)中显示的每行消息均包含“P”、“S”、“s”或“R”代码。 这些代码具有以下含义：

|代码|含义|
|----------|-------------|
|P|该消息已通过 PostMessage 函数发布到队列中。 没有关于该消息的最终处置的可用信息。|
|S|已通过 SendMessage 函数发送该消息。 这意味着，在接收方处理并返回该消息之前，发送方不会重新获得控制权。 因此，接收方可以将返回值传递回发送方。|
|s|已发送该消息，但安全性阻止了对返回值的访问。|
|R|每个“S”行都有对应的“R”（返回）行，后者列出了消息返回值。 有时，消息调用是嵌套的，这意味着一个消息处理程序会发送另一条消息。|