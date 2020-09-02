---
title: BP_RESOLUTION_LOCATION |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_LOCATION
helpviewer_keywords:
- BP_RESOLUTION_LOCATION structure
ms.assetid: 21dc5246-69c1-43e3-855c-9cd4e596c0e6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ea6539f2ed790dda5cc4c9de126aa226f4b2686
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153294"
---
# <a name="bp_resolution_location"></a>BP_RESOLUTION_LOCATION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定断点解析位置的结构。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
struct _BP_RESOLUTION_LOCATION {  
   BP_TYPE bpType;  
   union {  
      BP_RESOLUTION_CODE bpresCode;  
      BP_RESOLUTION_DATA bpresData;  
      int                unused;  
   } bpResLocation;  
} BP_RESOLUTION_LOCATION;  
```  
  
```csharp  
public struct BP_RESOLUTION_LOCATION {  
   public uint bpType;  
   public IntPtr unionmember1;  
   public IntPtr unionmember2;  
   public IntPtr unionmember3;  
   public uint   unionmember4;  
};  
```  
  
## <a name="members"></a>成员  
 `bpType`  
 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)枚举中的一个值，该值指定如何解释 `bpResLocation` 联合或 `unionmemberX` 成员。  
  
 `bpResLocation.bpresCode`  
 [仅限 c + +]如果为，则包含[BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)结构 `bpType`  =  `BPT_CODE` 。  
  
 `bpResLocation.bpresData`  
 [仅限 c + +]如果为，则包含[BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)结构 `bpType`  =  `BPT_DATA` 。  
  
 `bpResLocation.unused`  
 [仅限 c + +]占位符。  
  
 `unionmember1`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
 `unionmember2`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
 `unionmember3`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
 `unionmember4`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
## <a name="remarks"></a>备注  
 此结构是 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 和 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 结构的成员。  
  
 [仅限 c #] `unionmemberX` 按照下表解释成员。 在左列中查找 `bpType` 值，然后查看每个 `unionmemberX` 成员表示的内容并相应地对其进行封送处理 `unionmemberX` 。 有关使用 c # 解释此结构的方法，请参阅示例。  
  
|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|  
|----------------------|--------------------|--------------------|--------------------|--------------------|  
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|  
|`BPT_DATA`|`string` (数据表达式) |`string` (函数名称) |`string` (映像名称) |`enum_BP_RES_DATA_FLAGS`|  
  
## <a name="example"></a>示例  
 此示例演示如何解释 `BP_RESOLUTION_LOCATION` c # 中的结构。  
  
```csharp  
using System;  
using System.Runtime.Interop.Services;  
using Microsoft.VisualStudio.Debugger.Interop;  
  
namespace MyPackage  
{  
    public class MyClass  
    {  
        public void Interpret(BP_RESOLUTION_LOCATION bprl)  
        {  
            if (bprl.bpType == (uint)enum_BP_TYPE.BPT_CODE)  
            {  
                 IDebugCodeContext2 pContext = (IDebugCodeContext2)Marshal.GetObjectForIUnknown(bp.unionmember1);  
            }  
            else if (bprl.bpType == (uint)enum_BP_TYPE.BPT_DATA)  
            {  
                 string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);  
                 string functionName = Marshal.PtrToStringBSTR(bp.unionmember2);  
                 string imageName = Marshal.PtrToStringBSTR(bp.unionmember3);  
                 enum_BP_RES_DATA_FLAGS numElements = (enum_BP_RES_DATA_FLAGS)bp.unionmember4;  
            }  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)   
 [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)   
 [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
