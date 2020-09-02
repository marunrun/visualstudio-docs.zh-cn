---
title: IDebugThread2：： CanSetNextStatement |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::CanSetNextStatement
helpviewer_keywords:
- IDebugThread2::CanSetNextStatement
ms.assetid: 7014af80-ff4f-4790-a34b-0528918d1fa3
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c3e98603a39d820b5565836bd2620f8a27def76f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153075"
---
# <a name="idebugthread2cansetnextstatement"></a>IDebugThread2::CanSetNextStatement
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

确定当前指令指针是否可以设置为给定的堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT CanSetNextStatement (   
   IDebugStackFrame2*  pStackFrame,  
   IDebugCodeContext2* pCodeContext  
);  
```  
  
```csharp  
int CanSetNextStatement (   
   IDebugStackFrame2  pStackFrame,  
   IDebugCodeContext2 pCodeContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pStackFrame`  
 保留以供将来使用;设置为 null 值。 如果这是空值，请使用当前堆栈帧。  
  
 `pCodeContext`  
 中描述要执行的代码位置及其上下文的 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果此方法返回 `S_OK` ，则调用 [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md) 方法来实际设置下一个语句。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
