---
title: IDiaSession：： findSymbolsByRVAForAcceleratorPointerTag |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: a073cc45-0c7b-417e-b5fc-a3b08beccdbc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eb1b24d24de35de30b24937a6cfbf59d12f69482
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741991"
---
# <a name="idiasessionfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSession::findSymbolsByRVAForAcceleratorPointerTag
给定相应的标记值后，此方法将返回一个符号枚举，其中包含在指定的相对虚拟地址处的指定父加速器存根函数中。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag ( 
   IDiaSymbol*           parent,
   DWORD                 tagValue,
   DWORD                 rva,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

中与要搜索的快捷键存根函数相对应的 `IDiaSymbol`。

 `tagValue`

中指针标记值。

 `rva`

中相对虚拟地址。

 `ppResult`

弄指向使用结果初始化的 `IDiaEnumSymbols` 接口指针的指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 仅在对应于快捷键存根函数的 `IDiaSymbol` 接口上调用此方法。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)