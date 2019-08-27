---
title: IDiaAddressMap::get_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_addressMapEnabled method
ms.assetid: 6183dc5e-befa-4e5a-ae5a-f4aa24f3ed9e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7391010e409cc25a3151bb2abb806289c81288a1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554400"
---
# <a name="idiaaddressmapgetaddressmapenabled"></a>IDiaAddressMap::get_addressMapEnabled
指示是否已为特定会话建立映射的地址。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressMapEnabled ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out]返回`TRUE`如果启用了该地址的映射。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 可执行文件后处理器有时会更新可执行文件。 DIA 包含一种机制，以支持新布局的符号的转换。

 客户端应用程序可以设置地址映射为特定会话通过获取[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)从接口[IDiaSession](../../debugger/debug-interface-access/idiasession.md)接口并调用[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)方法后调用[idiaaddressmap:: Put_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)方法。 `get_addressMapEnabled`方法返回调用的结果`put_addressMapEnabled`方法。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)