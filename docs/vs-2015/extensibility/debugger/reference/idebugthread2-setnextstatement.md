---
title: IDebugThread2::SetNextStatement |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::SetNextStatement
helpviewer_keywords:
- IDebugThread2::SetNextStatement
ms.assetid: 9e2834dd-4ecf-45af-8e6c-f9318ebdac06
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 755044ec1d713075c1c1fd3165254ba192943288
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152966"
---
# <a name="idebugthread2setnextstatement"></a>IDebugThread2::SetNextStatement
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将当前指令指针设置为给定的代码上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT SetNextStatement (   
   IDebugStackFrame2*  pStackFrame,  
   IDebugCodeContext2* pCodeContext  
);  
```  
  
```csharp  
int SetNextStatement (   
   IDebugStackFrame2  pStackFrame,  
   IDebugCodeContext2 pCodeContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pStackFrame`  
 保留供将来使用;设置为 null 值。  
  
 `pCodeContext`  
 [in][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，描述要执行的代码位置和其上下文。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了其他可能的值。  
  
|值|描述|  
|-----------|-----------------|  
|E_CANNOT_SET_NEXT_STATEMENT_ON_NONLEAF_FRAME|下一条语句不能为帧堆栈上更深入的堆栈帧中。|  
|E_CANNOT_SETIP_TO_DIFFERENT_FUNCTION|下一条语句不是堆栈中任何帧与相关联。|  
|E_CANNOT_SET_NEXT_STATEMENT_ON_EXCEPTION|某些调试引擎不能设置在出现异常之后的下一个语句。|  
  
## <a name="remarks"></a>备注  
 指令指针指示的下一步的指令或语句，以执行。 若要重试源代码的行，或若要强制执行以继续在另一个函数，例如，使用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
