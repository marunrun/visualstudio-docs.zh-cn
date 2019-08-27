---
title: IDebugEngineProgram2::Stop |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb74cb2940a91bbc64fa4a06f28d07a828357fc6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431480"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

停止此程序中正在运行的所有线程。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Stop(   
   void   
);  
```  
  
```csharp  
int Stop();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 此程序在调试多程序环境中时，调用此方法。 收到一些其他程序中的停止事件后，此程序上调用此方法。 此方法的实现应为异步的;也就是说，并非所有的线程数应需要此方法返回之前停止。 此方法的实现可能很简单，与调用[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)上此程序的方法。  
  
 没有调试事件是发送给此方法的响应。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
