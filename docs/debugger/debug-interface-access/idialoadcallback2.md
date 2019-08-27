---
title: IDiaLoadCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2 interface
ms.assetid: 9a44277d-cbed-4811-9bad-5a2aa0f09323
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: daf0b48aca06b404824059030052223a8545a6b0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839701"
---
# <a name="idialoadcallback2"></a>IDiaLoadCallback2
接收来自 DIA 符号查找过程，从而限制强加于查找过程的回调。

## <a name="syntax"></a>语法

```
IDiaLoadCallback2 : IDiaLoadCallback
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了中的方法[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)接口，此接口公开以下方法：

|方法|描述|
|------------|-----------------|
|[IDiaLoadCallback2::RestrictOriginalPathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictoriginalpathaccess.md)|确定如果查找原始的调试目录中的.pdb 文件。|
|[IDiaLoadCallback2::RestrictReferencePathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictreferencepathaccess.md)|确定是否在.exe 文件所在位置的路径中允许查找.pdb 文件。|
|[IDiaLoadCallback2::RestrictDBGAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictdbgaccess.md)|确定从.dbg 文件是否允许查找调试信息。|
|[IDiaLoadCallback2::RestrictSystemRootAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictsystemrootaccess.md)|确定是否在系统根目录下允许搜索.pdb 文件。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，并提供对的调用中对它的引用[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。 请记住要实现的方法中的所有[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)也接口。

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)