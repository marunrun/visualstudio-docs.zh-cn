---
title: 正在注册程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31d03f12a31953cbc0e20d06820dd49b5f9827e6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441969"
---
# <a name="registering-the-program"></a>注册程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试引擎已获取某个端口后，由[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口，启用要进行调试的程序的下一步是将其注册到该端口。 注册后，该程序是可用于调试通过以下方法之一：  
  
- 连接的过程，这使调试器能够获取正在运行的应用程序的完整调试控件。  
  
- 在实时 (JIT) 调试时，这允许事实后调试的一个独立于调试器运行程序。 当运行时体系结构会捕获错误时，调试器通知操作系统之前或运行时环境释放的内存和出错的程序的资源。  
  
## <a name="registering-procedure"></a>注册过程  
  
#### <a name="to-register-your-program"></a>若要注册你的程序  
  
1. 调用[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)方法实现的端口。  
  
     `IDebugPortNotify2::AddProgramNode` 要求一个指向[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口。  
  
     通常情况下，当操作系统或运行时环境加载程序，它创建的程序节点。 如果调试引擎 (DE) 需要加载程序 DE 创建，并注册程序节点。  
  
     下面的示例演示调试引擎启动该程序并注册一个端口。  
  
    > [!NOTE]
    > 这不是唯一的方法来启动和恢复过程;这是主要与端口注册一个程序的示例。  
  
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
 [获取端口](../../extensibility/debugger/getting-a-port.md)   
 [启用要进行调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
