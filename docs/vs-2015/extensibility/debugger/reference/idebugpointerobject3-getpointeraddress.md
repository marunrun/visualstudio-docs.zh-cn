---
title: IDebugPointerObject3：： GetPointerAddress |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetPointerAddress
- IDebugPointerObject3::GetPointerAddress
ms.assetid: 4cc5af04-9e70-420d-8230-ef3108df6d51
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d8b770bea631d772280b227b3298a45acee66e51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202958"
---
# <a name="idebugpointerobject3getpointeraddress"></a>IDebugPointerObject3::GetPointerAddress
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索指针的地址。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetPointerAddress (  
   UINT64* puAddress  
);  
```  
  
```csharp  
int GetPointerAddress (  
   out ulong puAddress  
);  
```  
  
#### <a name="parameters"></a>参数  
 `puAddress`  
 弄返回指针的地址。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)
