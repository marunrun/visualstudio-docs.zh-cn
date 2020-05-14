---
title: 注册程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b68fa67f784d155288482ad724b632ed5ba5fa41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713162"
---
# <a name="register-the-program"></a>注册程序
调试引擎获取了由[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口表示的端口后，使程序进行调试的下一步是将其注册到端口。 注册后，程序可通过以下方式之一进行调试：

- 附加过程，它允许调试器获得正在运行的应用程序的完整调试控制。

- 实时 （JIT） 调试，允许对独立于调试器运行的程序进行事后调试。 当运行时体系结构捕获故障时，在操作系统或运行时环境释放故障程序的内存和资源之前通知调试器。

## <a name="registering-procedure"></a>注册过程

### <a name="to-register-your-program"></a>注册您的程序

1. 调用端口实现的[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)方法。

     `IDebugPortNotify2::AddProgramNode`需要指向[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口的指针。

     通常，当操作系统或运行时环境加载程序时，它会创建程序节点。 如果要求调试引擎 （DE） 加载程序，DE 将创建并注册程序节点。

     下面的示例显示调试引擎启动程序并将其注册到端口。

    > [!NOTE]
    > 此代码示例不是启动和恢复进程的唯一方法;因此，此过程不是启动和恢复进程的唯一方法。此代码主要是将程序注册到端口的示例。

    ```cpp
    // This is an IDebugEngineLaunch2 method.
    HRESULT CDebugEngine::LaunchSuspended(/* omitted parameters */,
                                          IDebugPort2 *pPort,
                                          /* omitted parameters */,
                                          IDebugProcess2**ppDebugProcess)
    {
        // do stuff here to set up for a launch (such as handling the other parameters)
        ...

        // Now get the IPortNotify2 interface so we can register a program node
        // in CDebugEngine::ResumeProcess.
        CComPtr<IDebugDefaultPort2> spDefaultPort;
        HRESULT hr = pPort->QueryInterface(&spDefaultPort);
        if (SUCCEEDED(hr))
        {
            CComPtr<IDebugPortNotify2> spPortNotify;
            hr = spDefaultPort->GetPortNotify(&spPortNotify);
            if (SUCCEEDED(hr))
            {
                // Remember the port notify so we can use it in ResumeProcess.
                m_spPortNotify = spPortNotify;

                // Now launch the process in a suspended state and return the
                // IDebugProcess2 interface
                CComPtr<IDebugPortEx2> spPortEx;
                hr = pPort->QueryInterface(&spPortEx);
                if (SUCCEEDED(hr))
                {
                    // pass on the parameters we were given (omitted here)
                    hr = spPortEx->LaunchSuspended(/* omitted parameters */,ppDebugProcess)
                }
            }
        }
        return(hr);
    }

    HRESULT CDebugEngine::ResumeProcess(IDebugProcess2 *pDebugProcess)
    {
        // Make a program node for this process
        HRESULT hr;
        CComPtr<IDebugProgramNode2> spProgramNode;
        hr = this->GetProgramNodeForProcess(pProcess, &spProgramNode);
        if (SUCCEEDED(hr))
        {
            hr = m_spPortNotify->AddProgramNode(spProgramNode);
            if (SUCCEEDED(hr))
            {
                // resume execution of the process using the port given to us earlier.
               // (Querying for the IDebugPortEx2 interface is valid here since
               // that's how we got the IDebugPortNotify2 interface in the first place.)
                CComPtr<IDebugPortEx2> spPortEx;
                hr = m_spPortNotify->QueryInterface(&spPortEx);
                if (SUCCEEDED(hr))
                {
                    hr  = spPortEx->ResumeProcess(pDebugProcess);
                }
            }
        }
        return(hr);
    }

    ```

## <a name="see-also"></a>请参阅
- [获取端口](../../extensibility/debugger/getting-a-port.md)
- [启用对程序进行调试](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
