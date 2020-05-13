---
title: CvIsEnabled 函数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvIsEnabledEx
- cvmarkers/CvIsEnabled
helpviewer_keywords:
- CvIsEnabled method
- CvIsEnabledEx method
ms.assetid: 2e4fea6d-758d-4150-8744-6102a1d58c1c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 92763e352d04d5aa3e88a68bad7adfcd05897027
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62945409"
---
# <a name="cvisenabled-function"></a>CvIsEnabled 函数
确定是否有任何会话启用了指定的 ETW 提供程序。

## <a name="syntax"></a>语法

```C
HRESULT CvIsEnabled(
   _In_ PCV_PROVIDER pProvider
);
HRESULT CvIsEnabledEx(
   _In_ PCV_PROVIDER pProvider,
   _In_ CV_IMPORTANCE level,
   _In_ int category
);
```

#### <a name="parameters"></a>参数
 `category` 类别。

 `level` 重要性级别。

 `pProvider` 有效的提供程序对象。 不能为 NULL。

## <a name="return-value"></a>返回值
 如果提供程序当前已启用，则返回 S_OK。 如果提供程序当前已禁用，则返回 S_FALSE。 出现任何错误时返回错误代码。 使用 FAILED 宏检查错误条件，然后检查 S_OK/S_FALSE。

## <a name="requirements"></a>要求
 **Header:** cvmarkers.h 

## <a name="see-also"></a>请参阅
- [C++ 库参考](../profiling/cpp-library-reference.md)