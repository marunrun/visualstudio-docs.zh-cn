---
title: IDebugSymbolProvider::GetAddressesFromPosition | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition method
ms.assetid: 1b0f02cb-8ace-4614-88f3-0e10239012b3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dcaef1e9675ae395826865604833fdb6683df944
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310187"
---
# <a name="idebugsymbolprovidergetaddressesfromposition"></a>IDebugSymbolProvider::GetAddressesFromPosition
此方法将映射到一个数组的调试地址的文档位置。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAddressesFromPosition( 
   IDebugDocumentPosition2* pDocPos,
   BOOL                     fStatmentOnly,
   IEnumDebugAddresses**    ppEnumBegAddresses,
   IEnumDebugAddresses**    ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromPosition( 
   IDebugDocumentPosition2  pDocPos,
   bool                     fStatmentOnly,
   out IEnumDebugAddresses  ppEnumBegAddresses,
   out IEnumDebugAddresses  ppEnumEndAddresses
);
```

## <a name="parameters"></a>参数
`pDocPos`\
[in]文档位置中。

`fStatmentOnly`\
[in]如果为 TRUE，则限制为单个语句的调试地址。

`ppEnumBegAddresses`\
[out]返回与此语句或行关联的起始调试地址的枚举器。

`ppEnumEndAddresses`\
[out]返回[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)结束的调试地址与此语句或行关联的枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 文档位置通常指示源行组成的范围。 此方法提供的起始和结束调试地址关联使用以下代码行。 某些语言允许跨多个行或包含多个语句的行的语句。 此方法提供了一个标志，用于限制到单个语句的调试地址。

 很可能具有多个调试地址，如下所示的模板大小写的单个语句。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)