---
title: IDiaInjectedSource：： get_sourceCompression |Microsoft Docs
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
ms.openlocfilehash: 9428b30df82d92a8c74511644aaf97f2166807a2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743324"
---
# <a name="idiainjectedsourceget_sourcecompression"></a>IDiaInjectedSource::get_sourceCompression
检索使用的源压缩的指示器。

## <a name="syntax"></a>语法

```C++
HRESULT get_sourceCompression ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回使用的源压缩的指示器。 如果值为零，则表示未使用源压缩。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值特定于所使用的编译器。 例如，编译器可能使用运行长度编码或 Huffman 样式压缩。

## <a name="see-also"></a>请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)