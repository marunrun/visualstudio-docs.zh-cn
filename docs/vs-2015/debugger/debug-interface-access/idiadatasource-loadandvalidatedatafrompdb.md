---
title: IDiaDataSource：： loadAndValidateDataFromPdb |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadAndValidateDataFromPdb method
ms.assetid: d66712dd-6c24-4192-919a-cce262066f0e
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f19a910af45ed70ae74c72441890ecae6c81d2a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198622"
---
# <a name="idiadatasourceloadandvalidatedatafrompdb"></a>IDiaDataSource::loadAndValidateDataFromPdb
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

打开并验证程序数据库 ( .pdb) 文件是否与提供的签名信息匹配，并将 .pdb 文件准备为调试数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT loadAndValidateDataFromPdb (   
   LPCOLESTR pdbPath,  
   GUID*     pcsig70,  
   DWORD     sig,  
   DWORD     age  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdbPath`  
 中.Pdb 文件的路径。  
  
 `pcsig70`  
 中要根据 .pdb 文件签名进行验证的 GUID 签名。 只有 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 和更高版本中的 .pdb 文件具有 GUID 签名。  
  
 `sig`  
 中要针对 .pdb 文件签名进行验证的32位签名。  
  
 `age`  
 中要验证的 Age 值。 Age 并不一定对应于任何已知的时间值，它用于确定 .pdb 文件是否与相应的 .exe 文件不同步。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了此方法的可能的返回值。  
  
|值|说明|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|无法打开该文件，或者该文件的格式无效。|  
|E_PDB_FORMAT|尝试访问具有过时格式的文件。|  
|E_PDB_INVALID_SIG|签名不匹配。|  
|E_PDB_INVALID_AGE|Age 不匹配。|  
|E_INVALIDARG|参数无效。|  
|E_UNEXPECTED|数据源已准备就绪。|  
  
## <a name="remarks"></a>备注  
 .Pdb 文件同时包含签名值和 age 值。 这些值是在 .exe 或 .dll 文件中复制的，后者与 .pdb 文件相匹配。 准备数据源之前，此方法会验证命名 .pdb 文件的签名和 age 是否与提供的值匹配。  
  
 若要加载 .pdb 文件而不进行验证，请使用 [IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) 方法。  
  
 若要通过回调机制) 访问数据加载过程 (，请使用 [IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。  
  
 若要直接从内存加载 .pdb 文件，请使用 [IDiaDataSource：： loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) 方法。  
  
## <a name="example"></a>示例  
  
```cpp#  
IDiaDataSource* pSource;  // Previously created data source.  
DEFINE_GUID(expectedGUIDSignature,0x1234,0x5678,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08);  
DWORD expectedFileSignature = 0x12345678;  
DWORD expectedAge           = 128;  
  
HRESULT hr;  
hr = pSource->loadAndValidateDataFromPdb( L"yprog.pdb",  
                                          &expectedGUIDSignature,  
                                          expectedFileSignature,  
                                          expectedAge);  
if (FAILED(hr))  
{  
    // Report an error  
}  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
