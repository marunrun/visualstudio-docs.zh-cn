---
title: 符号和符号标记 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK]
ms.assetid: 2ee3a262-cda6-48bf-b799-a37edde6c8b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6affc24a84ef4d008ece5f95e45a11eb70f33b4e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62854708"
---
# <a name="symbols-and-symbol-tags"></a>符号和符号标记
使用调试接口访问 (DIA) SDK Api 可以访问的符号作为在程序数据库 (.pdb) 文件中存储有关已编译的程序的调试信息。 所有符号都有[idiasymbol:: Get_symtag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)和一个[idiasymbol:: Get_symindexid](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)属性。 `symTag`属性指示符号的类型由定义[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举。 `symIndexId`属性是`DWORD`值，该值包含一个符号的每个实例的唯一标识符。

 符号还具有属性，可以指定有关其他信息的符号以及对其他符号的引用通常[idiasymbol:: Get_lexicalparent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)或[idiasymbol:: Get_classparent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md). 当查询包含的引用的属性时，作为返回的引用[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象。 此类属性始终配对与另一个属性的名称相同但后缀"id"，例如， [idiasymbol:: Get_lexicalparentid](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)并[idiasymbol:: Get_classparentid](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)。 中的表[符号位置](../../debugger/debug-interface-access/symbol-locations.md)，[符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)，并[符号类型的类层次结构的](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)概述不同类型的每个属性的符号。 这些属性可能具有相关的信息或对其他符号的引用。 因为`*Id`属性是只需数字序号标识符的相关属性，进一步讨论中省略了这些。 称其仅在需要时参数获取的。

 在尝试访问的属性，如果未发生错误，并且符号属性分配一个值，该属性的"get"方法返回`S_OK`。 返回值为`S_FALSE`指示该属性不能用于当前符号。

## <a name="in-this-section"></a>本节内容

[符号位置](../../debugger/debug-interface-access/symbol-locations.md)

介绍不同类型的符号可以具有的位置。

[符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)

介绍构成词法层次结构，如文件、 模块和函数的符号类型。

[符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)

介绍对应于不同的语言元素，如类、 数组和函数返回类型的符号类型。

## <a name="see-also"></a>请参阅

- [调试接口访问 SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)