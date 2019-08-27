---
title: IDebugSymbolProviderDirect::GetAppIDFromAddress | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect::GetAppIDFromAddress
- GetAppIDFromAddress
ms.assetid: d76a0f36-79c4-4c58-9db3-880b00d11610
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aa46f758e3f5b9379232b26da22c5ba234413d72
ms.sourcegitcommit: 0cd282a7584b9bfd4df7882f8fdf3ad8a270e219
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "62421314"
---
# <a name="idebugsymbolproviderdirectgetappidfromaddress"></a>IDebugSymbolProviderDirect::GetAppIDFromAddress
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索给定的调试地址的应用程序域标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetAppIDFromAddress(  
   IDebugAddress* pAddress,  
   DWORD*         pAppID  
);  
```  
  
```csharp  
int GetAppIDFromAddress(  
   IDebugAddress pAddress,  
   out uint      pAppID  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pAddress`  
 [in]调试由表示的地址[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口。  
  
 `pAppID`  
 [out]应用程序域的标识符。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
