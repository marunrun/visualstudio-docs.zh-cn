---
title: IDiaStackWalkHelper::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bfb3e219012effe47a2352f7c22c6cf51b4617f9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741407"
---
# <a name="idiastackwalkhelperget_registervalue"></a>IDiaStackWalkHelper::get_registerValue
检索寄存器的值。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerValue ( 
   DWORD      index,
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `index`

中[CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)枚举中的一个值，该值指定要从哪个寄存器获取值。

 `pRetVal`

弄返回寄存器的当前值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 尽管 `pRetVal` 参数的大小，实现应只存储寄存器通常保存的内容。 例如，8位寄存器只包含给定值的最低8位。 从此方法返回时，此8位值将扩展为64位。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)