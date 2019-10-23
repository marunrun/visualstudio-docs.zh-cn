---
title: IDiaEnumSourceFiles::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Clone method
ms.assetid: 87a9a9b6-3927-4131-927c-ad95f8f098b9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b1e3d1dde9d58fb11bd5e06b7394eaab4cc41e9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744123"
---
# <a name="idiaenumsourcefilesclone"></a>IDiaEnumSourceFiles::Clone
创建与当前枚举数包含相同枚举状态的枚举数。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumSourceFiles** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

弄返回一个[IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)对象，该对象包含枚举器的副本。 源文件不会复制，只会复制枚举器。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)