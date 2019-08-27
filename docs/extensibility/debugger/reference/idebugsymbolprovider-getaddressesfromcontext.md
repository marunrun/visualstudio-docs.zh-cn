---
title: IDebugSymbolProvider::GetAddressesFromContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ff38d2bd286c0a1ff82aafc3526936447be69056
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335222"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
此方法将文档上下文映射到调试地址的数组。

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
[in]文档上下文中。

`fStatmentOnly`\
[in]如果为 TRUE，则限制为单个语句的调试地址。

`ppEnumBegAddresses`\
[out]返回与此语句或行关联的起始调试地址的枚举器。

`ppEnumEndAddresses`\
[out]返回[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)结束的调试地址与此语句或行关联的枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 文档上下文通常指示源行组成的范围。 此方法提供的起始和结束调试地址关联使用以下代码行。 某些语言允许跨多个行或包含多个语句的行的语句。 此方法提供了一个标志，用于限制到单个语句的调试地址。

 很可能具有多个调试地址，如下所示的模板大小写的单个语句。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)