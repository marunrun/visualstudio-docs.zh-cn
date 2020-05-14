---
title: 消息枚举器 |微软文档
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
ms.openlocfilehash: 0e09b72bd228839268cffc228dd0dc503cc82bd9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702507"
---
# <a name="message-enumerator"></a>消息枚举器
以下标志用于`TEXTOUTPROC`函数，该函数是 IDE 在调用[SccOpenProject](../extensibility/sccopenproject-function.md)时提供的回调函数（有关回调函数的详细信息，请参阅[LPTEXTOUTPROC）。](../extensibility/lptextoutproc.md)

 如果要求 IDE 取消进程，它可能会收到取消消息之一。 在这种情况下，源代码管理插件用于`SCC_MSG_STARTCANCEL`要求 IDE 显示 **"取消"** 按钮。 在此之后，可能会发送任何一组正常消息。 如果其中任何一个`SCC_MSG_RTN_CANCEL`返回，则插件将退出该操作并返回。 插件还会定期轮询`SCC_MSG_DOCANCEL`以确定用户是否已取消该操作。 完成所有操作或用户已取消操作后，插件将发送`SCC_MSG_STOPCANCEL`。 SCC_MSG_WARNING`SCC_MSG_INFO`和SCC_MSG_ERROR类型用于显示在消息滚动列表中的邮件。 `SCC_MSG_STATUS`是一种特殊类型，指示文本应显示在状态栏或临时显示区域中。 它不会永久保留在列表中。

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
 SCC_MSG_RTN_CANCEL从回调返回以指示取消。

 SCC_MSG_RTN_OK从回调返回以继续。

 SCC_MSG_INFO消息是信息性的。

 SCC_MSG_WARNING消息是一个警告。

 SCC_MSG_ERROR消息是一个错误。

 SCC_MSG_STATUS消息用于状态栏。

 SCC_MSG_DOCANCEL 无文本;IDE`SCC_MSG_RTN_OK`返回`SCC_MSG_RTN_CANCEL`或 。

 SCC_MSG_STARTCANCEL启动取消循环。

 SCC_MSG_STOPCANCEL 停止取消循环。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
