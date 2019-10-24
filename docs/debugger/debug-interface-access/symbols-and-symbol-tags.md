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
ms.openlocfilehash: 5d2281a82926dabfde88b8d4bb9096f0e9624211
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738520"
---
# <a name="symbols-and-symbol-tags"></a>符号和符号标记
有关编译的程序的调试信息存储在程序数据库（.pdb）文件中，作为可使用调试接口访问（DIA） SDK Api 访问的符号。 所有符号都有一个[IDiaSymbol：： get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)和一个[IDiaSymbol：： get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)属性。 @No__t_0 属性指示[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举定义的符号类型。 @No__t_0 属性是一个 `DWORD` 值，该值包含符号的每个实例的唯一标识符。

 符号还具有一些属性，这些属性可以指定有关符号的其他信息以及对其他符号的引用，最常见的方式是[IDiaSymbol：： get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)或[IDiaSymbol：： get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)。 查询包含引用的属性时，该引用将作为[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象返回。 此类属性始终与具有相同名称的另一个属性配对，但带有后缀 "Id"，例如， [IDiaSymbol：： get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)和[IDiaSymbol：： get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)。 符号[位置](../../debugger/debug-interface-access/symbol-locations.md)的表、符号[类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)和[符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)概述了每种不同类型的符号的属性。 这些属性可能包含有关或引用其他符号的相关信息。 由于 `*Id` 属性只是其相关属性的数字序数标识符，因此，它们将被进一步讨论。 它们仅被称为参数说明所需的位置。

 尝试访问属性时，如果未发生错误并且已为符号属性赋值，则该属性的 "get" 方法将返回 `S_OK`。 @No__t_0 的返回值指示该属性对于当前符号无效。

## <a name="in-this-section"></a>本节内容

[符号位置](../../debugger/debug-interface-access/symbol-locations.md)

描述符号可以具有的不同类型的位置。

[符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)

描述构成词汇层次结构（如文件、模块和函数）的符号类型。

[符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)

描述与不同语言元素（如类、数组和函数返回类型）对应的符号类型。

## <a name="see-also"></a>请参阅

- [调试接口访问 SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)