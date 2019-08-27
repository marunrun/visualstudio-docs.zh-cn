---
title: IDebugField::Equal |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8af316c9669b00ae8316888c6a7072d4737dd23d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352667"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
此方法将此字段与指定字段相等进行比较。

## <a name="syntax"></a>语法

```cpp
HRESULT Equal( 
   IDebugField* pField
);
```

```csharp
int Equal(
   IDebugField pField
);
```

## <a name="parameters"></a>参数
`pField`\
[in]要与此比较的字段。

## <a name="return-value"></a>返回值
 如果字段是相同的则返回`S_OK`。 如果字段不同，返回`S_FALSE.`否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)