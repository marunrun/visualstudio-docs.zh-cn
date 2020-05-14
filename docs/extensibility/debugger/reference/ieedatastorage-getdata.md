---
title: IEEData存储：获取数据 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 62a1295aeb2a6afad51dee0f1015e3ab01d13fbb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718208"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
从对象检索指定数量的字节。

## <a name="syntax"></a>语法

```cpp
HRESULT GetData(
   ULONG  dataSize,
   ULONG* sizeGotten,
   BYTE*  data
);
```

```csharp
int GetData(
   uint     dataSize,
   out uint sizeGotten,
   byte[]   data
);
```

## <a name="parameters"></a>参数
`dataSize`\
[在]要检索的字节数（`data`数组必须至少保留此字节数）。

`sizeGotten`\
[出]返回实际检索的字节数。

`data`\
[进出]要用请求的数据填充的数组。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法的建议用途是检索到本地数组中的所有数据字节，因为在检索过程中无法跳过字节。 在这种情况下，参数`dataSize`应该是[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)方法返回的值。

## <a name="see-also"></a>请参阅
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
