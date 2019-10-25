---
title: IDiaLineNumber::get_sourceFileId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_sourceFileId method
ms.assetid: 4f482a1e-e85f-4173-98de-8e5f7622554b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54b460fc96d71048b192313d03956e3b2cbe321f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743142"
---
# <a name="idialinenumberget_sourcefileid"></a>IDiaLineNumber::get_sourceFileId
检索提供此行的源文件的唯一源文件标识符。

## <a name="syntax"></a>语法

```C++
HRESULT get_sourceFileId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回提供此行的源文件的唯一源文件标识符。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)