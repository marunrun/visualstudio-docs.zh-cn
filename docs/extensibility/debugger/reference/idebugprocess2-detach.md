---
title: IDebugProcess2::Detach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Detach
helpviewer_keywords:
- IDebugProcess2::Detach
ms.assetid: ee2b9084-2db1-4e49-a1d9-387284b7c3f8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3948ecce15b9b2b2e8b3bf974ecc2277d9fa0360
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353202"
---
# <a name="idebugprocess2detach"></a>IDebugProcess2::Detach
通过分离所有进程中的程序分离调试程序与此进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Detach( 
   void 
);
```

```csharp
int Detach();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 所有程序和进程继续运行，但不再是调试会话的一部分。 分离操作后对该过程 （以及其程序） 的事件将发送完成，没有更多调试。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)