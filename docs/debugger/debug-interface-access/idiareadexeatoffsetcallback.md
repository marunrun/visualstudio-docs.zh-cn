---
title: IDiaReadExeAtOffsetCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtOffsetCallback interface
ms.assetid: 3c961641-3ce3-4bc3-bd6e-a802fa3bec49
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df32012a100d36c8d288b6b988b9498ff4afd3b3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832550"
---
# <a name="idiareadexeatoffsetcallback"></a>IDiaReadExeAtOffsetCallback
允许客户端应用程序提供的按文件位置指定的可执行文件的字节数。

## <a name="syntax"></a>语法

```
IDiaReadExeAtOffsetCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDiaReadExeAtOffsetCallback`。

|方法|描述|
|------------|-----------------|
|[IDiaReadExeAtOffsetCallback::ReadExecutableAt](../../debugger/debug-interface-access/idiareadexeatoffsetcallback-readexecutableat.md)|读取指定的可执行文件从指定的偏移量开始的字节数。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口以提供到可执行文件的文件使用绝对偏移量的可执行文件的字节。 若要使用的相对虚拟地址，实现[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)接口。

## <a name="notes-for-callers"></a>调用方的说明
 此方法是由客户端应用程序实现并传递给[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法作为一种方法来读取文件。

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)