---
title: TaskScheduler 类-内部成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TaskScheduler class [.NET Framework debug engines]
- debug engines, TaskScheduler class [.NET Framework]
ms.assetid: 87f1c969-0217-4464-8907-7609c1bf61d3
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 427a84b3dcda0471f5ec9d71883a5a8e859bb92d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176704"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler 类 - 内部成员
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本主题介绍 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> 可帮助你实现自定义调试器的类的内部成员。 有关此类的常规信息，请参阅 <xref:System.Threading.Tasks.TaskScheduler> 参考主题。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly：** mscorlib (mscorlib.dll)   
  
 由于无法从 .NET Framework 访问这些内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。  
  
## <a name="syntax"></a>语法  
  
```  
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler  
       extends System.Object  
```  
  
## <a name="members"></a>成员  
  
### <a name="methods"></a>方法  
  
|名称|说明|  
|----------|-----------------|  
|[GetScheduledTasksForDebugger](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|检索所有计划任务的数组。|  
|[GetTaskSchedulersForDebugger](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|检索 <xref:System.Threading.Tasks.TaskScheduler> 当前处于活动状态的所有对象的数组。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>   
 [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
