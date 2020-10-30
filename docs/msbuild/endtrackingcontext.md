---
title: EndTrackingContext | Microsoft Docs
description: 了解使用 MSBuild EndTrackingContext 结束当前跟踪上下文的语法、返回值和要求。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: da1ef921106732a7787f68a979bc88f3ac012b6d
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436674"
---
# <a name="endtrackingcontext"></a>EndTrackingContext

结束当前跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI EndTrackingContext();
```

## <a name="return-value"></a>返回值

如果跟踪上下文结束，返回带 SUCCEEDED 位组的 HRESULT。

## <a name="requirements"></a>要求

<bpt id="p1">**</bpt>Header:<ept id="p1">**</ept> <bpt id="p2">*</bpt>FileTracker.h<ept id="p2">*</ept>

## <a name="see-also"></a>另请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)
