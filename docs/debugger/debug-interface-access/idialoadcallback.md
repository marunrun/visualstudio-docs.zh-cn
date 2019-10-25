---
title: IDiaLoadCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback interface
ms.assetid: 2f18c64c-2cf0-43fc-a447-21e82702ca2a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ca58a206fec15bb8a9ae7f68a278a4530be47d8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743043"
---
# <a name="idialoadcallback"></a>IDiaLoadCallback
接收来自 DIA 符号定位过程的回调，从而使用户界面能够报告位置尝试的进度。

## <a name="syntax"></a>语法

```
IDiaLoadCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口公开以下方法：

|方法|描述|
|------------|-----------------|
|[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)|在 .exe 文件中找到调试目录时调用。|
|[IDiaLoadCallback::NotifyOpenDBG](../../debugger/debug-interface-access/idialoadcallback-notifyopendbg.md)|在已打开候选的 dbg 文件时调用。|
|[IDiaLoadCallback::NotifyOpenPDB](../../debugger/debug-interface-access/idialoadcallback-notifyopenpdb.md)|在已打开候选 .pdb 文件时调用。|
|[IDiaLoadCallback::RestrictRegistryAccess](../../debugger/debug-interface-access/idialoadcallback-restrictregistryaccess.md)|确定是否可以使用注册表查询来查找符号搜索路径。|
|[IDiaLoadCallback::RestrictSymbolServerAccess](../../debugger/debug-interface-access/idialoadcallback-restrictsymbolserveraccess.md)|确定是否允许访问符号服务器来解析符号。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，并在对[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法的调用中提供对此接口的引用。

 有关可对加载过程施加的其他限制，请参阅[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)接口。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)