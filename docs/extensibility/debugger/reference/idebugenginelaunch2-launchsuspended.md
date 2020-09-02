---
title: IDebugEngineLaunch2：： LaunchSuspended |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e802c17d0a93aabbe5c6c0a8573abc6a551944ae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730554"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
此方法通过调试引擎 (DE) 来启动进程。

## <a name="syntax"></a>语法

```cpp
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

## <a name="parameters"></a>参数
`pszMachine`\
中要在其中启动进程的计算机的名称。 使用 null 值来指定本地计算机。

`pPort`\
中表示程序将在其中运行的端口的 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 接口。

`pszExe`\
中要启动的可执行文件的名称。

`pszArgs`\
中要传递给可执行文件的参数。 如果没有参数，则可以为 null 值。

`pszDir`\
中可执行文件使用的工作目录的名称。 如果不需要任何工作目录，则可以为 null 值。

`bstrEnv`\
中以 NULL 结尾的字符串的环境块，后跟一个其他 NULL 终止符。

`pszOptions`\
中可执行文件的选项。

`dwLaunchFlags`\
中指定会话的 [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md) 。

`hStdInput`\
中替代输入流的句柄。 如果不需要重定向，则可以为0。

`hStdOutput`\
中备用输出流的句柄。 如果不需要重定向，则可以为0。

`hStdError`\
中备用错误输出流的句柄。 如果不需要重定向，则可以为0。

`pCallback`\
中接收调试器事件的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。

`ppDebugProcess`\
弄返回生成的 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 对象，该对象表示已启动的进程。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 通常， [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 使用 [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) 方法启动程序，然后将调试器附加到挂起的程序。 但是，在某些情况下，调试引擎可能需要启动程序 (例如，如果调试引擎是解释器的一部分，而正在调试的程序是) 解释的语言，在这种情况下， [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 使用 `IDebugEngineLaunch2::LaunchSuspended` 方法。

 在进程成功启动并处于挂起状态后，调用 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md) 方法以启动进程。

## <a name="see-also"></a>另请参阅
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
