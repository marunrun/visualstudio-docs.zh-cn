---
title: IDebugPointerObject：： SetBytes |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPointerObject::SetBytes
helpviewer_keywords:
- IDebugPointerObject::SetBytes method
ms.assetid: 8c578b38-38d7-46f3-bb2e-8a730fccd334
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9d467b037f4e2affea53a142304507f876630999
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202961"
---
# <a name="idebugpointerobjectsetbytes"></a>IDebugPointerObject::SetBytes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

设置从一系列连续字节指向的值。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT SetBytes(   
   DWORD  dwStart,  
   DWORD  dwCount,  
   BYTE*  pBytes,  
   DWORD* pdwBytes  
);  
```  
  
```csharp  
int SetBytes(  
   uint     dwStart,   
   uint     dwCount,   
   byte[]   pBytes,   
   out uint pdwBytes  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwStart`  
 中从指向的对象的开始处的偏移量（以字节为单位）。  
  
 `dwCount`  
 中要设置的字节数。  
  
 `pBytes`  
 中表示新值的字节数组。 此值存储在对象中（从给定的偏移量开始）。  
  
 `pdwBytes`  
 弄返回实际设置的字节数。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果此 [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) 表示的指针指向基元类型或基元 (类型的简单数组，则使用此方法，这是一个可以由) 的简单字节序列表示的数组。 此 `IDebugPointerObject` 对象不能为 null 引用 (它必须指向内存) 中的地址。  
  
## <a name="see-also"></a>另请参阅  
 [GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)   
 [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
