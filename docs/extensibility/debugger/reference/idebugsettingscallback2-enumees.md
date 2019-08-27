---
title: IDebugSettingsCallback2::EnumEEs | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::EnumEEs
ms.assetid: 9f884c49-426f-461b-b547-9d909486e73f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc9073ae5244b05234b3f37874bd6bcd6347954f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322154"
---
# <a name="idebugsettingscallback2enumees"></a>IDebugSettingsCallback2::EnumEEs
枚举给定语言和供应商标识符可用表达式计算器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumEEs(
   DWORD  celtBuffer,
   GUID*  rgguidLang,
   GUID*  rgguidVendor,
   DWORD* pceltEEs
);
```

```csharp
public int EnumEEs(
   uint       celtBuffer,
   ref Guid   rgguidLang,
   ref Guid   rgguidVendor,
   ref uint[] pceltEEs
);
```

## <a name="parameters"></a>参数
`celtBuffer`\
[in]中的元素数`pceltEEs`缓冲区。

`rgguidLang`\
[in、 out]编程语言的唯一标识符。

`rgguidVendor`\
[in、 out]供应商的唯一标识符。

`pceltEEs`\
[in、 out]表达式计算器的数组。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)