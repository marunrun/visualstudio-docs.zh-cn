---
title: DEBUG_REFERENCE_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUG_REFERENCE_INFO
helpviewer_keywords:
- DEBUG_REFERENCE_INFO structure
ms.assetid: 24b83d00-d756-42a1-8083-730f998761dc
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 675373ae1728bbca2cc7a89fdaa8014e6286d8b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159325"
---
# <a name="debugreferenceinfo"></a>DEBUG_REFERENCE_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述的引用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct tagDEBUG_REFERENCE_INFO {   
   DEBUGREF_INFO_FLAGS dwFields;  
   BSTR                bstrName;  
   BSTR                bstrType;  
   BSTR                bstrValue;  
   DBG_ATTRIB_FLAGS    dwAttrib;  
   REFERENCE_TYPE.     dwRefType;  
   IDebugReference2*   m_pReference;  
} DEBUG_REFERENCE_INFO;  
```  
  
```csharp  
public struct DEBUG_REFERENCE_INFO {   
   public uint             dwFields;  
   public string           bstrName;  
   public string           bstrType;  
   public string           bstrValue;  
   public ulong            dwAttrib;  
   public uint.            dwRefType;  
   public IDebugReference2 m_pReference;  
};  
```  
  
## <a name="members"></a>成员  
 dwFields  
 中的标志的组合[DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)枚举，用于指定哪些字段填写。  
  
 bstrName  
 用户指定的名称[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象。  
  
 bstrType  
 形式的格式化字符串的引用类型。  
  
 bstrValue  
 形式的格式化字符串的引用值  
  
 dwAttrib  
 中的标志的组合[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)指定调试属性特性的标志的枚举。  
  
 dwRefType  
 中的值[REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)枚举，用于指定引用类型是强还是弱。  
  
 m_pReference  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象，它指定的参考信息。  
  
## <a name="remarks"></a>备注  
 此结构传递给调用[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)要填充的方法。 从列表的一部分，也会返回此结构[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)接口，反过来，通过调用将返回该值[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)   
 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)   
 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)   
 [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)   
 [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)   
 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
