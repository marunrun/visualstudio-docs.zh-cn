---
title: IDebugProgram2::EnumThreads |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumThreads
helpviewer_keywords:
- IDebugProgram2::EnumThreads
ms.assetid: 0f2a8c51-1315-4c96-8aa1-6a937dc2a769
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd3391973fd9f86c0473b811efe35dc02f5bf48f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353125"
---
# <a name="idebugprogram2enumthreads"></a>IDebugProgram2::EnumThreads
检索在程序中运行的线程的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumThreads( 
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int EnumThreads( 
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]返回[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)对象，其中包含主题的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)