---
title: IDebugProgram2：： Terminate |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4673259e4a8ca0d4354037efbc35b63bedfcbc96
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146342"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

终止程序。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Terminate(   
   void   
);  
```  
  
```csharp  
int Terminate();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果可能，程序将终止并从进程中卸载;否则，调试引擎 (DE) 会执行任何必要的清理。  
  
 此方法或 [终止](../../../extensibility/debugger/reference/idebugprocess2-terminate.md) 方法由 IDE 调用，通常是为了响应用户停止所有调试。 此方法的实现在理想情况下应终止进程内的程序。 如果无法做到这一点，则取消操作应该会阻止程序在此过程中运行更多 (，并执行任何必要的清理) 。 如果该 `IDebugProcess2::Terminate` 方法是由 IDE 调用的，则在调用方法后的某个时间，整个进程将被终止 `IDebugProgram2::Terminate` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 Terminate
