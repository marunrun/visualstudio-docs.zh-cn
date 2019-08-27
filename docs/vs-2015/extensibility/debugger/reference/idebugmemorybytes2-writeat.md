---
title: IDebugMemoryBytes2::WriteAt | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2479ac3948f81769ba2e73c746fd1811652aa239
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180571"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

写入指定的内存，在指定地址开始的字节数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT WriteAt(   
   IDebugMemoryContext2* pStartContext,  
   DWORD                 dwCount,  
   BYTE*                 rgbMemory  
);  
```  
  
```csharp  
int WriteAt(  
   IDebugMemoryContext2 pStartContext,  
   uint                 dwCount,  
   byte[]               rgbMemory  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pStartContext`  
 [in][IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象，它指定位置开始写入字节数。  
  
 `dwCount`  
 [in]要写入的字节数。  
  
 `rgbMemory`  
 [in]要写入的字节。 此数组被假定为至少`dwCount`字节的大小。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果不是所有字节都可以编写，或返回错误代码 (通常`E_FAIL`)。  
  
## <a name="remarks"></a>备注  
 如果起始地址不是由此内存窗口内[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)对象时，发生任何写操作和错误代码的`E_FAIL`返回 — 即使量要写入到内存空间重叠。  
  
## <a name="see-also"></a>请参阅  
 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
