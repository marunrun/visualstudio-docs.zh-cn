---
title: IDebugModule2：： ReloadSymbols_Deprecated |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::ReloadSymbols
helpviewer_keywords:
- IDebugModule2::ReloadSymbols method
ms.assetid: 0f9f0133-7d58-4cd9-a6ca-1141e095749d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e776434e17d90cd2c61c926bbf0100a44ecc524b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80726915"
---
# <a name="idebugmodule2reloadsymbols_deprecated"></a>IDebugModule2::ReloadSymbols_Deprecated
已过时。 请勿使用。 重新加载此模块的符号。

## <a name="syntax"></a>语法

```cpp
HRESULT ReloadSymbols( 
   LPCOLESTR pszUrlToSymbols,
   BSTR*     pbstrDebugMessage
);
```

```csharp
int ReloadSymbols( 
   string     pszUrlToSymbols,
   out string pbstrDebugMessage
);
```

## <a name="parameters"></a>参数
`pszUrlToSymbols`\
中指向符号存储区的路径。

`pbstrDebugMessage`\
弄返回一条信息性消息，如状态或错误消息，它显示在 "模块" 窗口中的模块名称右侧。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 调试引擎应该总是返回 `E_FAIL` 。

## <a name="remarks"></a>备注
 不再支持此方法。 改为实现 [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)
