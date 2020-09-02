---
title: IDebugErrorEvent2：： GetErrorMessage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2::GetErrorMessage
helpviewer_keywords:
- IDebugErrorEvent2::GetErrorMessage
ms.assetid: 9e3b0d74-a2dd-4eaa-bd95-21b2f9c79409
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1ff1da2f2a2d24b958a613e6fe5cb58c0081ed3e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730041"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
返回允许构造用户可读错误消息的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetErrorMessage(
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrErrorFormat,
   HRESULT*     hrErrorReason,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetErrorMessage(
   out enum_MESSAGETYPE   pMessageType,
   out string             pbstrErrorFormat,
   out int                phrErrorReason,
   out uint               pdwType,
   out string             pbstrHelpFileName,
   out uint               pdwHelpId
);
```

## <a name="parameters"></a>参数
`pMessageType`\
弄从 [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 枚举返回一个值，用于描述消息的类型。

`pbstrErrorFormat`\
弄用户的最终消息格式 (参阅 "备注" 以了解详细信息) 。

`hrErrorReason`\
弄消息的错误代码。

`pdwType`\
弄错误的严重性 (将 MB_XXX 常量用于 `MessageBox` ; 例如 `MB_EXCLAMATION` 或 `MB_WARNING`) 。

`pbstrHelpFileName`\
弄帮助文件的路径 (如果没有) 的帮助文件，则将设置为 null 值。

`pdwHelpId`\
弄要显示的帮助主题的 ID (如果没有) 的帮助主题，则设置为0。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 错误消息应按照的行格式设置 `"What I was doing.  %1"` 。 `"%1"`然后，调用方会将其替换为错误代码，此错误消息派生自) 中返回 (`hrErrorReason` 。 `pMessageType`参数告知调用方应如何显示最终的错误消息。

## <a name="see-also"></a>另请参阅
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
