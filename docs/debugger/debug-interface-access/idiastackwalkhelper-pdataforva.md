---
title: IDiaStackWalkHelper::pdataForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::pdataByVA method
ms.assetid: fafc38fe-74dc-4726-9a51-eebf3a673d7f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6315032a36369eff7a5d43241ae4968a64ad42cc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831890"
---
# <a name="idiastackwalkhelperpdataforva"></a>IDiaStackWalkHelper::pdataForVA
返回与虚拟地址相关联的 PDATA 数据块。

## <a name="syntax"></a>语法

```C++
HRESULT pdataForVA( 
   ULONGLONG  va,
   DWORD      cbData,
   DWORD*     pcbData,
   BYTE*      pbData
);
```

#### <a name="parameters"></a>参数
 `va`

[in]指定要获取的数据的虚拟地址。

 `cbData`

[in]以字节为单位来获取数据的大小。

 `pcbData`

[out]返回以字节为单位获取数据的实际大小。

 `pbData`

[in、 out]使用所请求的数据填充缓冲区。 不能为 `NULL`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`是否存在指定的地址不 PDATA。 否则，返回错误代码。

## <a name="remarks"></a>备注
 PDATA （名为".pdata"一节） 的编译单位包含有关异常处理函数的信息。

 调用方知道了要使调用方具有要求数据量对于提供了无需返回的数据量。 因此，它是可接受的返回错误，如果此方法的实现`pbData`参数是`NULL`。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)