---
title: IDebugProperty2::GetSize |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetSize
helpviewer_keywords:
- IDebugProperty2::GetSize
ms.assetid: 0deb8ec5-d6fb-4622-bb14-0c46b9459cc6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e6c9118a9ce5a6dddb284d41b3c0b23ca8275f06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193465"
---
# <a name="idebugproperty2getsize"></a>IDebugProperty2::GetSize
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取的大小，以字节为单位的属性值。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetSize (   
   DWORD* pdwSize  
);  
```  
  
```csharp  
int GetSize (   
   out uint pdwSize  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdwSize`  
 [out]返回的大小，以字节为单位的属性值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`S_GETSIZE_NO_SIZE`如果属性没有大小。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
