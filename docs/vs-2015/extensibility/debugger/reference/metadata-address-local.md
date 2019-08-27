---
title: METADATA_ADDRESS_LOCAL | Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62547164"
---
# <a name="metadataaddresslocal"></a>METADATA_ADDRESS_LOCAL
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构表示范围 （通常是一个函数或方法） 内的本地变量的地址。  
  
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
 方法或函数的 ID 本地变量为的一部分。  
  
 [C++]`_mdToken`是`typedef`适用于 32 位`int`。  
  
 pLocal  
 标记此结构表示其地址。  
  
 dwIndex  
 可以是局部变量的方法或函数或一些其他值 （特定于语言的） 中的索引。  
  
## <a name="remarks"></a>备注  
 此结构是中的联合的一部分[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)结构时`dwKind`字段`DEBUG_ADDRESS_UNION`结构设置为`ADDRESS_KIND_LOCAL`(从值[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举）。  
  
 `Warning:` [C++仅] 如果`pLocal`不为 null，则必须调用`Release`上标记的指针 (`addr`是中的字段[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构):  
  
```  
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL &&  addr.addr.addrLocal.pLocal != NULL)  
{  
    addr.addr.addrLocal.pLocal->Release();  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)   
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)   
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
