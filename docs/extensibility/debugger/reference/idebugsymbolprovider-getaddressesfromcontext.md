---
title: IDebugSymbol 提供程序：从上下文获取地址 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7cf7599cf0fc37c16467c29c2b432f1f58b172fe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719431"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
此方法将文档上下文映射到调试地址数组中。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAddressesFromContext( 
   IDebugDocumentContext2* pDocContext,
   BOOL                    fStatmentOnly,
   IEnumDebugAddresses**   ppEnumBegAddresses,
   IEnumDebugAddresses**   ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromContext(
   IDebugDocumentContext2  pDocContext,
   bool                    fStatmentOnly,
   out IEnumDebugAddresses ppEnumBegAddresses,
   out IEnumDebugAddresses ppEnumEndAddresses
);
```

## <a name="parameters"></a>参数
`pDocContext`\
[在]文档上下文。

`fStatmentOnly`\
[在]如果为 TRUE，则将调试地址限制为单个语句。

`ppEnumBegAddresses`\
[出]返回与此语句或行关联的起始调试地址的枚举器。

`ppEnumEndAddresses`\
[出]返回与此语句或行关联的结束调试地址的[IEnumDebug 地址](../../../extensibility/debugger/reference/ienumdebugaddresses.md)枚举器。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 文档上下文通常指示源行的范围。 此方法提供与这些行关联的开始和结束调试地址。 某些语言允许跨多行的语句或包含多个语句的行。 此方法提供一个标志，用于将调试地址限制为单个语句。

 单个语句可以有多个调试地址，如模板。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
