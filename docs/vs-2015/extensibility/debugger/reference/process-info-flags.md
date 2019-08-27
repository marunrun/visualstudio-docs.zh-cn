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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205055"
---
# <a name="processinfoflags"></a>PROCESS_INFO_FLAGS
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
 指示该过程是一个系统进程。  
  
 PIFLAG_DEBUGGER_ATTACHED  
 指示由调试器调试该进程。 可能会[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]调试器，也可能是一些其他调试器，例如，WinDbg。  
  
 PIFLAG_PROCESS_STOPPED  
 指示该进程已停止。 有效才`PIFLAG_DEBUGGER_ATTACHED`还指定了。 中提供[!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]及更高版本。  
  
 PIFLAG_PROCESS_RUNNING  
 指示进程正在运行。 有效才`PIFLAG_DEBUGGER_ATTACHED`还指定了。 中提供[!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]及更高版本。  
  
## <a name="remarks"></a>备注  
 用于`Flags`的成员[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)结构。  
  
 可能的按位组合这些标志`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
