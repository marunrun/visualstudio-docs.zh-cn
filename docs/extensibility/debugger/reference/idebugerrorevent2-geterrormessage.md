---
title: IDebugError事件2：：获取错误消息 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730041"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
返回允许构造人类可读错误消息的信息。

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
[出]从[消息类型](../../../extensibility/debugger/reference/messagetype.md)枚举中返回一个值，描述消息的类型。

`pbstrErrorFormat`\
[出]向用户发送的最后消息的格式（有关详细信息，请参阅"备注"）。

`hrErrorReason`\
[出]消息所讲述的错误代码。

`pdwType`\
[出]错误的严重性（使用`MessageBox`MB_XXX常量; `MB_EXCLAMATION` `MB_WARNING`

`pbstrHelpFileName`\
[出]帮助文件的路径（如果没有帮助文件，则设置为空值）。

`pdwHelpId`\
[出]要显示的帮助主题的 ID（如果没有帮助主题，则设置为 0）。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 错误消息的格式应沿`"What I was doing.  %1"`的 行。 然后`"%1"`，调用方将替换为从错误代码派生的错误消息（在 中`hrErrorReason`返回）。 参数`pMessageType`告诉调用方如何显示最终错误消息。

## <a name="see-also"></a>请参阅
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [消息类型](../../../extensibility/debugger/reference/messagetype.md)
