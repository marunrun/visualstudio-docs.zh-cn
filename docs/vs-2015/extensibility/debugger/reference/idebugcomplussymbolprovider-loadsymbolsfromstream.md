---
title: IDebugComPlusSymbolProvider::LoadSymbolsFromStream |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::LoadSymbolsFromStream
- LoadSymbolsFromStream
ms.assetid: 1de272f0-24f4-4548-8b70-a205cddd4727
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 50ff4d2ca585b243cf5b040e355a94ecb3a0576d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68176769"
---
# <a name="idebugcomplussymbolproviderloadsymbolsfromstream"></a>IDebugComPlusSymbolProvider::LoadSymbolsFromStream
加载调试符号提供数据流。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbolsFromStream(
    ULONG32   ulAppDomainID,
    GUID      guidModule,
    ULONGLONG baseAddress,
    IUnknown* pUnkMetadataImport,
    IStream*  pStream
);
```

```csharp
int LoadSymbolsFromStream(
    uint    ulAppDomainID,
    Guid    guidModule,
    ulong   baseAddress,
    object  pUnkMetadataImport,
    IStream pStream
);
```

#### <a name="parameters"></a>参数
`ulAppDomainID`

 [in]应用程序域的标识符。

`guidModule`

 [in]该模块的唯一标识符。

`baseAddress`

 [in]基本的内存地址。

`pUnkMetadataImport`

 [in]包含符号元数据的对象。

`pStream`

 [in]包含的符号的数据流。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CDebugSymbolProvider**对象，它公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口。 方法调用[LoadSymbolsFromStreamWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromstreamwithcormodule.md)方法。

```cpp
HRESULT CDebugSymbolProvider::LoadSymbolsFromStream(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    ULONGLONG baseOffset,
    IUnknown* pUnkMetadataImport,
    IStream* pStream
)
{
    return LoadSymbolsFromStreamWithCorModule (ulAppDomainID, guidModule, baseOffset, pUnkMetadataImport, NULL, pStream);
}
```

## <a name="see-also"></a>请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
