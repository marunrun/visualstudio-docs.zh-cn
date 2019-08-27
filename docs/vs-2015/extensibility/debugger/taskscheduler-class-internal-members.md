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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68176704"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler 类 - 内部成员
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本主题介绍的内部成员的<xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>类，可帮助您实现自定义调试器。 有关此类的常规信息，请参阅<xref:System.Threading.Tasks.TaskScheduler>参考主题。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问这些内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler  
       extends System.Object  
```  
  
## <a name="members"></a>成员  
  
### <a name="methods"></a>方法  
  
|name|描述|  
|----------|-----------------|  
|[GetScheduledTasksForDebugger](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|检索所有计划任务的数组。|  
|[GetTaskSchedulersForDebugger](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|检索的所有数组<xref:System.Threading.Tasks.TaskScheduler>当前处于活动状态的对象。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>   
 [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
