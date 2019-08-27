---
title: IDiaSession::findInlineFramesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: df9e68f6-e0a4-4cf6-b11d-61c40351e0cd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aeb9d7b9925e8708ab100e68f88b28310da68fce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827309"
---
# <a name="idiasessionfindinlineframesbyva"></a>IDiaSession::findInlineFramesByVA
检索一个枚举，允许客户端用于循环访问所有指定的虚拟地址 (VA) 上的内联框架。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineFramesByVA ( 
   IDiaSymbol*       parent,   ULONGLONG         va,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in]`IDiaSymbol`表示父对象。

 `va`

[in]指定的地址作为弗吉尼亚

 `ppResult`

[out]保存`IDiaEnumSymbols`对象，其中包含检索到的框架的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)