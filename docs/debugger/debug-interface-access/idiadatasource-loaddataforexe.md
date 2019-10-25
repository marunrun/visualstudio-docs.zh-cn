---
title: IDiaDataSource：： loadDataForExe |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataForExe method
ms.assetid: d94a1068-f53f-44b5-b6fb-00dec361a7f2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7a86abb00ebc090c37f03a5533376ae0b9c3e8ae
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744958"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
打开并准备与 .exe/.dll 文件关联的调试数据。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataForExe (
   LPCOLESTR executable,
   LPCOLESTR searchPath,
   IUnknown* pCallback
);
```

#### <a name="parameters"></a>参数
可执行文件

中.Exe 或 .dll 文件的路径。

SearchPath

中用于搜索调试数据的备用路径。

pCallback

中支持调试回调接口的对象的 `IUnknown` 接口，例如[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)、 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)、 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)和/或[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)接口。

## <a name="return-value"></a>返回值
如果成功，将返回 `S_OK`;否则，将返回错误代码。 下表显示了此方法的一些可能的错误代码。

|“值”|描述|
|-----------|-----------------|
|E_PDB_NOT_FOUND|无法打开该文件，或者该文件的格式无效。|
|E_PDB_FORMAT|尝试访问具有过时格式的文件。|
|E_PDB_INVALID_SIG|签名不匹配。|
|E_PDB_INVALID_AGE|Age 不匹配。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|数据源已准备就绪。|

## <a name="remarks"></a>备注
.Exe/.dll 文件的 debug 标头将关联的调试数据位置命名为。

此方法读取调试标头，然后搜索并准备调试数据。 可以选择通过回调报告和控制搜索进度。 例如，当 `IDiaDataSource::loadDataForExe` 方法查找并处理调试目录时，将调用[IDiaLoadCallback：： NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md) 。

使用[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)和[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)接口，客户端应用程序可以提供其他方法，以便在无法通过标准直接访问该文件时从可执行文件中读取数据。文件 i/o。

若要加载 .pdb 文件而不进行验证，请使用[IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)方法。

若要根据特定条件验证 .pdb 文件，请使用[IDiaDataSource：： loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)方法。

若要直接从内存加载 .pdb 文件，请使用[IDiaDataSource：： loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)方法。

## <a name="example"></a>示例

```C++
class MyCallBack: public IDiaLoadCallback
{
...
};
MyCallBack callback;
...
HRESULT hr = pSource->loadDataForExe( L"myprog.exe", L".\debug", (IUnknown*)&callback);
if (FAILED(hr))
{
    // Report error
}
```

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
