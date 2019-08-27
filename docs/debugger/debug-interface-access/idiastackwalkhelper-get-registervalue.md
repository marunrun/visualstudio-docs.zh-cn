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
ms.openlocfilehash: 275941aaf3a1eb2cab6554b18c6d9aa66605121a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831827"
---
# <a name="idiastackwalkhelpergetregistervalue"></a>IDiaStackWalkHelper::get_registerValue
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

[in]中的值[CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)枚举，它指定其注册以获取的值。

 `pRetVal`

[out]返回注册的当前值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 虽然的大，但`pRetVal`参数，实现应存储仅注册通常存放。 例如，一个 8 位寄存器保存仅中的最小 8 位的给定值。 此 8 位值扩展到 64 位时此方法返回。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)