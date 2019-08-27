---
title: IDebugProgram2::Detach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Detach
helpviewer_keywords:
- IDebugProgram2::Detach
ms.assetid: 5e8d88b0-a8d4-4746-88c0-ad332ee73f33
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3259a2b9d0f9c617aaeebaebfae0713da5d3f9f5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326875"
---
# <a name="idebugprogram2detach"></a>IDebugProgram2::Detach
从该程序的调试引擎中分离。

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
 分离的程序继续运行，但它不再是调试会话的一部分。 没有更多程序调试事件发送后分离调试引擎。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)