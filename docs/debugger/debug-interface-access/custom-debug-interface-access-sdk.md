---
title: 自定义 （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Custom symbol
ms.assetid: a219fc83-d2a8-4bc5-b7e1-bfafeb247f16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 15e0d58c49a66416371c7e66e12f469e6d224c91
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555138"
---
# <a name="custom-debug-interface-access-sdk"></a>自定义（调试接口访问 SDK）
某些编译器引入不识别的任何标准的词法符号类型的符号。 这些符号由标识`SymTagCustom`标记。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_dataBytes](../../debugger/debug-interface-access/idiasymbol-get-databytes.md)|`BYTE`|与符号关联的数据的数组。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagCustom`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|

## <a name="see-also"></a>请参阅
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)