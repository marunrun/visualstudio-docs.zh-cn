---
title: StopTrackingAndCleanup | Microsoft Docs
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 56f4fb82ab0e9792cadbeeea05499744e4c8ce46
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939018"
---
# <a name="stoptrackingandcleanup"></a>StopTrackingAndCleanup
停止所有跟踪，并释放跟踪会话使用的任何内存。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI StopTrackingAndCleanup(void);
```

## <a name="return-value"></a>返回值
 如果跟踪停止，则返回带 SUCCEEDED 位集的 HRESULT   。

## <a name="requirements"></a>要求
 **标头：** FileTracker.h 

## <a name="see-also"></a>请参阅
- [StartTrackingContext](../msbuild/starttrackingcontext.md)