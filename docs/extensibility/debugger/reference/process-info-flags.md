---
title: PROCESS_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e0694d83409a492a1d950a17ac5e2298ba9b8578
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309391"
---
# <a name="processinfoflags"></a>PROCESS_INFO_FLAGS

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
指示该过程是一个系统进程。

`PIFLAG_DEBUGGER_ATTACHED`\
指示由调试器调试该进程。 可能会[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试器，也可能是一些其他调试器，例如，WinDbg。

`PIFLAG_PROCESS_STOPPED`\
指示该进程已停止。 有效才`PIFLAG_DEBUGGER_ATTACHED`还指定了。 可在 Visual Studio 2005 和更高版本。

`PIFLAG_PROCESS_RUNNING`\
指示进程正在运行。 有效才`PIFLAG_DEBUGGER_ATTACHED`还指定了。 可在 Visual Studio 2005 和更高版本。

## <a name="remarks"></a>备注

用于`Flags`的成员[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构。

可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求

标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)