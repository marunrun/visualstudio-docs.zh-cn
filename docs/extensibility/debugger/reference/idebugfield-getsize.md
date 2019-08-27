---
title: IDebugField::GetSize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetSize
helpviewer_keywords:
- IDebugField::GetSize method
ms.assetid: 73329924-3751-4f44-af54-5986b7943374
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db4ef8a41ec6759194cc35203b6458c7688f4322
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333206"
---
# <a name="idebugfieldgetsize"></a>IDebugField::GetSize
此方法获取的字段，以字节为单位的大小。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   DWORD* pdwSize
);
```

```csharp
int GetSize(
   out uint pdwSize
);
```

## <a name="parameters"></a>参数
`pdwSize`\
[out]返回的大小。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 所有字段都具有一个类型和所有类型都具有一个大小。 例如，具有一种类型的字节的字段具有 1 个字节的大小。

## <a name="see-also"></a>请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)