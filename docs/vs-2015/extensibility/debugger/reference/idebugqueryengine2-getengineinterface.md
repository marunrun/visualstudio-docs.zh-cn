---
title: IDebugQueryEngine2：： GetEngineInterface |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2::GetEngineInterface
helpviewer_keywords:
- IDebugQueryEngine2::GetEngineInterface
ms.assetid: ed84aa98-7ec7-48f3-97ae-821090bc3664
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 12bdcf9de9731095a224f394cab13f3833f126de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158115"
---
# <a name="idebugqueryengine2getengineinterface"></a>IDebugQueryEngine2::GetEngineInterface
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取 (DE) 接口的自定义调试引擎。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetEngineInterface(   
   IUnknown** ppUnk  
);  
```  
  
```csharp  
int GetEngineInterface(   
   out object ppUnk  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppUnk`  
 弄返回一个 `IUnknown` 对象，该对象表示 (DE) 调试引擎，并可查询与 DE (相关联的任何其他有效接口，例如 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 或 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)) 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 应谨慎使用生成的接口，因为通过此方法检索到的接口会绕过会话调试管理器的处理，并可能导致 SDM 进入错误的状态或在调试时生成错误。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)   
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
