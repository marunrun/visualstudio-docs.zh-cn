---
title: IDebugEngine3：： SetSymbolPath |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730664"
---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
设置要为调试符号搜索的一个或哪些路径。

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
中包含符号搜索路径的字符串。 有关详细信息，请参阅 "备注"。 不能为 null。

`szSymbolCachePath`\
中包含可在其中缓存符号的本地路径的字符串。 不能为 null。

`Flags`\
中未使用;始终设置为0。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 字符串 `szSymbolSearchPath` 是用分号分隔的一个或多个路径的列表，用于搜索符号。 这些路径可以是本地路径、UNC 样式路径或 URL。 这些路径也可以是不同类型的混合。 如果路径为 UNC (例如， \\ \Symserver\Symbols) ，则调试引擎应确定该路径是否指向符号服务器，并应能够从该服务器加载符号，并将它们缓存到指定的路径中 `szSymbolCachePath` 。

 符号路径还可以包含一个或多个缓存位置。 缓存按优先级顺序列出，最高优先级缓存优先，并用 * 符号分隔。 例如：

```
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*https://msdl.microsoft.com
```

 [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)方法执行符号的实际加载。

## <a name="see-also"></a>另请参阅
- [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
