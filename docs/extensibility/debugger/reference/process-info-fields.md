---
title: PROCESS_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe9a1854fe5583d001e1dc156bfad5833fd1c08f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309459"
---
# <a name="processinfofields"></a>PROCESS_INFO_FIELDS
指定要检索进程信息的种类。

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
 初始化/用`bstrFileName`字段[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构。

 `PIF_BASE_NAME`\
 初始化/用`bstrBaseName`字段的`PROCESS_INFO`结构。

 `PIF_TITLE`\
 初始化/用`bstrTitle`字段的`PROCESS_INFO`结构。

 `PIF_PROCESS_ID`\
 初始化/用`ProcessId`字段的`PROCESS_INFO`结构。

 `PIF_SESSION_ID`\
 初始化/用`dwSessionId`字段的`PROCESS_INFO`结构。

 `PIF_ATTACHED_SESSION_NAME`\
 初始化/用`bstrAttachedSessionName`字段的`PROCESS_INFO`结构。

 `PIF_CREATION_TIME`\
 初始化/用`CreationTime`字段的`PROCESS_INFO`结构。

 `PIF_FLAGS`\
 初始化/用`Flags`字段的`PROCESS_INFO`结构。

 `PIF_ALL`\
 填写所有字段。

## <a name="remarks"></a>备注
 传递给[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)方法，以指示的哪些字段[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构是进行初始化。

 中也使用`Fields`字段的`PROCESS_INFO`结构，用于指示哪些字段是使用，有效。

 可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)