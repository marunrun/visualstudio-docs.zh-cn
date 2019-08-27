---
title: 获取端口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f980c9d14bc2d0c9728f87374828cf690737429c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436407"
---
# <a name="getting-a-port"></a>获取端口
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

端口表示进程正在其运行的计算机的连接。 该计算机可以是本地计算机或远程计算机 (这可能可能运行非基于 Windows 的操作系统，请参阅[端口](../../extensibility/debugger/ports.md)有关详细信息)。  
  
 表示一个端口[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口。 它用于获取的端口连接到计算机上运行的进程的信息。  
  
 调试引擎需要访问一个端口，以便注册程序节点的端口并满足请求过程的信息。 例如，如果调试引擎实现[IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md)接口的实现[GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)方法无法寻求必需流程的端口要返回的信息。  
  
 Visual Studio 提供必要的端口到调试引擎中，并从端口供应商处获取此端口。 如果程序附加到 （或从该调试器内因异常而引发，随即将会触发在实时 [JIT] 对话框），为用户提供选择的传输 （另一个端口提供程序名称） 来使用。 否则，如果用户启动该调试器内的从该程序，项目系统指定端口提供程序使用。 在既情况下，Visual Studio 实例化端口提供程序，由[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口，并通过调用要求提供一个新的端口[端口](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)与[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)接口。 此端口然后被传递给一个窗体中的调试引擎或另一个。  
  
## <a name="example"></a>示例  
 此代码片段演示了如何使用提供给的端口[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)注册中的程序节点[ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)。 为清楚起见，省略了此概念与不是直接相关的参数。  
  
> [!NOTE]
> 此示例中使用端口来启动和恢复过程，并假定[IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)接口实现的端口上。 这不是唯一的方法来执行这些任务，并且还有可能，端口可能不甚至会涉及到以外的程序的[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)提供给它。  
  
```cpp#  
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
 [正在注册程序](../../extensibility/debugger/registering-the-program.md)   
 [启用要进行调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)   
 [端口提供程序](../../extensibility/debugger/port-suppliers.md)   
 [端口](../../extensibility/debugger/ports.md)
