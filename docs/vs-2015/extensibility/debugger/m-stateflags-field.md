---
title: m_stateFlags 字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_stateFlags field, Task class [.NET Framework debug engines]
ms.assetid: 82b20efc-08f2-4cd2-91f6-4e01e3da906b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 794ab8baac441fc14d41c2d30b9db4b0894e88e8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149087"
---
# <a name="mstateflags-field"></a>m_stateFlags 字段
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

存储的当前状态有关的信息<xref:System.Threading.Tasks.Task>对象。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.field assembly int32 modreq(System.Runtime.CompilerServices.IsVolatile) m_stateFlags  
```  
  
## <a name="remarks"></a>备注  
 通常使用<xref:System.Threading.Tasks.Task.Status%2A?displayProperty=fullName>属性来访问此值。  
  
 此成员可以是下列值中的任意组合：  
  
- [TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)  
  
- [TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)  
  
- [TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)  
  
- [TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)  
  
- [TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)  
  
## <a name="see-also"></a>请参阅  
 [Task 类](../../extensibility/debugger/task-class-internal-members.md)
