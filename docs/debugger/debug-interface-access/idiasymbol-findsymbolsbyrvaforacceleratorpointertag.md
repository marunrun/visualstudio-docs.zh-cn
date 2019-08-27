---
title: IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 024ccd78-5867-4ca7-bc26-548758e9ac53
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 673ca8137244fed933df0be3fa0221115951a9c1
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62838992"
---
# <a name="idiasymbolfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag
提供相应的标记值，此方法返回在指定的相对虚拟地址此存根 （stub） 函数中包含的符号的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag (
   DWORD             tagValue,
   DWORD             rva,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>参数
 `tagValue`

[in]为其找到 pointee 符号记录指针标记值。

 `rva`

[in]用于筛选的符号与 pointee 变量和指定的标记值相对应的 rva。

 `ppResult`

[out]一个指向`IDiaEnumSymbols`使用结果初始化接口指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="remarks"></a>备注
 调用此方法仅对`IDiaSymbol`对应于加速器存根 （stub） 函数的接口。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)