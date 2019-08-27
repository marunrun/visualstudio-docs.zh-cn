---
title: IDiaStackFrame::get_rawLVarInstanceValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_rawLVarInstanceValue method
ms.assetid: ce526259-85a6-475b-9274-0b3a21d95db2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a8ad236307360a96f64999313764424305980fc9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838114"
---
# <a name="idiastackframegetrawlvarinstancevalue"></a>IDiaStackFrame::get_rawLVarInstanceValue
此方法作为原始字节检索指定的本地变量的值。

## <a name="syntax"></a>语法

```C++
HRESULT get_rawLVarInstanceValue(
   IDiaLVarInstance* pInstance,
   DWORD             cbDataMax,
   DWORD*            pcbData,
   BYTE*             pbData
);
```

#### <a name="parameters"></a>参数
 `pInstance`

[in]`IDiaLVarInstance`对象，表示要获取其值的本地变量的实例。

 `cbDataMax`

[in]指向的缓冲区中的字节的最大数目`pbData`。 这可以是 8 个字节的最大值 (`sizeof(ULONGLONG)`)。

 `pcbData`

[out]返回的实际存储在缓冲区中的字节数。

 `pbData`

[out]若要使用数据填充缓冲区。 该类型不能为 `NULL`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)