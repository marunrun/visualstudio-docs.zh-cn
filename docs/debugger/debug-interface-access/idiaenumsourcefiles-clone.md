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
ms.openlocfilehash: 328536b64bdea2591b4ab8c242348b8304984466
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829701"
---
# <a name="idiaenumsourcefilesclone"></a>IDiaEnumSourceFiles::Clone
创建一个包含当前枚举数形式的相同枚举状态的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumSourceFiles** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out]返回[IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)对象，其中包含重复的枚举器。 文件不是的源复制，仅枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)