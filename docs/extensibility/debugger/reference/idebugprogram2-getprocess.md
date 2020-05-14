---
title: IDebugProgram2：：获取过程 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722791"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
获取此程序正在运行的进程。

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
[出]返回表示进程的[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)接口。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 除非调试引擎 （DE） 实现[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)接口，否则 DE 此方法的实现应始终返回`E_NOTIMPL`，因为 DE 无法确定它在哪个进程中运行，因此无法满足此方法的实现。

 实现`IDebugEngineLaunch2`接口意味着 DE 必须知道如何创建进程;因此，DE [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的实现能够知道它正在运行的进程。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
