---
title: MESSAGETYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c17564c992f4c8855d8a96165975a5d0e132755c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547203"
---
# <a name="messagetype"></a>MESSAGETYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定消息类型和原因。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_MESSAGETYPE {   
   MT_OUTPUTSTRING      = 0x0000001,  
   MT_MESSAGEBOX        = 0x00000002,  
   MT_TYPE_MASK         = 0x000000FF,  
   MT_REASON_EXCEPTION  = 0x00000100,  
   MT_REASON_TRACEPOINT = 0x00000200,  
   MT_REASON_MASK       = 0x0000FF00  
};  
typedef DWORD MESSAGETYPE;  
```  
  
```csharp  
public enum enum_MESSAGETYPE {   
   MT_OUTPUTSTRING      = 0x0000001,  
   MT_MESSAGEBOX        = 0x00000002,  
   MT_TYPE_MASK         = 0x000000FF,  
   MT_REASON_EXCEPTION  = 0x00000100,  
   MT_REASON_TRACEPOINT = 0x00000200,  
   MT_REASON_MASK       = 0x0000FF00  
};  
```  
  
## <a name="members"></a>成员  
 MT_OUTPUTSTRING  
 指示应将消息发送到 "输出" 窗口。 这与互斥 `MT_MESSAGEBOX` 。  
  
 MT_MESSAGEBOX  
 指示消息应显示在消息框中。 这与互斥 `MT_OUTPUTSTRING` 。  
  
 MT_TYPE_MASK  
 用于隔离消息目标的掩码值。  
  
 MT_REASON_EXCEPTION  
 指示由于异常而显示的消息框。 这与互斥 `MT_REASON_TRACEPOINT` 。  
  
 MT_REASON_TRACEPOINT  
 指示由于命中跟踪点而显示的消息框。 这与互斥 `MT_REASON_EXCEPTION` 。  
  
 MT_REASON_MASK  
 用于隔离正在显示的消息原因的掩码值。  
  
## <a name="remarks"></a>备注  
 这些值从 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md) 和 [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md) 方法返回。  
  
 其中一个原因值可以使用按位与某个输出目标值相结合 `OR` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)   
 [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
