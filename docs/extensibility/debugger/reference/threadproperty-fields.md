---
title: THREADPROPERTY_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9da7b995826b905af7faf6cac3fa0fc3d5ceba5e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316208"
---
# <a name="threadpropertyfields"></a>THREADPROPERTY_FIELDS
指定要检索有关线程的哪些信息。

## <a name="syntax"></a>语法

```cpp
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

## <a name="fields"></a>字段
 `TPF_ID`\
 初始化/用`dwThreadId`字段[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)结构。

 `TPF_SUSPENDCOUNT`\
 初始化/用`dwSuspendCount`字段的`THREADPROPERTIE`S 结构。

 `TPF_STATE`\
 初始化/用`dwThreadState`字段的`THREADPROPERTIE`S 结构。

 `TPF_PRIORITY`\
 初始化/用`bstrPriority`字段的`THREADPROPERTIE`S 结构。

 `TPF_NAME`\
 初始化/用`bstrName`字段的`THREADPROPERTIE`S 结构。

 `TPF_LOCATION`\
 初始化/用`bstrLocation`字段的`THREADPROPERTIE`S 结构。

 `TPF_ALLFIELDS`\
 指定的所有字段。

## <a name="remarks"></a>备注
 这些值会作为参数传递[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)方法，以指示的哪些字段[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)结构是进行初始化。

 中还使用这些值`dwFields`的成员`THREADPROPERTIES`结构，用于指示哪些字段是使用，有效。

 可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)