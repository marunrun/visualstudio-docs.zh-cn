---
title: IDiaSourceFile::get_compilands | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_compilands method
ms.assetid: 57deb50a-9c22-43ea-a80c-eab205997bc4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 15ebc8296bdf78515b31d38a7543a4f41db84664
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838241"
---
# <a name="idiasourcefilegetcompilands"></a>IDiaSourceFile::get_compilands
检索了行号引用此文件的编译单位的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT get_compilands ( 
   IDiaEnumSymbols** ppRetVal
);
```

#### <a name="parameters"></a>参数
 `ppRetVal`

[out]返回[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)对象，其中包含了引用此文件的行号的所有编译单位的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)