---
title: IDebugAlias2::GetAppDomainId |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 79f6a71376d410f6eb0b524a309f5f6dffcdf614
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197922"
---
# <a name="idebugalias2getappdomainid"></a>IDebugAlias2::GetAppDomainId
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索应用程序域标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetAppDomainId (  
   ULONG32* pappDomainId  
);  
```  
  
```csharp  
int GetAppDomainId (  
   out uint pappDomainId  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pappDomainId`  
 [out]返回应用程序域标识符。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 创建应用程序域标识符更改时重新启动应用程序和新的应用程序域。  
  
## <a name="see-also"></a>请参阅  
 [IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)
