---
title: THREADPROPERTIES |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a0e39102fa66c04a15042ffd82086ac66d3058ca
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316174"
---
# <a name="threadproperties"></a>THREADPROPERTIES
介绍在线程的属性。

## <a name="syntax"></a>语法

```cpp
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
 `dwFields`\
 中的标志的组合[THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)描述此结构中的哪些字段有效的枚举。

 `dwThreadId`\
 线程 id。

 `dwSuspendCount`\
 在线程挂起计数。

 `dwThreadState`\
 中的值[THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)枚举，指示操作系统线程的状态。

 `bstrPriority`\
 一个字符串，指定线程的优先级。例如，"高于正常"、"Normal"或者"时间关键"。

 `bstName`\
 线程名称。

 `bstrLocation`\
 线程位置 （通常最顶层的堆栈帧），通常都表示为当前暂停执行方法的名称。

## <a name="remarks"></a>备注
 此结构通过调用来填充[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)方法。 因此返回的信息通常用于填充**线程**窗口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)
- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)