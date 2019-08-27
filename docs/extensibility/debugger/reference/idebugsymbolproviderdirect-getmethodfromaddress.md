---
title: IDebugSymbolProviderDirect::GetMethodFromAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect::GetMethodFromAddress
- GetMethodFromAddress
ms.assetid: 33ffd197-1221-41bc-a9f6-f133ebdcb783
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89a110886837c793d45842db6ed80690626dd9d6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335168"
---
# <a name="idebugsymbolproviderdirectgetmethodfromaddress"></a>IDebugSymbolProviderDirect::GetMethodFromAddress
检索有关指定的调试地址处的方法的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMethodFromAddress(
   IDebugAddress* pAddress,
   GUID*          pGuid,
   DWORD*         pAppID,
   _mdToken*      pTokenClass,
   _mdToken*      pTokenMethod,
   DWORD*         pdwOffset,
   DWORD*         pdwVersion
);
```

```csharp
int GetMethodFromAddress(
   IDebugAddress pAddress,
   out Guid      pGuid,
   out uint      pAppID,
   out uint      pTokenClass,
   out uint      pTokenMethod,
   out uint      pdwOffset,
   out uint      pdwVersion
);
```

## <a name="parameters"></a>参数
`pAddress`\
[in]调试由表示的地址[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口。

`pGuid`\
[out]该模块的唯一标识符。

`pAppID`\
[out]应用程序域的标识符。

`pTokenClass`\
[out]令牌，它表示包含类。

`pTokenMethod`\
[out]标记，表示该模块。

`pdwOffset`\
[out]以字节为单位从开头的偏移量`pAddress`参数。

`pdwVersion`\
[out]该方法的版本号。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)