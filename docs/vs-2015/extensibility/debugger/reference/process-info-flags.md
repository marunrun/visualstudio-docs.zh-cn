---
title: PROCESS_INFO_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
ms.assetid: 696951ce-701a-40c2-ac8c-b897f3aae6e2
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 88ff2a1da1f937fd4011932979bd95057eb40dfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205055"
---
# <a name="process_info_flags"></a>PROCESS_INFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述或指定进程的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
  
## <a name="members"></a>成员  
 PIFLAG_SYSTEM_PROCESS  
 指示进程是系统进程。  
  
 PIFLAG_DEBUGGER_ATTACHED  
 指示调试器正在调试该进程。 它可能是一个 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 调试器，也可能是其他一些调试器，例如 WinDbg。  
  
 PIFLAG_PROCESS_STOPPED  
 指示进程已停止。 仅当 `PIFLAG_DEBUGGER_ATTACHED` 还指定了时才有效。 在 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 和更高版本中可用。  
  
 PIFLAG_PROCESS_RUNNING  
 指示进程正在运行。 仅当 `PIFLAG_DEBUGGER_ATTACHED` 还指定了时才有效。 在 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 和更高版本中可用。  
  
## <a name="remarks"></a>备注  
 用于 `Flags` [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 结构的成员。  
  
 这些标志可以与按位组合 `OR` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
