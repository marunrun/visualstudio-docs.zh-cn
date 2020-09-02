---
title: THREADPROPERTY_FIELDS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dc0e0f7cae4aed887809c22bda0cd6a9ed50307f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204808"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索的有关线程的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_THREADPROPERTY_FIELDS {   
   TPF_ID           = 0x0001,  
   TPF_SUSPENDCOUNT = 0x0002,  
   TPF_STATE        = 0x0004,  
   TPF_PRIORITY     = 0x0008,  
   TPF_NAME         = 0x0010,  
   TPF_LOCATION     = 0x0020,  
   TPF_ALLFIELDS    = 0xffffffff  
};  
typedef DWORD THREADPROPERTY_FIELDS;  
```  
  
```csharp  
public enum enum_THREADPROPERTY_FIELDS {   
   TPF_ID           = 0x0001,  
   TPF_SUSPENDCOUNT = 0x0002,  
   TPF_STATE        = 0x0004,  
   TPF_PRIORITY     = 0x0008,  
   TPF_NAME         = 0x0010,  
   TPF_LOCATION     = 0x0020,  
   TPF_ALLFIELDS    = 0xffffffff  
};  
```  
  
## <a name="members"></a>成员  
 TPF_ID  
 初始化/使用 `dwThreadId` [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 结构的字段。  
  
 TPF_SUSPENDCOUNT  
 初始化/使用 `dwSuspendCount` S 结构的字段 `THREADPROPERTIE` 。  
  
 TPF_STATE  
 初始化/使用 `dwThreadState` S 结构的字段 `THREADPROPERTIE` 。  
  
 TPF_PRIORITY  
 初始化/使用 `bstrPriority` S 结构的字段 `THREADPROPERTIE` 。  
  
 TPF_NAME  
 初始化/使用 `bstrName` S 结构的字段 `THREADPROPERTIE` 。  
  
 TPF_LOCATION  
 初始化/使用 `bstrLocation` S 结构的字段 `THREADPROPERTIE` 。  
  
 TPF_ALLFIELDS  
 指定所有字段。  
  
## <a name="remarks"></a>备注  
 这些值作为参数传递给 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) 方法，以指示要初始化 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 结构的哪些字段。  
  
 这些值还用于 `dwFields` 结构的成员，用于 `THREADPROPERTIES` 指示哪些字段已使用并且有效。  
  
 这些标志可以与按位组合 `OR` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)   
 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
