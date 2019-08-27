---
title: IDebugEngineLaunch2::LaunchSuspended |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08f59f9f099f4cec52760c8a8364feb8f5481ffa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195748"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法通过调试引擎 (DE) 启动进程。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT LaunchSuspended (   
   LPCOLESTR             pszMachine,  
   IDebugPort2*          pPort,  
   LPCOLESTR             pszExe,  
   LPCOLESTR             pszArgs,  
   LPCOLESTR             pszDir,  
   BSTR                  bstrEnv,  
   LPCOLESTR             pszOptions,  
   LAUNCH_FLAGS          dwLaunchFlags,  
   DWORD                 hStdInput,  
   DWORD                 hStdOutput,  
   DWORD                 hStdError,  
   IDebugEventCallback2* pCallback,  
   IDebugProcess2**      ppDebugProcess  
);  
```  
  
```csharp  
int LaunchSuspended(  
   string               pszServer,   
   IDebugPort2          pPort,   
   string               pszExe,   
   string               pszArgs,   
   string               pszDir,   
   string               bstrEnv,   
   string               pszOptions,   
   enum_LAUNCH_FLAGS    dwLaunchFlags,   
   uint                 hStdInput,   
   uint                 hStdOutput,   
   uint                 hStdError,  
   IDebugEventCallback2 pCallback,   
   out IDebugProcess2   ppProcess  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszMachine`  
 [in]在要启动的过程中的计算机的名称。 使用 null 值指定本地计算机。  
  
 `pPort`  
 [in][IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口表示该程序将运行中的端口。  
  
 `pszExe`  
 [in]若要启动的可执行文件的名称。  
  
 `pszArgs`  
 [in]要传递给可执行文件的参数。 如果没有任何自变量可能为 null 值。  
  
 `pszDir`  
 [in]使用的可执行文件的工作目录的名称。 如果没有工作目录是必需的可能为 null 值。  
  
 `bstrEnv`  
 [in]以 NULL 结尾的字符串后, 跟其他的 NULL 结束符的环境块。  
  
 `pszOptions`  
 [in]有关可执行文件的选项。  
  
 `dwLaunchFlags`  
 [in]指定[LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)会话。  
  
 `hStdInput`  
 [in]其他输入流的句柄。 如果不需要重定向，则可能为 0。  
  
 `hStdOutput`  
 [in]备用输出流的句柄。 如果不需要重定向，则可能为 0。  
  
 `hStdError`  
 [in]备用错误输出流的句柄。 如果不需要重定向，则可能为 0。  
  
 `pCallback`  
 [in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)接收调试器事件的对象。  
  
 `ppDebugProcess`  
 [out]返回合并[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)对象，表示启动的进程。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 通常情况下，[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]启动程序使用[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)方法，然后将调试器附加到挂起的程序。 但是，有些情况下调试引擎可能需要以这种情况下启动的程序 （例如，如果调试引擎是解释器的一部分，并且正在调试的程序是一种解释型的语言），[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]使用`IDebugEngineLaunch2::LaunchSuspended`方法.  
  
 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)调用方法来启动进程后过程已成功启动处于挂起状态。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)   
 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
