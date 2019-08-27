---
title: 'Idiainjectedsource:: Get_source |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_source method
ms.assetid: 3c0b5386-321f-4f8f-85cc-e2ee7b4cc3d2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 604160cdaf8c1ff28b306106afe34e047768f3c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828429"
---
# <a name="idiainjectedsourcegetsource"></a>IDiaInjectedSource::get_source
检索源代码字节。

## <a name="syntax"></a>语法

```C++
HRESULT get_source ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>参数
 `cbData`

[in]表示大小的数据缓冲区的字节数。

 `pcbData`

[out]返回表示字节的字节数返回。 如果`data`是`NULL`，然后`pcbData`是可用的数据的字节总数。

 `data[]`

[out]若要使用的源字节填充缓冲区。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)