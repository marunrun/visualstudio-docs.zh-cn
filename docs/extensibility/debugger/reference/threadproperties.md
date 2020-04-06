---
title: 线程属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd0ed4e33b1f8e0e905f3c88493c9f513c177fbc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713420"
---
# <a name="threadproperties"></a>THREADPROPERTIES
描述线程的属性。

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
 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)枚举中的标志的组合，描述此结构中的哪些字段有效。

 `dwThreadId`\
 线程 ID。

 `dwSuspendCount`\
 线程挂起计数。

 `dwThreadState`\
 [来自 THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)枚举的值，指示操作线程的状态。

 `bstrPriority`\
 指定线程优先级的字符串;字符串例如，"高于正常"、"正常"或"时间关键"。

 `bstName`\
 线程名称。

 `bstrLocation`\
 线程位置（通常是最顶层堆栈帧）通常表示为当前停止执行的方法的名称。

## <a name="remarks"></a>备注
 此结构由对[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)方法的调用填充。 返回的信息通常用于填充 **"线程"** 窗口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)
- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
