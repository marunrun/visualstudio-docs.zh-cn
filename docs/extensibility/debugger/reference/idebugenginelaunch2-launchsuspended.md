---
title: IDebugEngine启动2：：启动暂停 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730554"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
此方法通过调试引擎 （DE） 启动进程。

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
[在]要在其中启动进程的机器的名称。 使用 null 值指定本地计算机。

`pPort`\
[在][IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口表示程序将在其中运行的端口。

`pszExe`\
[在]要启动的可执行文件的名称。

`pszArgs`\
[在]要传递给可执行文件的参数。 如果没有参数，则可能是 null 值。

`pszDir`\
[在]可执行文件使用的工作目录的名称。 如果不需要工作目录，则可能是空值。

`bstrEnv`\
[在]NULL 终止字符串的环境块，后跟一个额外的 NULL 终止符。

`pszOptions`\
[在]可执行文件的选项。

`dwLaunchFlags`\
[在]指定会话[的LAUNCH_FLAGS。](../../../extensibility/debugger/reference/launch-flags.md)

`hStdInput`\
[在]处理备用输入流。 如果不需要重定向，则可能是 0。

`hStdOutput`\
[在]处理备用输出流。 如果不需要重定向，则可能是 0。

`hStdError`\
[在]处理备用错误输出流。 如果不需要重定向，则可能是 0。

`pCallback`\
[在]接收调试器事件的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。

`ppDebugProcess`\
[出]返回表示启动过程的结果[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 通常，[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]使用[Launch暂停](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)方法启动程序，然后将调试器附加到挂起的程序。 但是，在某些情况下，调试引擎可能需要启动程序（例如，如果调试引擎是解释器的一部分，并且正在调试的程序是解释语言），在这种情况下[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]，使用 该方法。 `IDebugEngineLaunch2::LaunchSuspended`

 在进程以挂起状态成功启动后，将调用[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)方法以启动进程。

## <a name="see-also"></a>请参阅
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
