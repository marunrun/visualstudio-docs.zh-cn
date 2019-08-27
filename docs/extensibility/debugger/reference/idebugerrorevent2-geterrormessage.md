---
title: IDebugErrorEvent2::GetErrorMessage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2::GetErrorMessage
helpviewer_keywords:
- IDebugErrorEvent2::GetErrorMessage
ms.assetid: 9e3b0d74-a2dd-4eaa-bd95-21b2f9c79409
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 049f7a78a414df8202d64c1f25eaba854818c88d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327718"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
返回允许的用户可读的错误消息构造的信息。

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
[out]返回一个值从[MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)描述消息的类型的枚举。

`pbstrErrorFormat`\
[out]向用户最后一条消息的格式 （有关详细信息，请参阅"备注"）。

`hrErrorReason`\
[out]有关消息的错误代码。

`pdwType`\
[out]错误的严重性 (使用的 MB_XXX 常量`MessageBox`; 例如，`MB_EXCLAMATION`或`MB_WARNING`)。

`pbstrHelpFileName`\
[out]帮助文件 （设置为 null 的值，如果没有帮助文件） 的路径。

`pdwHelpId`\
[out]若要显示 （设置为 0，如果没有任何帮助主题） 的帮助主题的 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 错误消息的格式应按一系列`"What I was doing.  %1"`。 `"%1"`将替换为调用方并显示错误消息派生自的错误代码 (其返回`hrErrorReason`)。 `pMessageType`参数指示调用方应如何显示最后一条错误消息。

## <a name="see-also"></a>请参阅
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)