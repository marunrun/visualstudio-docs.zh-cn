---
title: IDebugProcess2：：枚举 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 52383649fc45eae6bbac6831f9bb233b9c0a2fde
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724071"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
检索进程中运行的所有线程的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumThreads(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int EnumThreads(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[出]返回包含进程中所有程序中所有线程的列表的[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法枚举每个程序中运行的线程，然后将它们合并到线程的进程视图中。 单个线程可能在多个程序中运行;但是，单个线程可能会在多个程序中运行。此方法仅枚举该线程一次。

 此方法显示进程线程的列表，而不重复。 否则，要枚举在特定程序中运行的线程，请使用[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
