---
title: IDebugProgramNodeAttach2：： OnAttach |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721872"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
附加到关联程序或将附加进程推迟到 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。

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
[in] `GUID` 分配给关联的程序。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果不应调用[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 在附加过程中调用 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法之前调用此方法。 `OnAttach`方法可以执行附加进程本身 (在这种情况下，此方法返回 `S_FALSE`) 或将附加进程推迟到方法 `IDebugEngine2::Attach` `OnAttach` 返回)  (方法 `S_OK` 。 在这两种情况下，该 `OnAttach` 方法都可以将 `GUID` 正在调试的程序的设置为给定的 `GUID` 。

## <a name="see-also"></a>另请参阅
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
