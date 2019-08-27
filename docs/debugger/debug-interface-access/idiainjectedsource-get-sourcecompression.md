---
title: 'Idiainjectedsource:: Get_sourcecompression |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_sourceCompression method
ms.assetid: 854b142f-23a9-466c-bf7f-98e581d5abcd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 00c7783752a183e8afc580c4c74285add8a51041
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839909"
---
# <a name="idiainjectedsourcegetsourcecompression"></a>IDiaInjectedSource::get_sourceCompression
检索源所使用的压缩的指示器。

## <a name="syntax"></a>语法

```C++
HRESULT get_sourceCompression ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回源所使用的压缩的指示器。 零值指示没有源压缩已使用。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值是特定于编译器使用。 例如，编译器可能会使用运行长度编码或 Huffman 样式压缩。

## <a name="see-also"></a>请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)