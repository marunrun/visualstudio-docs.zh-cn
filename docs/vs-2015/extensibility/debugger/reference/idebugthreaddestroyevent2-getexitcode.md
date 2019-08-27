---
title: IDebugThreadDestroyEvent2::GetExitCode | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThreadDestroyEvent2::GetExitCode
helpviewer_keywords:
- IDebugThreadDestroyEvent2::GetExitCode
ms.assetid: 8bf47a17-f811-4d9b-bcea-7488908830ff
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 93829c194e228309535f89f3ce39187e66e03ba6
ms.sourcegitcommit: da4079f5b6ec884baf3108cbd0519d20cb64c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62555655"
---
# <a name="idebugthreaddestroyevent2getexitcode"></a>IDebugThreadDestroyEvent2::GetExitCode
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取线程的退出代码。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetExitCode (   
   DWORD* pdwExit  
);  
```  
  
```csharp  
int GetExitCode (   
   out uint pdwExit  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdwExit`  
 [out]返回线程的退出代码。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)
