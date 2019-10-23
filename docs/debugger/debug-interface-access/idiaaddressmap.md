---
title: IDiaAddressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap interface
ms.assetid: e6467529-508c-4328-85d7-89444ae4d1c1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7e06acf045ce1893762d5c898752dd6bc40de50a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744981"
---
# <a name="idiaaddressmap"></a>IDiaAddressMap
提供对 DIA SDK 如何计算调试对象的虚拟和相对虚拟地址的控制。

## <a name="syntax"></a>语法

```
IDiaAddressMap : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示 `IDiaAddressMap` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)|指示是否已为特定会话建立地址映射。|
|[IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)|指定是否应使用地址映射来转换符号地址。|
|[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)|指示是否启用了相对虚拟地址的计算与使用。|
|[IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)|允许客户端启用或禁用相对虚拟地址的计算。|
|[IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)|检索当前图像的对齐方式。|
|[IDiaAddressMap::put_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)|设置图像的对齐方式。|
|[IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)|设置图像标头以支持相对虚拟地址的转换。|
|[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)|提供用于支持图像布局翻译的地址映射。|

## <a name="remarks"></a>备注
 此接口提供的控件封装在提供的两个数据集中：图像标头和地址映射。 大多数客户端使用[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法查找图像的正确调试信息，并且方法通常可以发现所有必需的标头并映射数据本身。 但是，某些客户端实现专用处理和搜索数据。 此类客户端使用 `IDiaAddressMap` 接口的方法向 DIA SDK 提供搜索结果。

## <a name="notes-for-callers"></a>调用方说明
 此接口可从 DIA 会话对象中获取。 客户端调用 DIA 会话对象接口（通常为[IDiaSession](../../debugger/debug-interface-access/idiasession.md)）上的 `QueryInterface` 方法来检索 `IDiaAddressMap` 接口。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)