---
title: IDebugCoreServer2：： GetPort |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetPort
helpviewer_keywords:
- IDebugCoreServer2::GetPort
ms.assetid: 3f5ea4a8-6085-4600-980a-9e48f8b5be56
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e00f055d8e6a0fe1bea82061431410eb1e3b236f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192931"
---
# <a name="idebugcoreserver2getport"></a>IDebugCoreServer2::GetPort
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索特定端口。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetPort(   
   REFGUID       guidPort,  
   IDebugPort2** ppPort  
);  
```  
  
```csharp  
int GetPort(   
   ref Guid        guidPort,  
   out IDebugPort2 ppPort  
);  
```  
  
#### <a name="parameters"></a>参数  
 `guidPort`  
 中要检索的端口的 GUID。  
  
 `ppPort`  
 弄返回表示所需端口的 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_PORTSUPPLIER_NO_PORT`如果没有具有给定标识符的端口，则返回。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
