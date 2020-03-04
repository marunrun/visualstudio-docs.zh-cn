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
ms.openlocfilehash: 950c6a07a46f7f4b970912e576257a577021367e
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77632000"
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