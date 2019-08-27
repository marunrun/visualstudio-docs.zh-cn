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
ms.openlocfilehash: c1724ee3e81ac00ed048f323105842361ec22bc7
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62827289"
---
# <a name="idiasymbolgetacceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
返回对应的所有快捷键指针标记值C++AMP 快捷键存根 （stub） 函数。

## <a name="syntax"></a>语法

```C++
HRESULT get_acceleratorPointerTags(
   DWORD          cnt,
   DWORD*         pcnt,
   DWORD*         pPointerTags);
```

#### <a name="parameters"></a>参数
 `cnt`

[in]输出数组的大小`pPointerTags`。

 `pcnt`

[out]Accelerator 指针中的标记的计数C++AMP 快捷键存根 （stub） 函数。

 `pPointerTags`

[out]一个`DWORD`中的加速器指针标记值填充数组指针C++AMP 快捷键存根 （stub） 函数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="remarks"></a>备注
 在调用此方法`IDiaSymbol`接口对应于C++AMP 快捷键存根 （stub） 函数。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)