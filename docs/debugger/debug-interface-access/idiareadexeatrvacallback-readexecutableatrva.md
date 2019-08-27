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
ms.openlocfilehash: cf423ddc91926fb04adac849783b7c26b4c4f720
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828472"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
读取指定的开始的指定相对虚拟地址 (RVA) 从可执行文件的字节数。

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

[in]若要开始读取的可执行文件中的 RVA。

 `cbData`

[in]要读取的字节数。

 `pcbData`

[out]返回读取的字节数。

 `data[]`

[in、 out]填充从文件中读取的字节数组。

## <a name="remarks"></a>备注
 若要从使用的相对虚拟地址的可执行文件加载数据字节的 DIA 支持代码调用此方法。 调用此方法支持[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)