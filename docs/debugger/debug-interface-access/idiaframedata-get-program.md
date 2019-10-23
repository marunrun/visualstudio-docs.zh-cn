---
title: IDiaFrameData::get_program | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 135f2b0a042dd74b573a0746831a48fb27e7c2a9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743516"
---
# <a name="idiaframedataget_program"></a>IDiaFrameData::get_program
检索用于在调用当前函数之前计算注册集的程序字符串。

## <a name="syntax"></a>语法

```C++
HRESULT get_program ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回程序字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 程序字符串是一系列用于建立序言的宏。 例如，典型的堆栈帧可能使用程序字符串 `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="`。 格式为反转波兰表示法，其中运算符遵循操作数。 `T0` 表示堆栈上的临时变量。 此示例执行以下步骤：

1. 将 register `ebp` 的内容移动到 `T0` 中。

2. 将 `4` 添加到 `T0` 中的值以生成地址，从该地址获取该值，并将该值存储在 register `eip` 中。

3. 获取 `T0` 中存储的地址的值，并将该值存储在 register `ebp` 中。

4. 将 `8` 添加到 `T0` 中的值，并将该值存储在 register `esp` 中。

   请注意，程序字符串特定于 CPU，并且针对当前堆栈帧所表示的函数设置的调用约定。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)