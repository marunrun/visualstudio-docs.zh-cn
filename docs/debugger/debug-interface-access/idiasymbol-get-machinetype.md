---
title: 'Idiasymbol:: Get_machinetype |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_machineType method
ms.assetid: 30870b10-6f32-45c6-a0d7-020dea707710
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eef0507ccb7036748f5c9d36c9de521a17860a39
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67032723"
---
# <a name="idiasymbolgetmachinetype"></a>IDiaSymbol::get_machineType
检索目标 CPU 的类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_machineType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个值从[IMAGE_FILE_MACHINE_ 常量](/windows/desktop/SysInfo/image-file-machine-constants)，它指定目标 CPU 类型。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IMAGE_FILE_MACHINE_ 常量](/windows/desktop/SysInfo/image-file-machine-constants) 
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)