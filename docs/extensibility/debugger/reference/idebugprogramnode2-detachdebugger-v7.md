---
title: IDebugProgramNode2::DetachDebugger_V7 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 241db5db55897932120b3253ff5185cb852ea77b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351206"
---
# <a name="idebugprogramnode2detachdebuggerv7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 不推荐使用。 不要使用。

## <a name="syntax"></a>语法

```cpp
HRESULT DetachDebugger_V7 (
   void 
);
```

```csharp
int DetachDebugger_V7 ();
```

## <a name="return-value"></a>返回值

实现应始终返回`E_NOTIMPL`。

## <a name="remarks"></a>备注

> [!WARNING]
> Visual Studio 2005 中，在撰写此方法不再使用，应始终返回`E_NOTIMPL`。

调试器会意外退出时，调用此方法。 调用此方法时，DE 应恢复该程序，就好像用户从其分离。 应发送没有更多的调试事件。 程序应该可附加成员在调试器的另一个实例的状态。

## <a name="see-also"></a>请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)