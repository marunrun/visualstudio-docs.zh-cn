---
title: StopTrackingAndCleanup | Microsoft Docs
description: 了解 MSBuild 如何使用 StopTrackingAndCleanup 停止所有跟踪，并释放跟踪会话使用的任何内存。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StopTrackingAndCleanup
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StopTrackingAndCleanup
ms.assetid: 9f8c5994-2dfc-43c3-a5fb-89b2f8990429
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 05aec8bc85ac392670469da8073da02888b2f063
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048102"
---
# <a name="stoptrackingandcleanup"></a>StopTrackingAndCleanup

停止所有跟踪，并释放跟踪会话使用的任何内存。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI StopTrackingAndCleanup(void);
```

## <a name="return-value"></a>返回值

 如果跟踪停止，则返回带 SUCCEEDED 位集的 HRESULT。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)