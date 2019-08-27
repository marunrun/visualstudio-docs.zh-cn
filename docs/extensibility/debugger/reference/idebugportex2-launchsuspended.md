---
title: IDebugPortEx2::LaunchSuspended | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::LaunchSuspended
helpviewer_keywords:
- IDebugPortEx2::LaunchSuspended
ms.assetid: 34b2cf99-2e52-4757-8969-1d12ac517ec0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94810761e546b0cae9eca32fc76bc0bfd396c7e7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311116"
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
[in]若要启动的可执行文件的名称。 这可以是完整路径或相对于工作目录中指定`pszDir`参数。

`pszArgs`\
[in]要传递给可执行文件的参数。 如果没有任何自变量可能为 null 值。

`pszDir`\
[in]使用的可执行文件的工作目录的名称。 如果没有工作目录是必需的可能为 null 值。

`bstrEnv`\
[in]以 null 结尾的字符串后, 跟其他的 NULL 结束符的环境块。

`hStdInput`\
[in]其他输入流的句柄。 如果不需要重定向，则可能为 0。

`hStdOutput`\
[in]备用输出流的句柄。 如果不需要重定向，则可能为 0。

`hStdError`\
[in]备用错误输出流的句柄。 如果不需要重定向，则可能为 0。

`ppPortProcess`\
[out]返回[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)对象，表示启动的进程。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法应启动的过程，以便它处于挂起状态和未运行任何代码。 [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)调用方法来继续执行过程。

 此外可以从调试引擎启动程序。 有关详细信息，请参阅[启动程序](../../../extensibility/debugger/launching-a-program.md)。

## <a name="see-also"></a>请参阅
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)
- [启动程序](../../../extensibility/debugger/launching-a-program.md)