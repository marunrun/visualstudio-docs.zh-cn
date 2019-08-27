---
title: BP_RESOLUTION_LOCATION | Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153294"
---
# <a name="bpresolutionlocation"></a>BP_RESOLUTION_LOCATION
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
 中的值[BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)枚举，用于指定如何解释`bpResLocation`union 或`unionmemberX`成员。  
  
 `bpResLocation.bpresCode`  
 [C++仅]包含[BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)结构，如果`bpType`  =  `BPT_CODE`。  
  
 `bpResLocation.bpresData`  
 [C++仅]包含[BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)结构，如果`bpType`  =  `BPT_DATA`。  
  
 `bpResLocation.unused`  
 [C++仅]一个占位符。  
  
 `unionmember1`  
 [C#仅]请参阅关于如何解释的备注。  
  
 `unionmember2`  
 [C#仅]请参阅关于如何解释的备注。  
  
 `unionmember3`  
 [C#仅]请参阅关于如何解释的备注。  
  
 `unionmember4`  
 [C#仅]请参阅关于如何解释的备注。  
  
## <a name="remarks"></a>备注  
 此结构是的成员[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)并[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)结构。  
  
 [C#仅]`unionmemberX`成员根据下表解释。 查看左侧列下方`bpType`值然后跨以确定每个`unionmemberX`成员表示和封送`unionmemberX`相应地。 请参阅一种方法来解释此结构在 C# 中的示例。  
  
|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|  
|----------------------|--------------------|--------------------|--------------------|--------------------|  
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|  
|`BPT_DATA`|`string` （数据表达式）|`string` （函数名称）|`string` （映像名称）|`enum_BP_RES_DATA_FLAGS`|  
  
## <a name="example"></a>示例  
 此示例显示了如何解释`BP_RESOLUTION_LOCATION`C# 中的结构。  
  
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
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)   
 [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)   
 [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
