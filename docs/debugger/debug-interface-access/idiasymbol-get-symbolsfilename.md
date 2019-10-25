---
title: IDiaSymbol::get_symbolsFileName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_symbolsFileName method
ms.assetid: c1aa39ee-d645-431e-bf5f-0640c0998934
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f282f7eeae0dd4def8468322bf73e192503ceef1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739248"
---
# <a name="idiasymbolget_symbolsfilename"></a>IDiaSymbol::get_symbolsFileName
检索从中加载符号的文件的名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_symbolsFileName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回从中加载符号的文件的名称。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性仅对[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值为 `SymTagExe` 且具有全局作用域的符号有效。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)