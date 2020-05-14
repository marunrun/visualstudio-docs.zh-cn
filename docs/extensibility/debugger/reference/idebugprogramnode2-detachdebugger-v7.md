---
title: IDebugProgramNode2：:Detach调试器_V7 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 925f1b07662ece35d21f9b647681bc898428c4c7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722110"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 废弃。 请勿使用。

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
> 自 Visual Studio 2005 起，此方法不再使用，应始终返回`E_NOTIMPL`。

当调试器意外退出时，将调用此方法。 调用此方法时，DE 应像用户从程序分离时一样恢复该程序。 不应再发送调试事件。 程序应处于一种状态，可以从调试器的另一个实例附加该程序。

## <a name="see-also"></a>请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
