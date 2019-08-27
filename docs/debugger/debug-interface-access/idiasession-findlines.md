---
title: 'Idiasession:: Findlines |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLines method
ms.assetid: d6e84916-fd55-457e-b057-57f97b51fe73
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b127cbc5c9ddc5a2aa2d293d1371bab18d191fdb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839285"
---
# <a name="idiasessionfindlines"></a>IDiaSession::findLines
检索指定的编译单位和源文件标识符中的行号。

## <a name="syntax"></a>语法

```C++
HRESULT findLines ( 
   IDiaSymbol*           compiland,
   IDiaSourceFile*       file,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `compiland`

[in][IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示将编译单位。 使用此接口作为要在其中搜索的行号的上下文。

 `file`

[in][IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，表示要在其中搜索的行号的源文件。

 `ppResult`

[out]返回[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)检索包含的行号列表的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)