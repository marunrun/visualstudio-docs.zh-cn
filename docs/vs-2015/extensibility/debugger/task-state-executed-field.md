---
title: TASK_STATE_EXECUTED 字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_EXECUTED field, Task class [.NET Framework debug engines]
ms.assetid: 75b8f9d0-b908-40d0-b109-70feaed2ab0c
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6dcfb6c7b4b79d1abd2b393e32b9795f613c205a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162223"
---
# <a name="taskstateexecuted-field"></a>TASK_STATE_EXECUTED 字段
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

该任务正在运行，但尚未完成。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.field static assembly literal int32 TASK_STATE_EXECUTED = int32(0x00020000)  
```  
  
## <a name="remarks"></a>备注  
 如果[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)字段包含此值，<xref:System.Threading.Tasks.Task.Status%2A>属性返回<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>。  
  
## <a name="see-also"></a>请参阅  
 [Task 类](../../extensibility/debugger/task-class-internal-members.md)
