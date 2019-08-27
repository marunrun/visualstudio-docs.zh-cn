---
title: IDiaSourceFile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile interface
ms.assetid: 6e9be757-797f-4960-ba62-c14092620bbd
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f8876febdae25c38d7cb637092d80dcac87f2418
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190614"
---
# <a name="idiasourcefile"></a>IDiaSourceFile
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

表示一个源代码文件。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaSourceFile : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaSourceFile`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaSourceFile::get_uniqueId](../../debugger/debug-interface-access/idiasourcefile-get-uniqueid.md)|检索一个简单的整数密钥值，该值是唯一的此映像。|  
|[IDiaSourceFile::get_fileName](../../debugger/debug-interface-access/idiasourcefile-get-filename.md)|检索源文件名。|  
|[IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)|检索的校验和类型。|  
|[IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)|具有行号引用此文件中检索编译单位的枚举的器。|  
|[IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)|检索的校验和字节数。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方的说明  
 通过调用来获取此接口[idiaenumsourcefiles:: Item](../../debugger/debug-interface-access/idiaenumsourcefiles-item.md)或[idiaenumsourcefiles:: Next](../../debugger/debug-interface-access/idiaenumsourcefiles-next.md)方法。 请参阅详细信息的示例。  
  
## <a name="example"></a>示例  
 此函数显示分配给指定的表的所有源代码文件的名称。  
  
```cpp#  
void ShowSourceFiles(IDiaTable *pTable)  
{  
    CComPtr<IDiaEnumSourceFiles> pSourceFiles;  
    if ( SUCCEEDED( pTable->QueryInterface(  
                                _uuidof( IDiaEnumSourceFiles ),  
                               (void**)&pSourceFiles )  
                  )  
       )  
    {  
        CComPtr<IDiaSourceFile> pSourceFile;  
        while ( SUCCEEDED( hr = pSourceFiles->Next( 1, &pSourceFile, &celt ) ) &&  
                celt == 1 )  
        {  
            CDiaBSTR fileName;  
            if ( pSourceFile->get_fileName( &fileName) == S_OK )  
            {  
                printf( "file name: %ws\n", fileName );  
            }  
            pSourceFile = NULL;  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumSourceFiles::Item](../../debugger/debug-interface-access/idiaenumsourcefiles-item.md)   
 [IDiaEnumSourceFiles::Next](../../debugger/debug-interface-access/idiaenumsourcefiles-next.md)   
 [IDiaLineNumber::get_sourceFile](../../debugger/debug-interface-access/idialinenumber-get-sourcefile.md)   
 [IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)   
 [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)   
 [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
