---
title: IDiaSymbol::get_sourceFileName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_sourceFileName method
ms.assetid: 0f5dce88-829e-4df3-8acd-8d71076ad167
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 258abfc908a065f7f1854cb7b52d4c16afbdd314
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64798992"
---
# <a name="idiasymbolgetsourcefilename"></a>IDiaSymbol::get_sourceFileName
检索编译单位源文件的文件名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_sourceFileName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回编译单位源文件的文件名。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)