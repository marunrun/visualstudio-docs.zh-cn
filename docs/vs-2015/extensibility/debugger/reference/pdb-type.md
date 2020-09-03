---
title: PDB_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PDB_TYPE
helpviewer_keywords:
- PDB_TYPE structure
ms.assetid: 1c1bb772-77d6-4870-90b2-fd9247d0004e
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad4b6a06a2a145daa85d780f4d23dfac9bebf7a0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205103"
---
# <a name="pdb_type"></a>PDB_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构指定有关从 PDB 符号获取的字段类型的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _tagTYPE_PDB {  
   ULONG32 ulAppDomainID;  
   GUID    guidModule;  
   DWORD   symid;  
} PDB_TYPE;  
```  
  
```csharp  
public struct PDB_TYPE {  
   public uint ulAppDomainID;  
   public Guid guidModule;  
   public uint symid;  
};  
```  
  
#### <a name="parameters"></a>参数  
 ulAppDomainID  
 符号所源自的应用程序的 ID。 用于唯一标识应用程序的实例。  
  
 guidModule  
 包含此字段的模块的 GUID。  
  
 symid  
 对应于此字段的符号的 ID。  
  
## <a name="remarks"></a>备注  
 当结构的[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) `dwKind` 字段 `TYPE_INFO` 设置为 `TYPE_KIND_PDB` 从[dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举) 中的值 (时，此结构显示为 TYPE_INFO 结构中联合的一部分。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)   
 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
