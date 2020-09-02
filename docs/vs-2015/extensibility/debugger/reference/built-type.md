---
title: BUILT_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6becf886d361e203dca313a7aa1dfdf166aa4614
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153174"
---
# <a name="built_type"></a>BUILT_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构指定了来自元数据的字段类型的相关信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _tagTYPE_BUILT {  
   ULONG32      ulAppDomainID;  
   GUID         guidModule;  
   IDebugField* pUnderlyingField;  
} BUILT_TYPE;  
```  
  
```csharp  
public struct BUILT_TYPE {  
   public uint        ulAppDomainID;  
   public Guid        guidModule;  
   public IDebugField pUnderlyingField;  
};  
```  
  
#### <a name="parameters"></a>参数  
 ulAppDomainID  
 符号所源自的应用程序的 ID。 用于唯一标识应用程序的实例。  
  
 guidModule  
 包含此字段的模块的 GUID。  
  
 pUnderlyingField  
 一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，该对象标识与此生成字段关联的基础字段。  
  
## <a name="remarks"></a>备注  
 当结构的[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) `dwKind` 字段 `TYPE_INFO` 设置为 `TYPE_KIND_BUILT` 从[dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举) 中的值 (时，此结构显示为 TYPE_INFO 结构中联合的一部分。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)   
 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
