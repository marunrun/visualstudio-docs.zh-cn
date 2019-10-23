---
title: IDiaSession::put_loadAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 39db3bc0e0107e734f5de3f6902a2ca0fcc55bb0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741894"
---
# <a name="idiasessionput_loadaddress"></a>IDiaSession::put_loadAddress
设置与此符号存储区中的符号对应的可执行文件的加载地址。

## <a name="syntax"></a>语法

```C++
HRESULT put_loadAddress ( 
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>参数
 `NewVal`

中可执行文件的加载地址。

## <a name="remarks"></a>备注
 使用此方法的值计算符号虚拟地址（VA）属性。 除非将该属性设置为非零，否则不会计算虚拟地址。

> [!NOTE]
> 如果需要使用符号上的任何虚拟属性，则在获取[IDiaSession](../../debugger/debug-interface-access/idiasession.md)对象时和开始使用对象之前，必须调用此方法。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)