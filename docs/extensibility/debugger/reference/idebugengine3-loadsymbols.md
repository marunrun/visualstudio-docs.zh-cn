---
title: IDebugEngine3::LoadSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72c4fce5a7e8dd53093e21db2771d2176462e67c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352524"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
此调试引擎正在调试的所有模块的 （如有必要） 加载符号。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbols();
```

```csharp
int LoadSymbols();
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则将返回错误代码。

## <a name="remarks"></a>备注
 这会加载调试符号的引用的此调试引擎的所有模块。 仅当它们尚未加载，还加载符号。 通过调用设置的路径上搜索符号[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)。

## <a name="see-also"></a>请参阅
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)