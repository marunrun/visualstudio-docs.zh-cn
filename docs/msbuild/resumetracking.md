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
ms.openlocfilehash: 248bb5e5e01b8209f826478e90b2c60b70922987
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77632493"
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