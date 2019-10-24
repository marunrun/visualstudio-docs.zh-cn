---
title: IDiaAddressMap::put_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5fe5589b667054ee75e3b01743553a2d60bef92
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745069"
---
# <a name="idiaaddressmapput_addressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
指定是否应使用地址映射来转换符号地址。

## <a name="syntax"></a>语法

```C++
HRESULT put_addressMapEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

中设置为 "`TRUE`" 以启用符号翻译，或将 `FALSE` 设置为 "禁用"。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 可执行的后处理器有时会更新可执行文件。 DIA 包含一种机制，用于支持将符号转换为新的布局。

 加载 PDB 文件时，存储在该文件中的地址映射已启用。 然而，在某些情况下，客户端应用程序可能需要通过调用[IDiaAddressMap：： set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)方法来提供其自己的地址映射。 如果 `set_addressMap` 方法成功，则客户端应用程序必须使用 `TRUE` 的 `NewVal` 参数调用 `put_addressMapEnabled` 方法才能使用该地址映射。

 使用对[IDiaAddressMap：： get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)方法的调用，可以检索正在启用的地址映射的当前状态。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)