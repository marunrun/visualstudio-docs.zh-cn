---
title: IDiaInjectedSource::get_virtualFilename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_virtualFilename method
ms.assetid: b9977075-8fd1-4b11-bfff-d87e9f2586dc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d60a8c46c4a9e6f17e0123554ac25cb14bbf430b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743301"
---
# <a name="idiainjectedsourceget_virtualfilename"></a>IDiaInjectedSource::get_virtualFilename
检索为非文件源代码指定的名称;也就是说，注入的代码。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualFilename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回为注入的非文件源代码指定的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)