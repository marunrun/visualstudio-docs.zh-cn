---
title: THREADPROPERTY_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b31c43187d1136f7a194c42749c430de6cd064a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713401"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
指定要检索的线程信息。

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
 初始化/使用`dwThreadId`[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)结构的字段。

 `TPF_SUSPENDCOUNT`\
 初始化/使用`dwSuspendCount`S 结构`THREADPROPERTIE`的字段。

 `TPF_STATE`\
 初始化/使用`dwThreadState`S 结构`THREADPROPERTIE`的字段。

 `TPF_PRIORITY`\
 初始化/使用`bstrPriority`S 结构`THREADPROPERTIE`的字段。

 `TPF_NAME`\
 初始化/使用`bstrName`S 结构`THREADPROPERTIE`的字段。

 `TPF_LOCATION`\
 初始化/使用`bstrLocation`S 结构`THREADPROPERTIE`的字段。

 `TPF_ALLFIELDS`\
 指定所有字段。

## <a name="remarks"></a>备注
 这些值作为参数传递给[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)方法，以指示要初始化[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)结构的字段。

 这些值还用于结构`dwFields`的成员中`THREADPROPERTIES`，以指示使用哪些字段有效。

 这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
