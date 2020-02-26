---
title: ResumeTracking | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- ResumeTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- ResumeTracking
ms.assetid: d637e019-7c50-4b0a-812e-bc822001e697
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6bb4663013a73d88ed7c2118816007705834162c
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578448"
---
# <a name="resumetracking"></a>ResumeTracking
在当前上下文中恢复跟踪。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI ResumeTracking();
```

## <a name="return-value"></a>返回值
 如果跟踪恢复，则返回带 SUCCEEDED 位集的 HRESULT   。 如果因为上下文不可用而无法恢复跟踪，将返回“E_FAIL”  。

## <a name="requirements"></a>要求
 **标头：** FileTracker.h 

## <a name="see-also"></a>请参阅
- [SuspendTracking](../msbuild/suspendtracking.md)