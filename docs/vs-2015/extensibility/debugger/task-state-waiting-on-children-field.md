---
title: TASK_STATE_WAITING_ON_CHILDREN 字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_WAITING_ON_CHILDREN field, Task class [.NET Framework debug engines]
ms.assetid: 6f26b098-84ad-4f6e-ba27-6136581ba630
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e2dfb7ca683b7a05151539feda92a2575197b189
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68176717"
---
# <a name="taskstatewaitingonchildren-field"></a>TASK_STATE_WAITING_ON_CHILDREN 字段
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

任务已完成执行其委托，隐式等待附加的子任务完成。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.field static assembly literal int32 TASK_STATE_WAITING_ON_CHILDREN = int32(0x01000000)  
```  
  
## <a name="remarks"></a>备注  
 如果[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)字段包含此值，<xref:System.Threading.Tasks.Task.Status%2A>属性返回<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>。  
  
## <a name="see-also"></a>请参阅  
 [Task 类](../../extensibility/debugger/task-class-internal-members.md)
