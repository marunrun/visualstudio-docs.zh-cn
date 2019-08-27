---
title: IDebugProgram2::GetProcess |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 366b35a90eb44496dc1b50cd85dfa0fef5656ddb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148654"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取此程序在运行时的进程。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetProcess(  
   IDebugProcess2** ppProcess  
);  
```  
  
```csharp  
int GetProcess(  
   out IDebugProcess2 ppProcess  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppProcess`  
 [out]返回[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)表示进程的接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 除非调试引擎 (DE) 实现[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)接口，此方法的 DE 的实现应始终返回`E_NOTIMPL`因为部署不能确定哪个进程正在运行中，因此不能满足此方法的实现。  
  
 实现`IDebugEngineLaunch2`界面意味着 DE 必须知道如何创建进程; 因此，德国的实施[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口是能够了解在运行的进程。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
