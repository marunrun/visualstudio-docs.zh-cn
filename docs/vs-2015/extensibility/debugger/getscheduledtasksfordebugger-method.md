---
title: GetScheduledTasksForDebugger 方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- GetScheduledTasksForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 7c9b4cde-6e4a-4cef-929f-7d02b1da5762
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b4ac6fa753be7672f1e698bda231bd11217c10d4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152730"
---
# <a name="getscheduledtasksfordebugger-method"></a>GetScheduledTasksForDebugger 方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索所有计划任务的数组。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly：** mscorlib (mscorlib.dll)   
  
 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。  
  
## <a name="syntax"></a>语法  
  
```  
.method assembly hidebysig instance class System.Threading.Tasks.Task[] GetScheduledTasksForDebugger() cil managed  
```  
  
## <a name="return-value"></a>返回值  
 所有计划任务的数组。 每个任务正在执行或已完成执行。  
  
## <a name="remarks"></a>备注  
 此方法不是线程安全的，不应与它的其他实例一起使用 <xref:System.Threading.Tasks.TaskScheduler> 。仅当调试器挂起了所有其他线程时，才应从调试器调用此方法。  
  
## <a name="see-also"></a>另请参阅  
 [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md)
