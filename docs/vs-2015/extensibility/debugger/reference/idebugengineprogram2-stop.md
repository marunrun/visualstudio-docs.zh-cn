---
title: IDebugEngineProgram2：： Stop |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431480"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

停止在此程序中运行的所有线程。  
  
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
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 在多程序环境中调试此程序时，将调用此方法。 当收到来自某个其他程序的停止事件时，将对此程序调用此方法。 此方法的实现应为异步;也就是说，在此方法返回之前，并不是所有线程都需要停止。 此方法的实现可能与在此程序上调用 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) 方法一样简单。  
  
 不会为响应此方法而发送调试事件。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
