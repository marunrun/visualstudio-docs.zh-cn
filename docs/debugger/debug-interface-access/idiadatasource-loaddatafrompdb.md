---
title: 'Idiadatasource:: Loaddatafrompdb |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromPdb method
ms.assetid: 02159073-8144-47f8-a0b0-aa0edcb92b5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fb34098f8d69d3c8618c406eff9666d52eace1f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554139"
---
# <a name="idiadatasourceloaddatafrompdb"></a>IDiaDataSource::loadDataFromPdb
此时将打开并准备程序数据库 (.pdb) 文件用作调试数据源。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataFromPdb (
   LPCOLESTR pdbPath
);
```

#### <a name="parameters"></a>参数
pdbPath

[in].Pdb 文件的路径。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了可能的此方法的返回值。

|“值”|描述|
|-----------|-----------------|
|E_PDB_NOT_FOUND|无法打开该文件，或确定该文件具有无效的格式。|
|E_PDB_FORMAT|尝试访问具有过时的格式的文件。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|已准备好数据源。|

## <a name="remarks"></a>备注
此方法直接从.pdb 文件加载调试数据。

若要验证.pdb 文件是否符合特定条件，请使用[idiadatasource:: Loadandvalidatedatafrompdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)方法。

若要访问的数据加载过程 （通过一种回调机制），请使用[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

若要直接从内存加载的.pdb 文件，请使用[idiadatasource:: Loaddatafromistream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)方法。

## <a name="example"></a>示例

```C++
HRESULT hr = pSource->loadDataFromPdb( L"myprog.pdb" );
if (FAILED(hr))
{
    // report error
}
```

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
