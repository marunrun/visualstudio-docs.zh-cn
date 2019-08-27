---
title: IDiaEnumSourceFiles::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Item method
ms.assetid: 3c19d7ed-0232-4b0e-9b10-f33ed9e0c93b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 403aa09a487ea1587ab30389f180afecec5ac6bf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833333"
---
# <a name="idiaenumsourcefilesitem"></a>IDiaEnumSourceFiles::Item
通过索引检索源文件。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD            index,
   IDiaSourceFile** sourceFile
);
```

#### <a name="parameters"></a>参数
 索引

[in]索引[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)要检索对象。 索引是 0 到范围内`count`-1，其中`count`返回的[idiaenumsourcefiles:: Get_count](../../debugger/debug-interface-access/idiaenumsourcefiles-get-count.md)方法。

 sourceFile

[out]返回[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，表示所需的源文件。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)