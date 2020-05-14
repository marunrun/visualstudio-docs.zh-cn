---
title: PROCESS_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO
helpviewer_keywords:
- PROCESS_INFO structure
ms.assetid: 260c33cc-a05e-4645-84b6-536d0b3b0537
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef73145fb0a2598dc5e4ee98e8652314e0bc1c89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713886"
---
# <a name="process_info"></a>PROCESS_INFO
包含有关进程的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct tagPROCESS_INFO { 
   PROCESS_INFO_FIELDS Fields;
   BSTR                bstrFileName;
   BSTR                bstrBaseName;
   BSTR                bstrTitle;
   AD_PROCESS_ID       ProcessId;
   DWORD               dwSessionId;
   BSTR                bstrAttachedSessionName;
   FILETIME            CreationTime;
   PROCESS_INFO_FLAGS  Flags;
} PROCESS_INFO;
```

```csharp
public struct PROCESS_INFO { 
   public uint          Fields;
   public string        bstrFileName;
   public string        bstrBaseName;
   public string        bstrTitle;
   public AD_PROCESS_ID ProcessId;
   public uint          dwSessionId;
   public string        bstrAttachedSessionName;
   public FILETIME      CreationTime;
   public uint          Flags;
};
```

## <a name="members"></a>成员
 `Fields`\
 [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)枚举中的标志的组合，用于指定填写哪些字段。

 `bstrFileName`\
 进程的完整路径名称。 等效于使用 参数`GN_FILENAME`调用[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)方法。

 `bstrBaseName`\
 进程的文件名和扩展名。 等效于使用`IDebugProcess2::Getname`参数`GN_BASENAME`调用 方法。

 `bstrTitle`\
 进程的标题（如果存在）。 等效于使用`IDebugProcess2::Getname`参数`GN_TITLE`调用 方法。

 `ProcessId`\
 标识进程的[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。 等效于调用[Get物理进程 Id](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)方法。

 `dwSessionId`\
 此过程正在运行的调试会话的标识符。

 `bstrAttachedSessionName`\
 附加的会话名称。 等效于调用[Get 附加会话名称](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)方法。

 `CreationTime`\
 创建流程的时间。

 `Flags`\
 [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)枚举中标记的组合，用于指定进程的属性。

## <a name="remarks"></a>备注
 此结构传递给填写它的[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)方法。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
- [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)
- [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)
