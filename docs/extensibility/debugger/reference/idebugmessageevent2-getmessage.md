---
title: IDebugMessageEvent2::GetMessage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2::GetMessage
helpviewer_keywords:
- GetMessage method
- IDebugMessageEvent2::GetMessage method
ms.assetid: 9fca7285-f7f1-422d-8565-92bf0e0db60a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 758b3b860167ed8c2db8bb20c0d76ab289e39a0f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346896"
---
# <a name="idebugmessageevent2getmessage"></a>IDebugMessageEvent2::GetMessage
获取要显示的消息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMessage( 
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrMessage,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetMessage( 
   out enum_MESSAGETYPE pMessageType,
   out string           pbstrMessage,
   out uint             pdwType,
   out string           pbstrHelpFileName,
   out uint             dwHelpId
);
```

## <a name="parameters"></a>参数
`pMessageType`\
[out]返回一个值从[MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)枚举，用于描述消息的类型。

`pbstrMessage`\
[out]返回的消息。

`pdwType`\
[out]返回使用 Win32 的约定的消息的类型`MessageBox`函数。 请参阅[AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)函数的详细信息。

`pbstrHelpFileName`\
[in、 out]返回的帮助文件名称。 可能为 null (C++) 或为空 (C#) 如果没有帮助文件，则值。

`pdwHelpId`\
[in、 out]返回的帮助标识符。 可能是 0，如果没有帮助与此消息关联。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
- [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)