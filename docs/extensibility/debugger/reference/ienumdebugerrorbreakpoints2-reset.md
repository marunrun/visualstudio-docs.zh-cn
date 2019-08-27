---
title: IEnumDebugErrorBreakpoints2::Reset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugErrorBreakpoints2::Reset
helpviewer_keywords:
- IEnumDebugErrorBreakpoints2::Reset
ms.assetid: d5b04bba-a8b9-4141-94fb-250c77f0534c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8122ec81fd69a0c38a4d1ad0df024d611ddcc49a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336441"
---
# <a name="ienumdebugerrorbreakpoints2reset"></a>IEnumDebugErrorBreakpoints2::Reset
将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 调用此方法下, 一步调用后[下一步](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)方法返回的第一个元素的枚举。

## <a name="see-also"></a>请参阅
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)