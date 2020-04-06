---
title: PROCESS_INFO_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f81709e7146bbdef13daa3564bb784fd9c08d58e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714012"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
指定要检索进程的信息类型。

## <a name="syntax"></a>语法

```cpp
enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
typedef DWORD PROCESS_INFO_FIELDS;
```

```csharp
public enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
```

## <a name="fields"></a>字段
 `PIF_FILE_NAME`\
 初始化/使用`bstrFileName`[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构的字段。

 `PIF_BASE_NAME`\
 初始化/使用`bstrBaseName`结构字段。 `PROCESS_INFO`

 `PIF_TITLE`\
 初始化/使用`bstrTitle`结构字段。 `PROCESS_INFO`

 `PIF_PROCESS_ID`\
 初始化/使用`ProcessId`结构字段。 `PROCESS_INFO`

 `PIF_SESSION_ID`\
 初始化/使用`dwSessionId`结构字段。 `PROCESS_INFO`

 `PIF_ATTACHED_SESSION_NAME`\
 初始化/使用`bstrAttachedSessionName`结构字段。 `PROCESS_INFO`

 `PIF_CREATION_TIME`\
 初始化/使用`CreationTime`结构字段。 `PROCESS_INFO`

 `PIF_FLAGS`\
 初始化/使用`Flags`结构字段。 `PROCESS_INFO`

 `PIF_ALL`\
 填写所有字段。

## <a name="remarks"></a>备注
 传递给[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)方法，指示要初始化[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构的哪些字段。

 还用于`Fields`结构字段，`PROCESS_INFO`以指示使用哪些字段有效。

 这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
