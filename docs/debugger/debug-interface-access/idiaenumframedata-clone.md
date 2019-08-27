---
title: 'Idiaenumframedata:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Clone Method
ms.assetid: 28a17300-1626-422f-a17a-3a4d3872c37c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5c86d9f4f8eb02b0389e7ea28b5858f8576f6c6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838397"
---
# <a name="idiaenumframedataclone"></a>IDiaEnumFrameData::Clone
创建一个包含当前枚举数形式的相同枚举状态的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT Clone( 
   IDiaEnumFrameData** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out]返回[IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)对象，其中包含重复的枚举器。 重复的数据不是的框架，仅枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)