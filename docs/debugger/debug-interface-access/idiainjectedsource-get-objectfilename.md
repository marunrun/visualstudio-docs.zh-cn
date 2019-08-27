---
title: IDiaInjectedSource::get_objectFilename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_objectFilename method
ms.assetid: 7c42847a-f0df-443a-a9fe-c495c1271ea8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4bf9b325354bd95678969e5d1db4c13370d6d8b3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839883"
---
# <a name="idiainjectedsourcegetobjectfilename"></a>IDiaInjectedSource::get_objectFilename
检索到的源已编译的对象文件名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_objectFilename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回源已编译到的对象文件名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)