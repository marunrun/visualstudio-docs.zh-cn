---
title: IDiaDataSource：： loadDataForExe |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataForExe method
ms.assetid: d94a1068-f53f-44b5-b6fb-00dec361a7f2
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 623cdd74b086a46bc52c0f0534953ae6e11168ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547372"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

打开并准备与 .exe/.dll 文件关联的调试数据。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
 中 `IUnknown` 支持调试回调接口的对象的接口，例如 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)、 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)、 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)和/或 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) 接口。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了此方法的一些可能的错误代码。  
  
|值|说明|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|无法打开该文件，或者该文件的格式无效。|  
|E_PDB_FORMAT|尝试访问具有过时格式的文件。|  
|E_PDB_INVALID_SIG|签名不匹配。|  
|E_PDB_INVALID_AGE|Age 不匹配。|  
|E_INVALIDARG|参数无效。|  
|E_UNEXPECTED|数据源已准备就绪。|  
  
## <a name="remarks"></a>备注  
 .Exe/.dll 文件的 debug 标头将关联的调试数据位置命名为。  
  
 此方法读取调试标头，然后搜索并准备调试数据。 可以选择通过回调报告和控制搜索进度。 例如，当方法查找并处理调试目录时，将调用 [IDiaLoadCallback：： NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md) `IDiaDataSource::loadDataForExe` 。  
  
 当无法通过标准文件 i/o 直接访问该文件时， [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) 和 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) 接口允许客户端应用程序提供用于从可执行文件中读取数据的替代方法。  
  
 若要加载 .pdb 文件而不进行验证，请使用 [IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) 方法。  
  
 若要根据特定条件验证 .pdb 文件，请使用 [IDiaDataSource：： loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) 方法。  
  
 若要直接从内存加载 .pdb 文件，请使用 [IDiaDataSource：： loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) 方法。  
  
## <a name="example"></a>示例  
  
```cpp#  
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
  
## <a name="see-also"></a>另请参阅  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)   
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)   
 [IDiaLoadCallback：： NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)   
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)   
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)   
 [IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource：： loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
