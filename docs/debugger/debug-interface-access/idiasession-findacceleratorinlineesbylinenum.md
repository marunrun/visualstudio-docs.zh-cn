---
title: IDiaSession::findAcceleratorInlineesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 386c87aa-f7b2-4d38-9dd6-fffba9ff01f0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 12a2f23c42de99e0ea9a9d6c50e2d9aabed589d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839454"
---
# <a name="idiasessionfindacceleratorinlineesbylinenum"></a>IDiaSession::findAcceleratorInlineesByLinenum
返回指定的源位置相对应的内嵌帧的符号的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findAcceleratorInlineeLinesByName ( 
   IDiaSymbol*           parent,
   IDiaSourceFile*       file,
   DWORD                 linenum,
   DWORD                 colnum,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in]`IDiaSymbol` ，对应于需要搜索的加速器存根 （stub） 函数。

 `file`

[in]`IDiaSourceFile`的源位置。

 `linenum`

[in]源位置的行数。

 `colnum`

[in]源位置的列数。

 `ppResult`

[out]一个指向`IDiaEnumLineNumbers`使用结果初始化的接口指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)