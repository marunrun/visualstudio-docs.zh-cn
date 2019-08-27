---
title: IDebugModule3::LoadSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::LoadSymbols
helpviewer_keywords:
- IDebugModule3::LoadSymbols
ms.assetid: 7548c8c1-cbc6-48aa-a845-19058d4a85bb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e1b23e7b1ae837087db198795ffeda6a5827f045
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323847"
---
# <a name="idebugmodule3loadsymbols"></a>IDebugModule3::LoadSymbols
加载当前模块的符号。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbols(
   void
);
```

```csharp
int LoadSymbols();
```

## <a name="return-value"></a>返回值
 如果此方法成功，它将返回`S_OK`。 如果失败，则返回错误代码。

## <a name="remarks"></a>备注
 此方法从当前的搜索路径加载符号 (这可以通过调用更改[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)方法)。

 此方法是通过首选[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)