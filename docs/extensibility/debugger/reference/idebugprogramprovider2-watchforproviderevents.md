---
title: IDebugProgram提供程序2：：观看提供商事件 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::WatchForProviderEvents
helpviewer_keywords:
- IDebugProgramProvider2::WatchForProviderEvents
ms.assetid: 2eb93653-b5fb-45b6-b136-56008c5d25ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a48e082556cf96a35ed83afd5008d3240e600b1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721762"
---
# <a name="idebugprogramprovider2watchforproviderevents"></a>IDebugProgramProvider2::WatchForProviderEvents
允许通知进程端口事件。

## <a name="syntax"></a>语法

```cpp
HRESULT WatchForProviderEvents(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   CONST_GUID_ARRAY     EngineFilter,
   REFGUID              guidLaunchingEngine,
   IDebugPortNotify2*   pEventCallback
);
```

```csharp
int WatchForProviderEvents(
   enum_PROVIDER_FLAGS   Flags,
   IDebugDefaultPort2    pPort,
   AD_PROCESS_ID         ProcessId,
   CONST_GUID_ARRAY      EngineFilter,
   ref Guid              guidLaunchingEngine,
   IDebugPortNotify2     pEventCallback
);
```

## <a name="parameters"></a>参数
`Flags`\
[在][PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)枚举中的标志的组合。 以下标志是此调用的典型标志：

|标志|描述|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|呼叫者在远程计算机上运行。|
|`PFLAG_DEBUGGEE`|当前正在调试调用方（返回有关每个节点的编组的其他信息）。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|调用方已附加到调试器，但未启动。|
|`PFLAG_REASON_WATCH`|呼叫者希望监视事件。 如果未设置此标志。 然后删除回调事件，呼叫者不再接收通知。|

`pPort`\
[在]调用进程正在运行的端口。

`processId`\
[在]包含包含相关程序的进程 ID 的[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。

`EngineFilter`\
[在]与进程关联的调试引擎的 GUID 数组。

`guidLaunchingEngine`\
[在]启动此过程的调试引擎的 GUID（如果有）。

`pEventCallback`\
[在]接收事件通知的[IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 当调用方想要删除以前调用此方法时建立的事件处理程序时，调用方传递的参数与首次调用时相同，但会离开`PFLAG_REASON_WATCH`标志。

## <a name="example"></a>示例
 下面的示例演示如何为公开[IDebugProgram.Provider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)接口的**CDebugEngine**对象实现此方法。

```cpp
STDMETHODIMP CDebugEngine::WatchForProviderEvents(
    PROVIDER_FLAGS Flags,
    IDebugDefaultPort2 *pPort,
    AD_PROCESS_ID processId,
    CONST_GUID_ARRAY EngineFilter,
    REFGUID guidLaunchingEngine,
    IDebugPortNotify2 *pPortNotify)
{
    HRESULT hRes = E_FAIL;

    if (EVAL(pPort != NULL) && EVAL(pPortNotify != NULL))
    {
        // We will only watch/send events about the process if the debugger
        // is actually debugging the process, and only if this is an attach or a LoRIE launch
        if (IsFlagSet(Flags, PFLAG_DEBUGGEE) &&
            guidLaunchingEngine == GUID_NULL &&
            processId.ProcessIdType == AD_PROCESS_ID_SYSTEM)
        {
            // We don't support WatchForProviderEvents when in interop mode
            if (m_fInterop)
            {
                ASSERT(!"Shouldn't ever be called in interop mode");
                hRes = E_FAIL;
            }
            else
            {
                if (IsFlagSet(Flags, PFLAG_REASON_WATCH))
                {
                    // QI to get IDebugEventCallback2 which is required.
                    CComQIPtr<IDebugEventCallback2> pCallback(pPortNotify);

                    ASSERT(pCallback != NULL);
                    if ( pCallback != NULL )
                    {
                        // Register the callback
                        hRes = this->InitDebugSession(pCallback);

                        if ( S_OK == hRes )
                        {
                            // Get the IDebugProcess2 from the port and call AttachImpl
                            CComPtr<IDebugProcess2> spProcess;

                            hRes = pPort->GetProcess(processId, &spProcess);

                            if (HREVAL(S_OK, hRes))
                            {
                                hRes = AttachImpl(spProcess, NULL, NULL, processId.ProcessId.dwProcessId, ATTACH_REASON_USER, NULL);

                                if ( FAILED(hRes) && (!m_pPidList || 0 == m_pPidList->GetCount()) )
                                    this->Cleanup();
                            }
                        }
                        else
                            this->Cleanup();
                    }
                    else
                        hRes = E_FAIL;
                }
                else
                {
                    // Detach will be done by SDM calling on programs directly if there are managed programs.

                    // This handling is the case where no managed code ever ran.
                    if ( this->IsProcessBeingDebugged(processId.ProcessId.dwProcessId) )
                    {
                        ProgramList *pProgList = this->GetProgramListCopy();

                        if ( EVAL(pProgList) )
                        {
                            if ( pProgList->GetCount() == 0)
                            {
                                CComPtr<ICorDebugProcess> pCorProcess;

                                hRes = this->GetCorProcess(processId.ProcessId.dwProcessId, &pCorProcess);

                                if (HREVAL(S_OK, hRes) )
                                {
                                    hRes = pCorProcess->Stop(INFINITE);

                                    if ( HREVAL(S_OK, hRes) )
                                        hRes = pCorProcess->Detach();
                                }

                                // Tell the engine that it should unregister this process from com+
                                this->UnregisterProcess(processId.ProcessId.dwProcessId);

                                // If there are no more pids left then cleanup everything.
                                if ( 0 == m_pPidList->GetCount() )
                                    this->Cleanup();
                            }
                            // This is needed for cases where the SDM has not yet received program create
                            // by the time that we need to detach (example: the managed attach succeeds,
                            // but some other attach step fails).
                            else
                            {
                                PROGNODE *pProgNode = NULL;
                                while ( pProgNode = pProgList->Next(pProgNode) )
                                {
                                    CDebugProgram * pProgram = ((CDebugProgram *)pProgNode->data);
                                    hRes = pProgram->Detach();
                                }
                            }

                            delete pProgList;
                        }
                    }
                    else
                        hRes = S_OK;
                }
            }
        }
        else
        {
            hRes = S_FALSE;
        }
    }
    else
    {
        hRes = E_INVALIDARG;
    }

    return hRes;
}
```

## <a name="see-also"></a>请参阅
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
