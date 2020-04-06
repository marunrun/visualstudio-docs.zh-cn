---
title: IDebugEngine3：：设置符号路径 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetSymbolPath
helpviewer_keywords:
- IDebugEngine3::SetSymbolPath
ms.assetid: 47b48f84-8a96-401f-84df-0baa8a96d26e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1fbe5128900fa10147c747cbcba4129e96d4c4ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730664"
---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
设置搜索调试符号的路径或路径。

## <a name="syntax"></a>语法

```cpp
HRESULT SetSymbolPath (
   LPOLESTR            szSymbolSearchPath,
   LPOLESTR            szSymbolCachePath,
   LOAD_SYMBOLS_FLAGS  Flags
);
```

```csharp
int SetSymbolPath(
   string                    szSymbolSearchPath,
   string                    szSymbolCachePath,
   enum_LOAD_SYMBOLS_FLAGS   Flags
);
```

## <a name="parameters"></a>参数

`szSymbolSearchPath`\
[在]包含符号搜索路径或路径的字符串。 有关详细信息，请参阅"备注"。 不可为 null。

`szSymbolCachePath`\
[在]包含可以缓存符号的本地路径的字符串。 不可为 null。

`Flags`\
[在]未使用;始终设置为 0。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则返回错误代码。

## <a name="remarks"></a>备注
 该字符串`szSymbolSearchPath`是一个或多个路径的列表，由分号分隔，以搜索符号。 这些路径可以是本地路径、UNC 样式路径或 URL。 这些路径也可以是不同类型的混合路径。 如果路径为 UNC（例如，[Symserver]Symbols），\\则调试引擎应确定路径是否属于符号服务器，并且应该能够从该服务器加载符号，将其缓存在 指定的`szSymbolCachePath`路径中。

 符号路径还可以包含一个或多个缓存位置。 缓存按优先级顺序列出，优先缓存优先，并由 * 符号分隔。 例如：

```
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*https://msdl.microsoft.com
```

 [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)方法执行符号的实际负载。

## <a name="see-also"></a>请参阅
- [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
