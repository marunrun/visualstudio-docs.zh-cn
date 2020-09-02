---
title: IEnumDebugAddresses：： Skip |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Skip
helpviewer_keywords:
- IEnumDebugAddresses::Skip method
ms.assetid: ed9a8e71-30ef-414b-9da5-c9a2a251b84e
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a150ab025221ddd22870082d9b8d08d044594856
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62572750"
---
# <a name="ienumdebugaddressesskip"></a>IEnumDebugAddresses::Skip
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法跳过指定数目的元素。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Skip(  
   [in] ULONG celt  
);  
```  
  
```csharp  
int Skip(  
   uint celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 中要跳过的元素数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果 `celt` 大于剩余元素的数目，则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果 `celt` 指定的值大于剩余元素的数目，则枚举将设置为 end，并 `S_FALSE` 返回。  
  
## <a name="see-also"></a>另请参阅  
 [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
