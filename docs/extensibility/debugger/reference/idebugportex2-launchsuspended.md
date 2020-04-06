---
title: IDebugPortEx2：：启动暂停 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::LaunchSuspended
helpviewer_keywords:
- IDebugPortEx2::LaunchSuspended
ms.assetid: 34b2cf99-2e52-4757-8969-1d12ac517ec0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28ff6065bbe83852b5acc3ffe253a0bdabcc67ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725097"
---
# <a name="idebugportex2launchsuspended"></a>IDebugPortEx2::LaunchSuspended
启动可执行文件。

## <a name="syntax"></a>语法

```cpp
HRESULT LaunchSuspended( 
   LPCOLESTR        pszExe,
   LPCOLESTR        pszArgs,
   LPCOLESTR        pszDir,
   BSTR             bstrEnv,
   DWORD            hStdInput,
   DWORD            hStdOutput,
   DWORD            hStdError,
   IDebugProcess2** ppPortProcess
);
```

```csharp
int LaunchSuspended( 
   string             pszExe,
   string             pszArgs,
   string             pszDir,
   string             bstrEnv,
   uint               hStdInput,
   uint               hStdOutput,
   uint               hStdError,
   out IDebugProcess2 ppPortProcess
);
```

## <a name="parameters"></a>参数
`pszExe`\
[在]要启动的可执行文件的名称。 这可以是完整路径，也可以与`pszDir`参数中指定的工作目录相关。

`pszArgs`\
[在]要传递给可执行文件的参数。 如果没有参数，则可能是 null 值。

`pszDir`\
[在]可执行文件使用的工作目录的名称。 如果不需要工作目录，则可能是空值。

`bstrEnv`\
[在]null 终止字符串的环境块，后跟一个额外的 NULL 终止符。

`hStdInput`\
[在]处理备用输入流。 如果不需要重定向，则可能是 0。

`hStdOutput`\
[在]处理备用输出流。 如果不需要重定向，则可能是 0。

`hStdError`\
[在]处理备用错误输出流。 如果不需要重定向，则可能是 0。

`ppPortProcess`\
[出]返回表示启动进程的[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法应启动进程，以便它挂起并且不运行任何代码。 调用[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)方法以恢复该过程。

 也可以从调试引擎启动程序。 有关详细信息，请参阅[启动程序](../../../extensibility/debugger/launching-a-program.md)。

## <a name="see-also"></a>请参阅
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)
- [启动程序](../../../extensibility/debugger/launching-a-program.md)
