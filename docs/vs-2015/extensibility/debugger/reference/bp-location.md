---
title: BP_LOCATION |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2a3e5f690a679118c7bb02c110d6e5d066a2bd0d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153399"
---
# <a name="bp_location"></a>BP_LOCATION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定用于描述断点位置的结构类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _BP_LOCATION {  
   BP_LOCATION_TYPE bpLocationType;  
   union {  
      BP_LOCATION_CODE_FILE_LINE   bplocCodeFileLine;  
      BP_LOCATION_CODE_FUNC_OFFSET bplocCodeFuncOffset;  
      BP_LOCATION_CODE_CONTEXT     bplocCodeContext;  
      BP_LOCATION_CODE_STRING      bplocCodeString;  
      BP_LOCATION_CODE_ADDRESS     bplocCodeAddress;  
      BP_LOCATION_DATA_STRING      bplocDataString;  
      BP_LOCATION_RESOLUTION       bplocResolution;  
      DWORD                        unused;  
   } bpLocation;  
} BP_LOCATION;  
```  
  
```csharp  
public struct BP_LOCATION {  
   public uint   bpLocationType;  
   public IntPtr unionmember1;  
   public IntPtr unionmember2;  
   public IntPtr unionmember3;  
   public IntPtr unionmember4;  
};  
```  
  
## <a name="members"></a>成员  
 `bpLocationType`  
 用于解释联合或成员的 [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) 枚举中的一个值 `bpLocation` `unionmemberX` 。  
  
 `bpLocation`.`bplocCodeFileLine`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)结构 `bpLocationType`  =  `BPLT_CODE_FILE_LINE` 。  
  
 `bpLocation.bplocCodeFuncOffset`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)结构 `bpLocationType`  =  `BPLT_CODE_FUNC_OFFSET` 。  
  
 `bpLocation.bplocCodeContext`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)结构 `bpLocationType`  =  `BPLT_CODE_CONTEXT` 。  
  
 `bpLocation.bplocCodeString`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)结构 `bpLocationType`  =  `BPLT_CODE_STRING` 。  
  
 `bpLocation.bplocCodeAddress`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)结构 `bpLocationType`  =  `BPLT_CODE_ADDRESS` 。  
  
 `bpLocation.bplocDataString`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)结构 `bpLocationType`  =  `BPLT_DATA_STRING` 。  
  
 `bpLocation.bplocResolution`  
 [仅限 c + +]如果为，则包含[BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)结构 `bpLocationType`  =  `BPLT_RESOLUTION` 。  
  
 `unionmember1`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
 `unionmember2`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
 `unionmember3`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
 `unionmember4`  
 [仅限 c #]有关如何解释的说明，请参阅备注。  
  
## <a name="remarks"></a>备注  
 此结构是 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 和 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构的成员。  
  
 [仅限 c #] `unionmemberX` 按照下表解释成员。 在左列中查找 `bpLocationType` 值，然后查看其他列，以确定每个 `unionmemberX` 成员表示的内容并相应地对其进行封送处理 `unionmemberX` 。 有关使用 c # 解释此结构的部分的方法，请参阅示例。  
  
|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|  
|----------------------|--------------------|--------------------|--------------------|--------------------|  
|`BPLT_CODE_FILE_LINE`|`string` (上下文) |[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|  
|`BPLT_CODE_FUNC_OFFSET`|`string` (上下文) |[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|  
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|  
|`BPLT_CODE_STRING`|`string` (上下文) |`string` (条件表达式) |-|-|  
|`BPLT_CODE_ADDRESS`|`string` (上下文) |`string` (模块 URL) |`string` (函数名称) |`string` (地址) |  
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string` (上下文) |`string` (数据表达式) |`uint` (元素数) |  
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|  
  
## <a name="example"></a>示例  
 此示例演示如何 `BP_LOCATION` 用 c # 解释类型的结构 `BPLT_DATA_STRING` 。 此特定类型显示了如何将 `unionmemberX` 所有可能格式的四个成员解释 (对象、字符串和数字) 。  
  
```csharp  
using System;  
using System.Runtime.Interop.Services;  
using Microsoft.VisualStudio.Debugger.Interop;  
  
namespace MyPackage  
{  
    public class MyClass  
    {  
        public void Interpret(BP_LOCATION bp)  
        {  
            if (bp.bpLocationType == (uint)enum_BP_LOCATION_TYPE.BPLT_DATA_STRING)  
            {  
                 IDebugThread2 pThread = (IDebugThread2)Marshal.GetObjectForIUnknown(bp.unionmember1);  
                 string context = Marshal.PtrToStringBSTR(bp.unionmember2);  
                 string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);  
                 uint numElements = (uint)Marshal.ReadInt32(bp.unionmember4);  
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
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)   
 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)   
 [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)   
 [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)   
 [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)   
 [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)   
 [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)
