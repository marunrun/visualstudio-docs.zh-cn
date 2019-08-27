---
title: PROGRAM_NODE_ARRAY | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROGRAM_NODE_ARRAY
helpviewer_keywords:
- PROGRAM_NODE_ARRAY structure
ms.assetid: 8eeea600-eda5-4b7c-868a-0b86d177b0a5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ffbefd03bccc215dd68c30bae3cebb28c85654d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204997"
---
# <a name="programnodearray"></a>PROGRAM_NODE_ARRAY
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

包含描述程序感兴趣的对象的数组。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct tagPROGRAM_NODE_ARRAY {  
   DWORD                dwCount;  
   IDebugProgramNode2** Members;  
} PROGRAM_NODE_ARRAY;  
```  
  
```csharp  
public struct tagPROGRAM_NODE_ARRAY {  
   public uint                 dwCount;  
   public IDebugProgramNode2[] Members;  
}  
```  
  
## <a name="members"></a>成员  
 dwCount  
 中的对象数`Members`数组。  
  
 成员  
 一个数组[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)描述所请求的程序的对象。  
  
## <a name="remarks"></a>备注  
 此结构是的一部分[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)结构，这反过来调用填写[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
