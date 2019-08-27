---
title: IDebugMessageEvent2::GetMessage | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2::GetMessage
helpviewer_keywords:
- GetMessage method
- IDebugMessageEvent2::GetMessage method
ms.assetid: 9fca7285-f7f1-422d-8565-92bf0e0db60a
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 14eb540962db3a806273d5c76facb7f9bf25dee7
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685900"
---
# <a name="idebugmessageevent2getmessage"></a>IDebugMessageEvent2::GetMessage
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取要显示的消息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
  
#### <a name="parameters"></a>参数  
 `pMessageType`  
 [out]返回一个值从[MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)枚举，用于描述消息的类型。  
  
 `pbstrMessage`  
 [out]返回的消息。  
  
 `pdwType`  
 [out]返回使用 Win32 的约定的消息的类型`MessageBox`函数。 请参阅[AfxMessageBox](https://msdn.microsoft.com/library/d66d0328-cdcc-48f6-96a4-badf089099c8)函数的详细信息。  
  
 `pbstrHelpFileName`  
 [in、 out]返回的帮助文件名称。 可能为 null (C++) 或为空 (C#) 如果没有帮助文件，则值。  
  
 `pdwHelpId`  
 [in、 out]返回的帮助标识符。 可能是 0，如果没有帮助与此消息关联。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)   
 [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)   
 [AfxMessageBox](https://msdn.microsoft.com/library/d66d0328-cdcc-48f6-96a4-badf089099c8)
