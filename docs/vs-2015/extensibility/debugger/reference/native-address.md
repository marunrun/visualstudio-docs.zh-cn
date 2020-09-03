---
title: NATIVE_ADDRESS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- NATIVE_ADDRESS
helpviewer_keywords:
- NATIVE_ADDRESS structure
ms.assetid: 7a0cd085-bfc8-45cc-a3d4-4459070e207a
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 13c2bdd2e7fcaeeb15d6e208f1a7c1411cac4b0c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205160"
---
# <a name="native_address"></a>NATIVE_ADDRESS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构表示本机地址。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct _tagNATIVE_ADDRESS {  
   DWORD unknown;  
} NATIVE_ADDRESS;  
```  
  
```csharp  
public struct NATIVE_ADDRESS {  
   public uint unknown;  
}  
```  
  
## <a name="terms"></a>术语  
 未知  
 本机地址 (这种情况取决于运行时和操作系统) 。  
  
## <a name="remarks"></a>备注  
 当结构的[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) `dwKind` 字段 `DEBUG_ADDRESS_UNION` 设置为 `ADDRESS_KIND_NATIVE` 从[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举) 中的值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的一部分。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
