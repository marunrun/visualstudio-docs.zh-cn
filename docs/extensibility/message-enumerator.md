---
title: 消息枚举器 |Microsoft Docs
description: 此枚举器的成员用于 TEXTOUTPROC 函数，该函数是 IDE 在调用 SccOpenProject 时提供的回调函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- message enumerator
- source control plug-ins, message enumeration
ms.assetid: 4a4faa0d-d352-40ea-a21d-c09ea286a8e1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1a7d4607afd9b46d35db416baed73007c67a7832
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863730"
---
# <a name="message-enumerator"></a>消息枚举器
以下标志用于 `TEXTOUTPROC` 函数，该函数是 IDE 在调用 [SccOpenProject](../extensibility/sccopenproject-function.md) 时提供的回调函数 (请参阅 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) ，以获取回调函数) 的详细信息。

 如果要求 IDE 取消此过程，则可能会收到一条 "取消" 消息。 在这种情况下，源代码管理插件使用 `SCC_MSG_STARTCANCEL` 来请求 IDE 显示 " **取消** " 按钮。 此后，可能会发送一组普通消息。 如果其中有任何返回 `SCC_MSG_RTN_CANCEL` ，则插件将退出操作并返回。 此插件还会定期轮询 `SCC_MSG_DOCANCEL` 以确定用户是否已取消该操作。 完成所有操作后，如果用户已取消，则插件将发送 `SCC_MSG_STOPCANCEL` 。 `SCC_MSG_INFO`、SCC_MSG_WARNING 和 SCC_MSG_ERROR 类型用于显示在消息滚动列表中的消息。 `SCC_MSG_STATUS` 是一种特殊类型，指示文本应显示在状态栏或临时显示区域中。 它不会永久保留在列表中。

## <a name="syntax"></a>语法

```
enum { 
   SCC_MSG_RTN_CANCEL = -1, 
   SCC_MSG_RTN_OK = 0, 
   SCC_MSG_INFO = 1 
   SCC_MSG_WARNING, 
   SCC_MSG_ERROR, 
   SCC_MSG_STATUS, 
   SCC_MSG_DOCANCEL, 
   SCC_MSG_STARTCANCEL, 
   SCC_MSG_STOPCANCEL 
};
```

## <a name="members"></a>成员
 SCC_MSG_RTN_CANCEL 从回调返回以指示取消。

 SCC_MSG_RTN_OK 从回调返回以继续。

 SCC_MSG_INFO 消息为信息性消息。

 SCC_MSG_WARNING 消息是一个警告。

 SCC_MSG_ERROR 消息为错误。

 SCC_MSG_STATUS 消息用于状态栏。

 SCC_MSG_DOCANCEL 无文本;IDE 将返回 `SCC_MSG_RTN_OK` 或 `SCC_MSG_RTN_CANCEL` 。

 SCC_MSG_STARTCANCEL 启动 "取消" 循环。

 SCC_MSG_STOPCANCEL 停止 "取消" 循环。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
