---
title: IDebugProcess2::CanDetach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CanDetach
helpviewer_keywords:
- IDebugProcess2::CanDetach
ms.assetid: 2830f7c3-69fb-474a-97b8-5b869e38d546
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 83cb927d86604096eac89da1d0efdf7e64e209be
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353227"
---
# <a name="idebugprocess2candetach"></a>IDebugProcess2::CanDetach
确定会话调试管理器 (SDM) 可以与进程分离。

## <a name="syntax"></a>语法

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK.`返回`S_FALSE`如果调试器无法从进程中分离。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)