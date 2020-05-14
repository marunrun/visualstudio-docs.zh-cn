---
title: IDebug程序节点附加2：：上附加 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dfb8a39af3c030dadddcb148a79a96b57f20e183
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721872"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
附加到关联的程序或延迟附加过程到[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。

## <a name="syntax"></a>语法

```cpp
HRESULT OnAttach(
   [in] REFGUID guidProgramId
);
```

```csharp
int OnAttach(
   ref Guid guidProgramId
};
```

## <a name="parameters"></a>参数
`guidProgramId`\
[在]`GUID`分配给关联的程序。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果`S_FALSE`不应调用[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 在调用[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法之前，在附加过程中调用此方法。 该方法`OnAttach`可以执行附加进程本身（在这种情况下，此方法`S_FALSE`返回）或将附加过程延迟到`IDebugEngine2::Attach`方法（`OnAttach`该方法返回）。 `S_OK` 在任一事件中，`OnAttach`该方法都可以将正在`GUID`调试的程序设置为给定`GUID`的 。

## <a name="see-also"></a>请参阅
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
