---
title: IDiaSymbol::get_numberOfAcceleratorPointerTags | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 1886e3ec-b227-4187-8d93-c5144b4b77ae
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 47c5827348c7b7cb450017a0e6176d71f555c841
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739698"
---
# <a name="idiasymbolget_numberofacceleratorpointertags"></a>IDiaSymbol::get_numberOfAcceleratorPointerTags
返回C++ AMP 存根函数中的快捷键指针标记数。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfAcceleratorPointerTags(
   DWORD* count);
```

#### <a name="parameters"></a>参数
 `count`

弄一个指向 `DWORD` 的指针，该指针包含C++ AMP 存根函数中的快捷键指针标记的数目。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="remarks"></a>备注
 此方法在与C++ AMP 快捷键存根函数相对应的 `IDiaSymbol` 接口上调用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)