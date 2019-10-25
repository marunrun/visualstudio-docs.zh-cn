---
title: IDiaReadExeAtRVACallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback interface
ms.assetid: b2892513-3952-4f99-9b98-60cb9b1fdc91
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2aee44ff3acc1d7423e19de8fd64be0e46d8e372
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742808"
---
# <a name="idiareadexeatrvacallback"></a>IDiaReadExeAtRVACallback
使客户端应用程序能够提供相对虚拟地址指定的可执行文件的字节数。

## <a name="syntax"></a>语法

```
IDiaReadExeAtRVACallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示 `IDiaReadExeAtRVACallback` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaReadExeAtRVACallback::ReadExecutableAtRVA](../../debugger/debug-interface-access/idiareadexeatrvacallback-readexecutableatrva.md)|从可执行文件中读取指定的相对虚拟地址（RVA）开始的指定字节数。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，以便使用相对虚拟地址将可执行文件的字节提供给可执行文件的文件。 若要使用绝对文件偏移，实现[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)接口。

## <a name="notes-for-callers"></a>调用方说明
 此方法由客户端应用程序实现，并作为读取文件的替代方法传递给[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)