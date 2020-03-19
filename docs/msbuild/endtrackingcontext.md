---
title: EndTrackingContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- EndTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- EndTrackingContext
ms.assetid: c2c5d794-8dc8-4594-8717-70dc79a0e75d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf982200b8e65e404325bdbd189ff3b0f2daebac
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634235"
---
# <a name="endtrackingcontext"></a>EndTrackingContext

结束当前跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI EndTrackingContext();
```

## <a name="return-value"></a>返回值

如果跟踪上下文结束，返回带 SUCCEEDED  位组的 HRESULT  。

## <a name="requirements"></a>要求

**标头：** FileTracker.h 

## <a name="see-also"></a>请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)
