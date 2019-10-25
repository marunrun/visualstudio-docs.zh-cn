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
ms.openlocfilehash: dea4b53daae31c90753ef7afb293e69157f58e41
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741815"
---
# <a name="idiasourcefileget_compilands"></a>IDiaSourceFile::get_compilands
检索具有引用此文件的行号的 compiland 的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT get_compilands ( 
   IDiaEnumSymbols** ppRetVal
);
```

#### <a name="parameters"></a>参数
 `ppRetVal`

弄返回一个[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)对象，该对象包含具有引用此文件的行号的所有 compiland 的列表。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)