---
title: IDiaSession::get_loadAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::get_loadAddress method
ms.assetid: 5162ae1a-38e3-4571-8995-4ed9be1dec3e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fed7653b5f1a270d2e297cdd2b59366b5b563c3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839181"
---
# <a name="idiasessiongetloadaddress"></a>IDiaSession::get_loadAddress
检索对应于此符号存储区中的符号的可执行文件的加载地址。

## <a name="syntax"></a>语法

```C++
HRESULT get_loadAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个虚拟地址 (VA) 加载的.exe 文件或.dll 文件的位置。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 返回的加载地址始终为零，除非专门设置了使用[idiasession:: Put_loadaddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)