---
title: IDebugProgramNode2::Attach_V7 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
ms.assetid: b5ffc736-efc7-4ca8-964d-5536ff891b0e
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08028f2b03f3ea36cc72172ca8f9de31740b49f3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63417910"
---
# <a name="idebugprogramnode2attachv7"></a>IDebugProgramNode2::Attach_V7
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

不推荐使用。 不要使用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Attach_V7 (   
   IDebugProgram2*       pMDMProgram,  
   IDebugEventCallback2* pCallback,  
   DWORD                 dwReason  
);  
```  
  
```csharp  
int Attach_V7 (   
   IDebugProgram2       pMDMProgram,  
   IDebugEventCallback2 pCallback,  
   uint                 dwReason  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pMDMProgram`  
 [in][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口，表示要将附加到的程序。  
  
 `pCallback`  
 [in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)要用来将调试事件发送到 SDM 的接口。  
  
 `dwReason`  
 [in]中的值[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)枚举，用于指定附加的原因。  
  
## <a name="return-value"></a>返回值  
 实现应始终返回`E_NOTIMPL`。  
  
## <a name="remarks"></a>备注  
  
> [!WARNING]
> 起始日期[!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]，此方法不能再使用，否则应始终返回`E_NOTIMPL`。 请参阅[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)接口的另一种方法，如果程序节点需要指示不能将它附加到或如果程序节点只需设置程序`GUID`。 否则，实现[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。  
  
## <a name="prior-to-visual-studio-2005"></a>在 Visual Studio 2005 之前  
 此方法需要仅当正在调试的程序的地址空间中运行 DE 实现。 否则，此方法应返回`S_FALSE`。  
  
 调用此方法时，必须发送 DE [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)事件对象，如果它不已发送的此实例[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口，并将[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)并[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)事件对象。 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)事件对象然后发送，如果`dwReason`参数是`ATTACH_REASON_LAUNCH`。  
  
 必须调用 DE [GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)提供的对象[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象，并必须将存储该程序的 GUID实例数据中`IDebugProgram2`DE 由实现的对象。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)   
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)   
 [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)   
 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)   
 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
