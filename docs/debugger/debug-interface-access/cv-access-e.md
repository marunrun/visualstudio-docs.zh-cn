---
title: CV_access_e | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CV_access_e enumeration
ms.assetid: 33c05d65-abb4-4800-a382-54a3805ea7b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbe338ba9d3aa6cbc795606c3fa285526afdfd36
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745361"
---
# <a name="cv_access_e"></a>CV_access_e
指定成员函数和变量的可见性（访问级别）的作用域。

## <a name="syntax"></a>语法

```C++
typedef enum CV_access_e {
    CV_private   = 1,
    CV_protected = 2,
    CV_public    = 3
} CV_access_e;
```

## <a name="elements"></a>元素
CV_private 成员具有私有访问权限。

CV_protected 成员具有受保护的访问权限。

CV_public 成员具有公共访问权限。

## <a name="remarks"></a>备注
此处不包含 `friend` 访问说明符，因为它通常由对类的私有和受保护元素具有访问权限的非成员函数使用。 使用[IDiaSymbol：： get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)方法查找具有 `SymTagFriend` 访问权限的符号。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
