---
title: IDebugEngine2：：附加 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93890885dbbdfd3cc26984590955681487977200
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731217"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
将调试引擎 （DE） 附加到程序或程序。 当 DE 在进程中运行到 SDM 时，会话调试管理器 （SDM） 调用。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>参数
`pProgram`\
[在]表示要附加到的程序的[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象的数组。 这些是端口程序。

`rgpProgramNodes`\
[在]表示程序节点的[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象的数组，每个程序一个。 此数组中的程序节点表示与 中的`pProgram`程序相同。 为程序节点提供，以便 DE 可以标识要附加到的程序。

`celtPrograms`\
[在]`pProgram`和`rgpProgramNodes`数组中的程序和/或程序节点数。

`pCallback`\
[在]用于将调试事件发送到 SDM 的[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。

`dwReason`\
[在][ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)枚举中指定附加这些程序的原因的值。 有关详细信息，请参见“备注”部分。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 附加到程序有三个原因，如下所示：

- `ATTACH_REASON_LAUNCH`指示 DE 附加到程序，因为用户启动了包含它的进程。

- `ATTACH_REASON_USER`指示用户已显式请求 DE 附加到程序（或包含程序的进程）。

- `ATTACH_REASON_AUTO`指示 DE 附加到特定程序，因为它已在调试特定进程中的其他程序。 这也称为自动附加。

  调用此方法时，DE 需要按顺序发送这些事件：

1. [IDebugEngineCreateEvent2（](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)如果尚未为调试引擎的特定实例发送）

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   此外，如果附加的原因是`ATTACH_REASON_LAUNCH`，DE 需要发送[IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)事件。

   一旦 DE 获取与正在调试的程序对应的[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象，就可以查询它的任何专用接口。

   在调用`pProgram`或`rgpProgramNodes`中给出的数组中的程序节点的方法之前，应在表示程序节点的`IDebugProgram2`接口上启用 模拟（如果需要）。 但是，通常不需要此步骤。 有关详细信息，请参阅[安全问题](../../../extensibility/debugger/security-issues.md)。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
