---
title: 消息代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- message codes
ms.assetid: 9f91f4e2-c1f1-4349-9f11-2fbbf59654be
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 92cc911b0217a406302553b3d913c032fc915b4c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182967"
---
# <a name="message-codes"></a>消息代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[消息视图](../debugger/messages-view.md)中显示的每行消息均包含“P”、“S”、“s”或“R”代码。 这些代码具有以下含义：  
  
|代码|含义|  
|----------|-------------|  
|P|该消息已通过 PostMessage 函数发布到队列中。 没有关于该消息的最终处置的可用信息。|  
|S|已通过 SendMessage 函数发送该消息。 这意味着，在接收方处理并返回该消息之前，发送方不会重新获得控制权。 因此，接收方可以将返回值传递回发送方。|  
|s|已发送该消息，但安全性阻止了对返回值的访问。|  
|R|每个“S”行都有对应的“R”（返回）行，后者列出了消息返回值。 有时，消息调用是嵌套的，这意味着一个消息处理程序会发送另一条消息。|
