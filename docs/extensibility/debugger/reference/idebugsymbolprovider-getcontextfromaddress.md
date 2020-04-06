---
title: IDebug符号提供程序：从地址获取上下文 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetContextFromAddress
helpviewer_keywords:
- IDebugSymbolProvider::GetContextFromAddress method
ms.assetid: 7a27d56f-20d4-4e5c-af7b-7307d3aff0a1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ca6c3fa5d657100ecce55de31117ea2c2532374d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719247"
---
# <a name="idebugsymbolprovidergetcontextfromaddress"></a>IDebugSymbolProvider::GetContextFromAddress
此方法将调试地址映射到文档上下文中。

## <a name="syntax"></a>语法

```cpp
HRESULT GetContextFromAddress( 
   IDebugAddress*           pAddress,
   IDebugDocumentContext2** ppDocContext
);
```

```csharp
int GetContextFromAddress(
   IDebugAddress              pAddress,
   out IDebugDocumentContext2 ppDocContext
);
```

## <a name="parameters"></a>参数
`pAddress`\
[在]由[IDebug 地址](../../../extensibility/debugger/reference/idebugaddress.md)接口表示的调试地址。

`ppDocContext`\
[出]返回由[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)接口表示的文档上下文。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
