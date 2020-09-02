---
title: BP_LOCATION_CODE_FILE_LINE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FILE_LINE
helpviewer_keywords:
- BP_LOCATION_CODE_FILE_LINE structure
ms.assetid: 3ff32032-d412-44d3-91bf-870cc354a09e
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 29fbb041a90118e7725ed3140e6583c7ac756a07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153472"
---
# <a name="bp_location_code_file_line"></a>BP_LOCATION_CODE_FILE_LINE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

包含代码源文件中特定行的断点位置的数据。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _BP_LOCATION_CODE_FILE_LINE {   
   BSTR                     bstrContext;  
   IDebugDocumentPosition2* pDocPos;  
} BP_LOCATION_CODE_FILE_LINE;  
```  
  
## <a name="members"></a>成员  
 `bstrContext`  
 断点的上下文，通常是在调用堆栈上显示的方法或函数名称。  
  
 `pDocPos`  
 表示断点的文档位置的 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) 对象。  
  
## <a name="remarks"></a>备注  
 此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
