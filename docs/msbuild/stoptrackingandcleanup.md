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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee30bf031761fa7920dadad04d8f17a1bcc0b3a2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631986"
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