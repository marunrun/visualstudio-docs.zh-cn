---
title: SetNotificationForWaitCompletion 方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 874e31c331f16e760e030f337dda715473b77af8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423395"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion 方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置或清除 TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状态位。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly：** mscorlib (mscorlib.dll)   
  
## <a name="syntax"></a>语法  
  
```vb  
internal void SetNotificationForWaitCompletion(bool enabled)  
```  
  
#### <a name="parameters"></a>参数  
 `enabled`  
  
 `true` 设置位;取消 `false` 设置此位。  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>备注  
 调试器将此位设置为帮助跳出异步方法体。 如果 `enabled` 为 `true` ，则必须仅对尚未完成的任务调用此方法。 如果 `enabled` 为 `false` ，则可以对已完成的任务调用此方法。 在这两种情况下，它只应用于承诺样式任务。  
  
## <a name="requirements"></a>要求  
  
## <a name="see-also"></a>另请参阅  
 [Task 类](../../extensibility/debugger/task-class-internal-members.md)
