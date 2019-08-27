---
title: 'Idiaenumdebugstreams:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Clone method
ms.assetid: e85ec592-de97-4f95-a774-1623315ba415
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 11a7f8e051350b066c745c47530ab4ed818f8b1b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838384"
---
# <a name="idiaenumdebugstreamsclone"></a>IDiaEnumDebugStreams::Clone
创建一个包含当前枚举数形式的相同枚举状态的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumDebugStreams** ppenum
);
```

#### <a name="parameters"></a>参数
 `ppenum`

[out]返回[IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)对象，其中包含重复的枚举器。 流不会重复，仅枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)