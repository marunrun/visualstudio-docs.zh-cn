---
title: IDebug符号搜索事件2：：获取符号搜索信息 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
helpviewer_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
ms.assetid: ae9eb72b-f2aa-43b8-87ca-da19d2e78d17
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be498154a8141c61f114682893d0aaf8b841cf95
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718897"
---
# <a name="idebugsymbolsearchevent2getsymbolsearchinfo"></a>IDebugSymbolSearchEvent2::GetSymbolSearchInfo
由事件处理程序调用以检索有关符号加载进程的结果。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymbolSearchInfo(
   IDebugModule3**    pModule,
   BSTR*              pbstrDebugMessage,
   MODULE_INFO_FLAGS* pdwModuleInfoFlags
);
```

```csharp
int GetSymbolSearchInfo(
   IDebugModule3              pModule,
   ref string                 pbstrDebugMessage,
   out enum_MODULE_INFO_FLAGS pdwModuleInfoFlags
);
```

## <a name="parameters"></a>参数
`pModule`\
[出]IDebugModule3 对象，表示为其加载符号的模块。

`pbstrDebugMessage`\
[进出]返回包含模块中任何错误消息的字符串。 如果没有错误，则此字符串将仅包含模块的名称，但它永远不会为空。

> [!NOTE]
> [C++]`pbstrDebugMessage`不能，`NULL`必须释放与`SysFreeString`。

`pdwModuleInfoFlags`\
[出][MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)枚举中的标志的组合，指示是否加载了任何符号。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。

## <a name="remarks"></a>备注
 当处理程序尝试加载模块的调试符号后收到[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)事件时，处理程序可以调用此方法以确定该加载的结果。

## <a name="see-also"></a>请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
