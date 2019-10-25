---
title: IDiaLineNumber::get_addressOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_addressOffset method
ms.assetid: 3bcb5500-b26c-4d3c-9d81-0a389a3715c3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b99addc04a7b9dc2f2b77d1943605f8c24af6aa7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743289"
---
# <a name="idialinenumberget_addressoffset"></a>IDiaLineNumber::get_addressOffset
检索内存地址中某个块开始处的偏移量部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回某个块开始的内存地址的偏移量部分。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="example"></a>示例

```C++
CComPtr< IDiaLineNumber > pLine;
DWORD offset;
pLine->get_addressOffset( &offset);
```

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
- [IDiaLineNumber::get_addressSection](../../debugger/debug-interface-access/idialinenumber-get-addresssection.md)