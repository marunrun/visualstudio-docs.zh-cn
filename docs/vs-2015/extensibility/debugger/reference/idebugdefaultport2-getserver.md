---
title: IDebugDefaultPort2::GetServer |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2a74a9e846532b119c5b72495c39226effdc94f0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196269"
---
# <a name="idebugdefaultport2getserver"></a>IDebugDefaultPort2::GetServer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法获取此端口的服务器的接口。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetServer(  
   IDebugCoreServer3** ppServer  
);  
```  
  
```csharp  
int GetServer(  
   out IDebugCoreServer3 ppServer  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppServer`  
 [out]返回一个对象，实现[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)实现由 Visual Studio 和表示该端口位于的服务器。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)   
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
