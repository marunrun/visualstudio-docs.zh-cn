---
title: IDiaDataSource | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource interface
ms.assetid: 6260ac76-4f9d-4144-ba22-32f8620b32c2
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a02eb9048c0e9338e6300fc63666af4db535b3ac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198589"
---
# <a name="idiadatasource"></a>IDiaDataSource
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

启动对调试符号源的访问。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaDataSource : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDiaDataSource` 。  
  
|方法|说明|  
|------------|-----------------|  
|[IDiaDataSource::get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md)|检索最后一个加载错误的文件名。|  
|[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)|打开并准备程序数据库 ( .pdb) 文件作为调试数据源。|  
|[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)|打开并验证程序数据库 ( .pdb) 文件是否与提供的签名信息匹配;准备用作调试数据源的 .pdb 文件。|  
|[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)|打开并准备与 .exe/.dll 文件关联的调试数据。|  
|[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)|准备 ( 程序数据库中存储的调试数据，) 通过内存中数据流访问的文件。|  
|[IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)|为查询符号打开一个会话。|  
  
## <a name="remarks"></a>备注  
 对接口的其中一个 load 方法的调用 `IDiaDataSource` 会打开符号源。 对 [IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) 方法的成功调用将返回支持查询数据源的 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) 接口。 如果 load 方法返回与文件相关的错误，则 [IDiaDataSource：： get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md) 方法返回值将包含与该错误关联的文件名。  
  
## <a name="notes-for-callers"></a>调用方说明  
 此接口是通过调用 `CoCreateInstance` 具有类标识符 `CLSID_DiaSource` 和的接口 ID 的函数获取的 `IID_IDiaDataSource` 。 该示例演示如何获取此接口。  
  
## <a name="example"></a>示例  
  
```cpp#  
  
      IDiaDataSource* pSource;  
HRESULT hr = CoCreateInstance(CLSID_DiaSource,  
                              NULL,  
                              CLSCTX_INPROC_SERVER,  
                              IID_IDiaDataSource,  
                              (void**) &pSource);  
if (FAILED(hr))  
{  
    // Report error and exit  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： Dia2  
  
 库： diaguids  
  
 DLL： msdia80.dll  
  
## <a name="see-also"></a>另请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
