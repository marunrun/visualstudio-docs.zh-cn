---
title: IDiaSymbol::get_acceleratorPointerTags | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 30e13cee-e511-49ec-affd-99b0097071b2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f36b4bf9fdd362f4941e33745d59d481a473c607
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741119"
---
# <a name="idiasymbolget_acceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
返回与C++ AMP 加速器存根函数相对应的所有快捷键指针标记值。

## <a name="syntax"></a>语法

```C++
HRESULT get_acceleratorPointerTags(
   DWORD          cnt,
   DWORD*         pcnt,
   DWORD*         pPointerTags);
```

#### <a name="parameters"></a>参数
 `cnt`

中@No__t_0 输出数组的大小。

 `pcnt`

弄C++ AMP 加速器存根函数中的快捷键指针标记的计数。

 `pPointerTags`

弄一个 `DWORD` 数组指针，该指针使用C++ AMP 加速器存根函数中的快捷键指针标记值进行填充。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="remarks"></a>备注
 此方法在与C++ AMP 快捷键存根函数相对应的 `IDiaSymbol` 接口上调用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)