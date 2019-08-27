---
title: IDebugProcessEx2::AddImplicitProgramNodes |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: faca728144bde572d8a1d3424fbfcf908403d679
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202820"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法将添加指定每种调试引擎 (DE) 的程序节点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT AddImplicitProgramNodes(  
   REFGUID guidLaunchingEngine,  
   GUID*   rgguidSpecificEngines,  
   DWORD   celtSpecificEngines  
);  
```  
  
```csharp  
int AddImplicitProgramNodes(  
   ref Guid guidLaunchingEngine,  
   Guid[]   rgguidSpecificEngines,  
   uint     celtSpecificEngines  
);  
```  
  
#### <a name="parameters"></a>参数  
 `guidLaunchingEngine`  
 [in]`GUID`的 DE 是要用来启动程序 （并且假定添加其自身程序节点）。  
  
 `rgguidSpecificEngines`  
 [in]数组`GUID`的 DEs 将节点添加的程序。  
  
 `celtSpecificEngines`  
 [in]数`GUID`中的 s`rgguidSpecificEngines`数组。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 [程序节点](../../../extensibility/debugger/program-nodes.md)中列出的每个 DE 将添加`rgguidSpecificEngines`— 不包括启动引擎 (中给出`guidLaunchingEngine`)，这假定它启动程序时添加其自己的程序节点。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)   
 [程序节点](../../../extensibility/debugger/program-nodes.md)
