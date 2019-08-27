---
title: 'Idiadatasource:: Loaddatafromistream |Microsoft Docs'
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
ms.openlocfilehash: cb9b218935085b04ae1a9931733aeca34766aa5f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833681"
---
# <a name="idiadatasourceloaddatafromistream"></a>IDiaDataSource::loadDataFromIStream
准备存储在内存中数据的流通过访问程序数据库 (.pdb) 文件中的调试数据。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataFromIStream ( 
   IStream* pIStream
);
```

#### <a name="parameters"></a>参数
 pIStream

[in]<xref:IStream>对象，表示要使用的数据流。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了可能的此方法的返回值。

|“值”|描述|
|-----------|-----------------|
|E_PDB_FORMAT|尝试访问具有过时的格式的文件。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|已准备好数据源。|

## <a name="remarks"></a>备注
 此方法允许可执行文件以获取通过内存中的调试数据<xref:IStream>对象。

 若要加载的.pdb 文件而不进行验证，请使用[idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)方法。

 若要验证.pdb 文件是否符合特定条件，请使用[idiadatasource:: Loadandvalidatedatafrompdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)方法。

 若要访问的数据加载过程 （通过一种回调机制），请使用[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)