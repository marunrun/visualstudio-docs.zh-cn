---
title: IDiaDataSource：： loadDataFromIStream |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromIStream method
ms.assetid: 8fe33eea-1457-4b8c-ae19-f1ede5578483
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b2bcf657b4404ed72059351175d124a9c07abb46
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744942"
---
# <a name="idiadatasourceloaddatafromistream"></a>IDiaDataSource::loadDataFromIStream
准备通过内存中数据流访问的程序数据库（.pdb）文件中存储的调试数据。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataFromIStream ( 
   IStream* pIStream
);
```

#### <a name="parameters"></a>参数
 pIStream

中一个 <xref:IStream> 对象，该对象表示要使用的数据流。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 下表显示了此方法的可能的返回值。

|“值”|描述|
|-----------|-----------------|
|E_PDB_FORMAT|尝试访问具有过时格式的文件。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|数据源已准备就绪。|

## <a name="remarks"></a>备注
 此方法允许通过 <xref:IStream> 对象从内存中获取可执行文件的调试数据。

 若要加载 .pdb 文件而不进行验证，请使用[IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)方法。

 若要根据特定条件验证 .pdb 文件，请使用[IDiaDataSource：： loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)方法。

 若要获取对数据加载过程（通过回调机制）的访问权限，请使用[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)