---
title: THREADPROPERTIES |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4815a1e42b98fba812e8a3c2a53516bff16081db
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204821"
---
# <a name="threadproperties"></a>THREADPROPERTIES
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

介绍在线程的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _tagTHREADPROPERTIES {   
   THREADPROPERTY_FIELDS dwFields;  
   DWORD                 dwThreadId;  
   DWORD                 dwSuspendCount;  
   DWORD                 dwThreadState;  
   BSTR                  bstrPriority;  
   BSTR                  bstrName;  
   BSTR                  bstrLocation;  
} THREADPROPERTIES;  
```  
  
```csharp  
public struct THREADPROPERTIES {   
   public uint   dwFields;  
   public uint   dwThreadId;  
   public uint   dwSuspendCount;  
   public uint   dwThreadState;  
   public string bstrPriority;  
   public string bstrName;  
   public string bstrLocation;  
};  
```  
  
## <a name="members"></a>成员  
 dwFields  
 中的标志的组合[THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)描述此结构中的哪些字段有效的枚举。  
  
 dwThreadId  
 线程 id。  
  
 dwSuspendCount  
 在线程挂起计数。  
  
 dwThreadState  
 中的值[THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)枚举，指示操作系统线程的状态。  
  
 bstrPriority  
 一个字符串，指定线程的优先级。例如，"高于正常"、"Normal"或者"时间关键"。  
  
 bstName  
 线程名称。  
  
 bstrLocation  
 线程位置 （通常最顶层的堆栈帧），通常都表示为当前暂停执行方法的名称。  
  
## <a name="remarks"></a>备注  
 此结构通过调用来填充[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)方法。 因此返回的信息通常用于填充**线程**窗口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)   
 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)   
 [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
