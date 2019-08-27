---
title: IDebugProcess2::EnumThreads | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 664f4264fd12106fef0650a31a888470e09a3154
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353169"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
检索在进程中运行的所有线程的列表。

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
[out]返回[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)对象，其中包含一系列过程中的所有程序中的所有线程。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法枚举每个程序中正在运行的线程，然后将它们合并到线程的进程视图。 单个线程可能会运行多个程序;此方法一次枚举该线程。

 此方法会显示该进程的线程没有重复项的列表。 否则，若要枚举在特定的程序中运行的线程，请使用[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)