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
ms.openlocfilehash: 352c9516180c0ee0021fca4e0913f154f3b8d46f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744090"
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

中要检索的[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象的索引。 索引的范围为0到 `count`-1，其中 `count` 由[IDiaEnumSourceFiles：： get_Count](../../debugger/debug-interface-access/idiaenumsourcefiles-get-count.md)方法返回。

 sourceFile

弄返回一个[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，该对象表示所需的源文件。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)