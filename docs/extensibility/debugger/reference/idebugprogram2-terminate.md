---
title: IDebugProgram2::Terminate | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 16a6d60173090642bda7d8fd940ecf0699e1d7ec
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331499"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
终止程序。

## <a name="syntax"></a>语法

```cpp
HRESULT Terminate( 
   void 
);
```

```csharp
int Terminate();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 如果可能，将终止并从进程; 中卸载程序否则，调试引擎 (DE) 将执行任何必要的清理。

 此方法或[Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md) IDE 中，通常以响应停止所有调试用户调用方法。 此方法的实现应，理想情况下，终止过程中的程序。 如果无法做到这一点，DE 应运行此过程中的其他任何阻止程序 （和执行任何必要的清理）。 如果`IDebugProcess2::Terminate`由 IDE 调用方法，将一段时间后终止整个过程`IDebugProgram2::Terminate`调用方法。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)