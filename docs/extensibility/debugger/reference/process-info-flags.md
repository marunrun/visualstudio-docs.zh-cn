---
title: PROCESS_INFO_FLAGS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 36c4cbbe17a109eacd69b76500e8c10d21d2d554
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713955"
---
# <a name="process_info_flags"></a>PROCESS_INFO_FLAGS

描述或指定进程的属性。

## <a name="syntax"></a>语法

```cpp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
typedef DWORD PROCESS_INFO_FLAGS;
```

```csharp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
```

## <a name="fields"></a>字段

`PIFLAG_SYSTEM_PROCESS`\
指示该过程是系统进程。

`PIFLAG_DEBUGGER_ATTACHED`\
指示调试器正在调试进程。 它可能是调试[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]器，或者可能是其他调试器，例如 WinDbg。

`PIFLAG_PROCESS_STOPPED`\
指示进程已停止。 仅在也指定`PIFLAG_DEBUGGER_ATTACHED`时有效。 可在 Visual Studio 2005 及更高版本提供。

`PIFLAG_PROCESS_RUNNING`\
指示进程正在运行。 仅在也指定`PIFLAG_DEBUGGER_ATTACHED`时有效。 可在 Visual Studio 2005 及更高版本提供。

## <a name="remarks"></a>备注

用于[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构`Flags`的成员。

这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求

标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅

- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
