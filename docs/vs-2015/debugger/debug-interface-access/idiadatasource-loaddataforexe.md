---
title: 'Idiadatasource:: Loaddataforexe |Microsoft Docs'
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62547372"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将打开并准备与.exe/.dll 文件相关联的调试数据。  
  
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
 [in].Exe 或.dll 文件的路径。  
  
 SearchPath  
 [in]要搜索的调试数据的备用路径。  
  
 pCallback  
 [in]`IUnknown`接口的对象的支持调试回调接口，如[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)， [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)，则[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)，和/或[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了一些可能的错误代码为此方法。  
  
|“值”|描述|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|无法打开该文件，或该文件具有无效的格式。|  
|E_PDB_FORMAT|尝试访问具有过时的格式的文件。|  
|E_PDB_INVALID_SIG|签名不匹配。|  
|E_PDB_INVALID_AGE|年龄不匹配。|  
|E_INVALIDARG|参数无效。|  
|E_UNEXPECTED|已准备好数据源。|  
  
## <a name="remarks"></a>备注  
 .Exe/.dll 文件的调试标头名称关联的调试数据位置。  
  
 此方法读取调试标头，然后搜索并准备调试数据。 搜索的进度可能，（可选） 报告和控制通过回调。 例如， [idialoadcallback:: Notifydebugdir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)时调用`IDiaDataSource::loadDataForExe`方法查找并处理调试目录。  
  
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)并[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)接口允许客户端应用程序提供替代方法，用于从可执行文件中读取数据文件时文件不能直接通过标准文件 I/O 访问。  
  
 若要加载的.pdb 文件而不进行验证，请使用[idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)方法。  
  
 若要验证.pdb 文件是否符合特定条件，请使用[idiadatasource:: Loadandvalidatedatafrompdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)方法。  
  
 若要直接从内存加载的.pdb 文件，请使用[idiadatasource:: Loaddatafromistream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)方法。  
  
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
  
## <a name="see-also"></a>请参阅  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)   
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)   
 [IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)   
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)   
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)   
 [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
