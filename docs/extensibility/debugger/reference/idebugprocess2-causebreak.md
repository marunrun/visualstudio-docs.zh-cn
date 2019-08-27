---
title: IDebugProcess2::CauseBreak | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CauseBreak
helpviewer_keywords:
- IDebugProcess2::CauseBreak
ms.assetid: efda8865-2319-4d53-90bf-6d9d74cd5195
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fbe4f3cac40306467e6efc7d87ca860a6d6f3f0e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353230"
---
# <a name="idebugprocess2causebreak"></a>IDebugProcess2::CauseBreak
下一步，它是程序在此过程中运行代码的请求中断并发送[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)事件对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CauseBreak( 
   void
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)