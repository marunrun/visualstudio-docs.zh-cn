---
title: IDebugEngine2::Attach |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a82d26fbfd6fe08f4976aaa7643bcaa95008032f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196048"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将调试引擎 (DE) 附加到一个程序或程序。 会话调试管理器 (SDM) 由进程到 SDM DE 时调用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Attach(   
   IDebugProgram2**      pProgram,  
   IDebugProgramNode2**  rgpProgramNodes,  
   DWORD                 celtPrograms,  
   IDebugEventCallback2* pCallback,  
   ATTACH_REASON         dwReason  
);  
```  
  
```csharp  
int Attach(   
   IDebugProgram2[]     pProgram,  
   IDebugProgramNode2[] rgpProgramNodes,  
   uint                 celtPrograms,  
   IDebugEventCallback2 pCallback,  
   Enum_ATTACH_REASON   dwReason  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pProgram`  
 [in]一个数组[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)代表程序附加到的对象。 这些是端口程序。  
  
 `rgpProgramNodes`  
 [in]一个数组[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象，表示程序节点，一个用于每个程序。 此数组中的程序节点表示作为中的相同程序`pProgram`。 提供程序节点，以便 DE 可以标识要附加到的程序。  
  
 `celtPrograms`  
 [in]程序和/或程序中的节点数`pProgram`和`rgpProgramNodes`数组。  
  
 `pCallback`  
 [in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象要用来将调试事件发送到 SDM。  
  
 `dwReason`  
 [in]中的值[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)枚举，用于指定用于附加这些程序的原因。 有关详细信息，请参阅“备注”部分。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 有三个原因的附加到的程序，按如下所示：  
  
- `ATTACH_REASON_LAUNCH` 指示，DE 附加到程序中，因为用户启动应用包含它的进程。  
  
- `ATTACH_REASON_USER` 指示用户已显式请求 DE 将附加到一个程序 （或包含程序的进程）。  
  
- `ATTACH_REASON_AUTO` 指示 DE 附加到特定程序，因为它已调试其他程序中的特定进程。 这也称为自动附加。  
  
  调用此方法时，DE 需要将这些事件发送序列中：  
  
1. [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) （如果它不已发送的调试引擎对特定实例）  
  
2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)  
  
3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)  
  
   此外，如果附加的原因是`ATTACH_REASON_LAUNCH`，需要发送 DE [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)事件。  
  
   一次 DE 获取[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象对应于正在调试的程序可以为任何私有接口对其进行查询。  
  
   调用程序节点的方法由给定数组中之前`pProgram`或`rgpProgramNodes`，模拟的更多信息，如有必要，应在上启用`IDebugProgram2`表示程序节点的接口。 通常情况下，但是，此步骤不必要。 有关详细信息，请参阅[安全问题](../../../extensibility/debugger/security-issues.md)。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)   
 [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)   
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)   
 [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)   
 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
