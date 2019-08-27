---
title: IDebugErrorBreakpoint2::GetPendingBreakpoint |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpoint2::GetPendingBreakpoint
helpviewer_keywords:
- IDebugErrorBreakpoint2::GetPendingBreakpoint
ms.assetid: 59d0defc-99fd-445c-bdac-8224d5dea3f9
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aafdc16702620bfdbbba1f6323ec22281a875974
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188903"
---
# <a name="idebugerrorbreakpoint2getpendingbreakpoint"></a>IDebugErrorBreakpoint2::GetPendingBreakpoint
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取导致了错误的挂起断点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetPendingBreakpoint (   
   IDebugPendingBreakpoint2** ppPendingBreakpoint  
);  
```  
  
```csharp  
int GetPendingBreakpoint (   
   out IDebugPendingBreakpoint2 ppPendingBreakpoint  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppPendingBreakpoint`  
 [out]返回[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)表示无法绑定挂起断点的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
