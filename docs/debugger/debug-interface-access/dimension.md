---
title: 维度 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Dimension Symbol
ms.assetid: 94f791da-bfea-454f-8a14-da31e8e1596a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97b03f1a3ceb8424cc3e533512f6d0d3e034f791
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554800"
---
# <a name="dimension"></a>维度
每个 FORTRAN 数组具有由标识的维度`SymTagDimension`符号。

## <a name="properties"></a>属性
 下表显示此符号类型的其他有效属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_lowerBound](../../debugger/debug-interface-access/idiasymbol-get-lowerbound.md)|`IDiaSymbol*`|FORTRAN 数组维度的下限。|
|[IDiaSymbol::get_lowerBoundId](../../debugger/debug-interface-access/idiasymbol-get-lowerboundid.md)|`DWORD`|下界符号 ID。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagDimension`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_upperBound](../../debugger/debug-interface-access/idiasymbol-get-upperbound.md)|`IDiaSymbol*`|FORTRAN 数组维度的上限。|
|[IDiaSymbol::get_upperBoundId](../../debugger/debug-interface-access/idiasymbol-get-upperboundid.md)|`DWORD`|上限符号的 ID。|

## <a name="see-also"></a>请参阅
- [ArrayType](../../debugger/debug-interface-access/arraytype.md)
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)