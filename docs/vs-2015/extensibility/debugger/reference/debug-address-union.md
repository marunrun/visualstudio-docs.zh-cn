---
title: DEBUG_ADDRESS_UNION |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS_UNION
helpviewer_keywords:
- DEBUG_ADDRESS_UNION union
ms.assetid: e3d11aab-de0d-4109-b5dc-11e07e64382d
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b500bcb49e9072c3d31ea5ac3f77bda606c23b78
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179174"
---
# <a name="debug_address_union"></a>DEBUG_ADDRESS_UNION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述不同类型的地址。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct _tagDEBUG_ADDRESS_UNION {  
   ADDRESS_KIND dwKind;  
   union {  
      NATIVE_ADDRESS                  addrNative;  
      UNMANAGED_ADDRESS_THIS_RELATIVE addrThisRel;  
      UNMANAGED_ADDRESS_PHYSICAL      addrUPhysical;  
      METADATA_ADDRESS_METHOD         addrMethod;  
      METADATA_ADDRESS_FIELD          addrField;  
      METADATA_ADDRESS_LOCAL          addrLocal;  
      METADATA_ADDRESS_PARAM          addrParam;  
      METADATA_ADDRESS_ARRAYELEM      addrArrayElem;  
      METADATA_ADDRESS_RETVAL         addrRetVal;  
      DWORD                           unused;  
   } addr;  
} DEBUG_ADDRESS_UNION;  
```  
  
```csharp  
public struct DEBUG_ADDRESS_UNION {  
   public ADDRESS_KIND dwKind;  
   public IntPtr       unionmember;  
}  
```  
  
## <a name="terms"></a>术语  
 dwKind  
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中的一个值，指定如何解释联合。  
  
 addrNative  
 [仅限 c + +]如果 = ADDRESS_KIND_NATIVE，则包含 [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) 结构 `dwKind` 。  
  
 addrThisRel  
 [仅限 c + +]如果 = ADDRESS_KIND_UNMANAGED_THIS_RELATIVE，则包含[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) 结构 `dwKind` 。  
  
 addUPhysical  
 [仅限 c + +]如果 = ADDRESS_KIND_UNMANAGED_PHYSICAL，则包含[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) 结构 `dwKind` 。  
  
 addrMethod  
 [仅限 c + +]如果 = ADDRESS_KIND_METHOD，则包含[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) 结构 `dwKind` 。  
  
 addrField  
 [仅限 c + +]如果 = ADDRESS_KIND_FIELD，则包含[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) 结构 `dwKind` 。  
  
 addrLocal  
 [仅限 c + +]如果 = ADDRESS_KIND_LOCAL，则包含[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) 结构 `dwKind` 。  
  
 addrParam  
 [仅限 c + +]如果 = ADDRESS_KIND_PARAM，则包含[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) 结构 `dwKind` 。  
  
 addrArrayElem  
 [仅限 c + +]如果 = ADDRESS_KIND_ARRAYELEM，则包含[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) 结构 `dwKind` 。  
  
 addrRetVal  
 [仅限 c + +]如果 = ADDRESS_KIND_RETVAL，则包含[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) 结构 `dwKind` 。  
  
 地址未使用  
 [仅限 c + +] 填充。  
  
 addr  
 [仅限 c + +]联合的名称。  
  
 unionmember  
 [仅限 c #]此值需要基于的适当的结构类型进行封送处理 `dwKind` 。 请参阅对联合之间的关联的备注 `dwKind` 。  
  
## <a name="remarks"></a>备注  
 此结构是 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 结构的一部分，它表示结构中 (的一种不同类型的地址， `DEBUG_ADDRESS` 通过调用 [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) 方法) 进行填充。  
  
 [仅限 c #]下表显示了如何解释 `unionmember` 每种类型的地址的成员。 该示例演示如何针对一种地址完成此操作。  
  
|`dwKind`|`unionmember` 解释为|  
|--------------|----------------------------------|  
|`ADDRESS_KIND_NATIVE`|[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)|  
|`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`|[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)|  
|`ADDRESS_KIND_UNMANAGED_PHYSICAL`|[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)|  
|`ADDRESS_KIND_METHOD`|[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)|  
|`ADDRESS_KIND_FIELD`|[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)|  
|`ADDRESS_KIND_LOCAL`|[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)|  
|`ADDRESS_KIND_PARAM`|[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)|  
|`ADDRESS_KIND_ARRAYELEM`|[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)|  
|`ADDRESS_KIND_RETVAL`|[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)|  
  
## <a name="example"></a>示例  
 此示例演示如何 `METADATA_ADDRESS_ARRAYELEM` `DEBUG_ADDRESS_UNION` 在 c # 中解释结构的一种类型的地址 () 。 其余元素可以通过完全相同的方式进行解释。  
  
```csharp  
using System;  
using System.Runtime.Interop.Services;  
using Microsoft.VisualStudio.Debugger.Interop;  
  
namespace MyPackage  
{  
    public class MyClass  
    {  
        public void Interpret(DEBUG_ADDRESS_UNION dau)  
        {  
            if (dau.dwKind == (uint)enum_ADDRESS_KIND.ADDRESS_KIND_METADATA_ARRAYELEM)  
            {  
                 METADATA_ADDRESS_ARRAYELEM arrayElem =  
                     (METADATA_ADDRESS_ARRAYELEM)Marshal.PtrToStructure(dau.unionmember,  
                                 typeof(METADATA_ADDRESS_ARRAYELEM));  
            }  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)   
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)   
 [获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
