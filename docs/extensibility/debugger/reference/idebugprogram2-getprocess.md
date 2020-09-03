---
title: IDebugProgram2：： GetProcess |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aca1842e92e7e1c164a6468e6c1e94a352ef67c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722791"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
获取此程序在其中运行的进程。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProcess(
   IDebugProcess2** ppProcess
);
```

```csharp
int GetProcess(
   out IDebugProcess2 ppProcess
);
```

## <a name="parameters"></a>参数
`ppProcess`\
弄返回表示进程的 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 除非调试引擎 (DE) 实现 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md) 接口，否则，此方法的 de 实现应始终返回， `E_NOTIMPL` 因为 de 无法确定它在哪个进程中运行，因此无法满足此方法的实现。

 实现 `IDebugEngineLaunch2` 接口意味着 de 必须知道如何创建进程，因此， [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的 DE 实现可以知道它正在运行的进程。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
