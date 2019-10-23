---
title: IDiaReadExeAtRVACallback::ReadExecutableAtRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback::ReadExecutableAtRVA method
ms.assetid: 3c1e965f-8f05-41a8-86d8-01830b2377c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ca1b1ec2bea56ad167951ad8b60cf849bd22e315
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742784"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
从可执行文件中读取指定的相对虚拟地址（RVA）开始的指定字节数。

## <a name="syntax"></a>语法

```C++
HRESULT ReadExecutableAtRVA ( 
   DWORD  relativeVirtualAddress,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>参数
 `relativeVirtualAddress`

中要开始读取的可执行文件中的 RVA。

 `cbData`

中要读取的字节数。

 `pcbData`

弄返回读取的字节数。

 `data[]`

[in，out]使用从文件中读取的字节填充的数组。

## <a name="remarks"></a>备注
 DIA 支持代码调用此方法，通过使用相对虚拟地址从可执行文件加载数据字节。 调用此方法是为了支持[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)