---
title: IEnumDebugFrameInfo2：： Skip |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2::Skip
helpviewer_keywords:
- IEnumDebugFrameInfo2::Skip
ms.assetid: 68cd3948-022a-41ad-bd9f-9ab776cf6248
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3714a4eac50e8f8175879181dc025536d15af7b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161034"
---
# <a name="ienumdebugframeinfo2skip"></a>IEnumDebugFrameInfo2::Skip
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

跳过指定数目的元素。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Skip(  
   ULONG celt  
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
 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
