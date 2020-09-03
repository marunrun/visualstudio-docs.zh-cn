---
title: GetTaskSchedulersForDebugger 方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 995bf40669a4480f6f1ddfe8071a7885a4659c9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152712"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger 方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索 <xref:System.Threading.Tasks.TaskScheduler> 当前处于活动状态的所有对象的数组。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly：** mscorlib (mscorlib.dll)   
  
 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。  
  
## <a name="syntax"></a>语法  
  
```  
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed  
```  
  
## <a name="return-value"></a>返回值  
 <xref:System.Threading.Tasks.TaskScheduler>此中当前处于活动状态的所有对象的数组 <xref:System.AppDomain> 。  
  
## <a name="remarks"></a>备注  
 此方法不是线程安全的，不应与的其他实例同时使用 <xref:System.Threading.Tasks.TaskScheduler> 。 仅当调试器挂起了所有其他线程时，才应从调试器调用此方法。  
  
## <a name="see-also"></a>另请参阅  
 [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md)
