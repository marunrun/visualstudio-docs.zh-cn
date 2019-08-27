---
title: IDebugSymbolProviderDirect::GetMetaDataImport | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetMetaDataImport
- IDebugSymbolProviderDirect::GetMetaDataImport
ms.assetid: b51a492c-af00-4b08-93fb-6c19ee4916aa
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a2cd79581487e7e407cc409c4b8496abc53bfa7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347289"
---
# <a name="idebugsymbolproviderdirectgetmetadataimport"></a>IDebugSymbolProviderDirect::GetMetaDataImport
检索元数据导入信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMetaDataImport (
    GUID*      guid,
    DWORD      appID,
    IUnknown** ppImport
);
```

```csharp
int GetMetaDataImport (
    Guid       guid,
    uint       appID,
    out object ppImport
);
```

## <a name="parameters"></a>参数
`guid`\
[in]该模块的唯一标识符。

`appID`\
[in]应用程序域标识符。

`ppImport`\
[out]返回一个对象，它包含的元数据导入信息。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)