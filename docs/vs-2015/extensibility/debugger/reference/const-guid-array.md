---
title: CONST_GUID_ARRAY |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CONST_GUID_ARRAY
helpviewer_keywords:
- CONST_GUID_ARRAY structure
ms.assetid: bd55e7d8-372c-4c3e-9eed-28f6b415a5db
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 43715ca8fa8174b2b8b9509a93e98cf15ad4611c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198865"
---
# <a name="constguidarray"></a>CONST_GUID_ARRAY
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

一个包含一系列结构`GUID`s。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct tagCONST_GUID_ARRAY {  
   DWORD       dwCount;  
   CONST GUID* Members;  
} CONST_GUID_ARRAY;  
```  
  
```csharp  
public struct CONST_GUID_ARRAY {  
   public uint   dwCount;  
   public Guid[] Members;  
}  
```  
  
## <a name="members"></a>成员  
 dwCount  
 数`GUID`中的 s`Members`数组。  
  
 成员  
 数组`GUID`s。  
  
## <a name="remarks"></a>备注  
 此结构传递给[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)方法，并返回从[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)并[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)方法。  
  
 此结构的实例的所有者负责释放分配的任何内存。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)   
 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)   
 [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
