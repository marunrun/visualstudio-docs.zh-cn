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
ms.openlocfilehash: 6d08168a83b9bb635fd6a0e22dc22f91a454001f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742324"
---
# <a name="idiasessionfindacceleratorinlineesbylinenum"></a>IDiaSession::findAcceleratorInlineesByLinenum
返回与指定源位置对应的内联帧的符号枚举。

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

中与需要搜索的快捷键存根函数相对应的 `IDiaSymbol`。

 `file`

中源位置的 `IDiaSourceFile`。

 `linenum`

中源位置的行号。

 `colnum`

中源位置的列号。

 `ppResult`

弄指向使用结果初始化的 `IDiaEnumLineNumbers` 接口指针的指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)