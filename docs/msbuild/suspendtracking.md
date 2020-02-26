---
title: SuspendTracking | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- SuspendTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- SuspendTracking
ms.assetid: f5e06e5a-8083-444c-99c1-07ba834226b5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d48c29b9dcca477c5a5470c443be08d5060b413d
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578109"
---
# <a name="suspendtracking"></a>SuspendTracking
在当前上下文中暂停跟踪。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI SuspendTracking(void);
```

## <a name="return-value"></a>返回值
 如果跟踪暂停，则返回带 SUCCEEDED 位集的 HRESULT   。

## <a name="requirements"></a>要求
 **标头：** FileTracker.h 

## <a name="see-also"></a>请参阅
- [ResumeTracking](../msbuild/resumetracking.md)