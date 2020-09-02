---
title: METADATA_ADDRESS_LOCAL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_LOCAL
helpviewer_keywords:
- METADATA_ADDRESS_LOCAL structure
ms.assetid: 635f6bc5-c486-4e0e-83db-36f15e543843
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5928f6092adc62dc8f0eb075f20367c056fc50c1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547164"
---
# <a name="metadata_address_local"></a>METADATA_ADDRESS_LOCAL
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构表示作用域内的本地变量的地址， (通常是) 的函数或方法。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct _tagMETADATA_ADDRESS_LOCAL {  
   _mdToken  tokMethod;  
   IUnknown* pLocal;  
   DWORD     dwIndex;  
} METADATA_ADDRESS_LOCAL;  
```  
  
```csharp  
public struct METADATA_ADDRESS_LOCAL {  
   public int    tokMethod;  
   public object pLocal;  
   public uint   dwIndex;  
}  
```  
  
## <a name="terms"></a>术语  
 tokMethod  
 本地变量所属的方法或函数的 ID。  
  
 [C + +] `_mdToken` 是 `typedef` 32 位的 `int` 。  
  
 pLocal  
 此结构所表示的地址的标记。  
  
 dwIndex  
 可以是方法或函数中此局部变量的索引，也可以是特定于语言的)  (其他值。  
  
## <a name="remarks"></a>备注  
 当结构的[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) `dwKind` 字段 `DEBUG_ADDRESS_UNION` 设置为 `ADDRESS_KIND_LOCAL` 从[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举) 中的值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的一部分。  
  
 `Warning:` [仅限 c + +] 如果不为 `pLocal` null，则必须 `Release` 在令牌指针上调用， (`addr` 是 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 结构中的字段) ：  
  
```  
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL &&  addr.addr.addrLocal.pLocal != NULL)  
{  
    addr.addr.addrLocal.pLocal->Release();  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)   
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)   
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
