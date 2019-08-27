---
title: IDebugSymbolProviderDirect::GetSymUnmanagedReader |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetSymUnmanagedReader
- IDebugSymbolProviderDirect::GetSymUnmanagedReader
ms.assetid: 147bacfa-f66c-43e0-8a72-e601058dc57f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 842201b2dc5163abcd957d8e76f9505298e07a6e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153103"
---
# <a name="idebugsymbolproviderdirectgetsymunmanagedreader"></a>IDebugSymbolProviderDirect::GetSymUnmanagedReader
检索非托管代码的符号读取器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymUnmanagedReader (
   ULONG32    ulAppDomainID,
   GUID       guidModule,
   IUnknown** ppSymUnmanagedReader
);
```

```csharp
int GetSymUnmanagedReader (
   uint       ulAppDomainID,
   Guid       guidModule,
   out object ppSymUnmanagedReader
);
```

#### <a name="parameters"></a>参数
 `ulAppDomainID`

 [in]应用程序域的标识符。

 `guidModule`

 [in]该模块的唯一标识符。

 `ppSymUnmanagedReader`

 [out]返回一个对象，表示非托管代码的符号读取器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)