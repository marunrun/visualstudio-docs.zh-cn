---
title: IDebug消息事件2：：获取消息 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2::GetMessage
helpviewer_keywords:
- GetMessage method
- IDebugMessageEvent2::GetMessage method
ms.assetid: 9fca7285-f7f1-422d-8565-92bf0e0db60a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 819b796a656f0ef8775fbb1c9e800e3019b81729
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727396"
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
[出]从[消息类型](../../../extensibility/debugger/reference/messagetype.md)枚举中返回描述消息类型的值。

`pbstrMessage`\
[出]返回消息。

`pdwType`\
[出]使用 Win32`MessageBox`函数的约定返回消息的类型。 有关详细信息，请参阅[AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)功能。

`pbstrHelpFileName`\
[进出]返回帮助文件名。 如果没有帮助文件，则可能是空（C++）或空 （C#） 值。

`pdwHelpId`\
[进出]返回帮助标识符。 如果没有与此消息关联的帮助，则可能是 0。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [消息类型](../../../extensibility/debugger/reference/messagetype.md)
- [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)
