---
title: IDebugProgram2::EnumModules |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumModules
helpviewer_keywords:
- IDebugProgram2::EnumModules
ms.assetid: 876ac9da-3b7c-4156-b79a-8f340e9fcea6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c5e133045c83b62892850ede552d1f9cfd886506
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202740"
---
# <a name="idebugprogram2enummodules"></a>IDebugProgram2::EnumModules
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索此程序已加载且正在执行的模块的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumModules(   
   IEnumDebugModules2** ppEnum  
);  
```  
  
```csharp  
int EnumModules(   
   out IEnumDebugModules2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppEnum`  
 [out]返回[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)对象，其中包含的模块的列表。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 模块是一个 DLL 或程序集，它通常以列出**模块**调试窗口。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
