---
title: IDebugPort2::GetPortName |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortName
helpviewer_keywords:
- IDebugPort2::GetPortName
ms.assetid: 4478b3d5-aa30-4105-8d05-e3bae2f8917a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 25952355f77acb30587b7aab9820dfc1bed36507
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202895"
---
# <a name="idebugport2getportname"></a>IDebugPort2::GetPortName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取端口名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetPortName(   
   BSTR* pbstrName  
);  
```  
  
```csharp  
int GetPortName(   
   out string pbstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrName`  
 [out]返回的端口的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
