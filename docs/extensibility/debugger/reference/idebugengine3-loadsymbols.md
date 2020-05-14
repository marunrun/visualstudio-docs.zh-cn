---
title: IDebugEngine3：：加载符号 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7963d39601a0d3a90ca2daa7632902d7aa506de8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730809"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
此调试引擎正在调试的所有模块的加载（根据需要）符号。

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
 如果成功，返回S_OK;否则返回错误代码。

## <a name="remarks"></a>备注
 这将加载此调试引擎引用的所有模块的调试符号。 仅当符号尚未加载时，才会加载这些符号。 符号在调用[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)设置的路径上搜索。

## <a name="see-also"></a>请参阅
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
