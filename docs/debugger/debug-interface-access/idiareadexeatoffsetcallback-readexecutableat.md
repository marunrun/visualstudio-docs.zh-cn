---
title: IDiaReadExeAtOffsetCallback::ReadExecutableAt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtOffsetCallback::ReadExecutableAt method
ms.assetid: 30b1cef0-b366-4712-8e89-d21f640964f8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0f199db93fa2ea0b3ee2633f9af8a02fff5a4fdf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828205"
---
# <a name="idiareadexeatoffsetcallbackreadexecutableat"></a>IDiaReadExeAtOffsetCallback::ReadExecutableAt
读取指定的可执行文件从指定的偏移量开始的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT ReadExecutableAt ( 
   DWORDLONG fileOffset,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>参数
 fileOffset

[in]开始读取的可执行文件中的偏移量。

 cbData

[in]要读取的字节数。

 pcbData

[out]返回读取的字节数。

 data[]

[in、 out]填充从文件中读取的字节数组。

## <a name="remarks"></a>备注
 若要从使用绝对文件偏移量的可执行文件加载数据字节的 DIA 支持代码调用此方法。 调用此方法支持[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)