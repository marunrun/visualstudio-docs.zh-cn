---
title: 获取端口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7bf4948e7cb2590136774eab76fbafec91dbfa40
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738633"
---
# <a name="get-a-port"></a>获取端口
端口表示与运行进程的计算机的连接。 该计算机可以是本地计算机或远程计算机（可能运行非基于 Windows 的操作系统;有关详细信息，请参阅[端口](../../extensibility/debugger/ports.md)）。

端口由[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口表示。 它用于获取有关在端口连接到的计算机上运行的进程的信息。

调试引擎需要访问端口，以便向端口注册程序节点并满足进程信息请求。 例如，如果调试引擎实现[IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md)接口，[则 GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)方法的实现可能会要求端口返回必要的进程信息。

Visual Studio 向调试引擎提供必要的端口，并从端口供应商处获取此端口。 如果程序附加到（从调试器内部或由于引发异常而触发"实时 [JIT] 对话框"），则为用户提供要使用的传输选择（端口供应商的另一个名称）。 否则，如果用户从调试器中启动程序，则项目系统指定要使用的端口供应商。 在这两个事件中，Visual Studio 会实例化端口供应商（由[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口表示），并通过使用[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)接口调用[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)来请求新的端口。 然后，此端口以这种或另一种形式传递到调试引擎。

## <a name="example"></a>示例
此代码片段演示如何使用提供给[Launch暂停](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)的端口在[ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)中注册程序节点。 为了清楚起见，省略了与这一概念没有直接关系参数的参数。

> [!NOTE]
> 本示例使用端口启动和恢复该过程，并假定[IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)接口在端口上实现。 这绝不是执行这些任务的唯一方法，而且除了将程序的[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)交给它之外，端口可能甚至不涉及该端口。

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
                hr = spPortEx->ResumeProcess(pDebugProcess);
            }
        }
    }
    return(hr);
}
```

## <a name="see-also"></a>请参阅
- [注册程序](../../extensibility/debugger/registering-the-program.md)
- [启用对程序进行调试](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
- [港口供应商](../../extensibility/debugger/port-suppliers.md)
- [港口](../../extensibility/debugger/ports.md)
