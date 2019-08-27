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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0e2ff32a4eb2218a8b3d09188c787156e484147f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996696"
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