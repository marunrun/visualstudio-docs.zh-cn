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
ms.openlocfilehash: 7db8b6a115acdafeca2e7e0adbe11be97834cd6d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742960"
---
# <a name="idialoadcallback2"></a>IDiaLoadCallback2
接收来自 DIA 符号定位过程的回调，以允许对查找过程施加限制。

## <a name="syntax"></a>语法

```
IDiaLoadCallback2 : IDiaLoadCallback
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)接口中的方法之外，此接口还公开以下方法：

|方法|描述|
|------------|-----------------|
|[IDiaLoadCallback2::RestrictOriginalPathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictoriginalpathaccess.md)|确定是否在原始调试目录中查找 .pdb 文件。|
|[IDiaLoadCallback2::RestrictReferencePathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictreferencepathaccess.md)|确定是否允许在 .exe 文件所在的路径中查找 .pdb 文件。|
|[IDiaLoadCallback2::RestrictDBGAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictdbgaccess.md)|确定是否允许从 dbg 文件查找调试信息。|
|[IDiaLoadCallback2::RestrictSystemRootAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictsystemrootaccess.md)|确定是否允许在系统根目录中搜索 .pdb 文件。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，并在对[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法的调用中提供对此接口的引用。 还应记得实现[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)接口中的所有方法。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)