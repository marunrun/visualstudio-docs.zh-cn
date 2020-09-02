---
title: METADATA_ADDRESS_RETVAL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6f685bcfad5cf576215aa50aa26540ba207de2e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62546858"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构表示方法或函数的返回值。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct _tagMETADATA_ADDRESS_RETVAL {  
   _mdToken tokMethod;  
   DWORD    dwCorType;  
   DWORD    dwSigSize;  
   BYTE     rgSig[10];  
} METADATA_ADDRESS_RETVAL;  
```  
  
```csharp  
public struct METADATA_ADDRESS_RETVAL {  
   public int    tokMethod;  
   public uint   dwCorType;  
   public uint   dwSigSize;  
   public byte[] rgSig;  
}  
```  
  
## <a name="terms"></a>术语  
 tokMethod  
 此返回值的方法的 ID。  
  
 dwCorType  
 返回值的基类型。 这是 `CorElementType` SDK corhdr.h 文件中定义的枚举的值 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 。  
  
 dwSigSize  
 返回值签名的大小 (存储在 `rgSig`) 中。  
  
 rgSig  
 构成返回值签名的字节数组。  
  
## <a name="remarks"></a>备注  
 当结构的[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) `dwKind` 字段 `DEBUG_ADDRESS_UNION` 设置为 `ADDRESS_KIND_RETVAL` 从[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举) 中的值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的一部分。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)   
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
