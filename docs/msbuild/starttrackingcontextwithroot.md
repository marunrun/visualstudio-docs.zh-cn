---
title: StartTrackingContextWithRoot | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StartTrackingContextWithRoot
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StartTrackingContextWithRoot
ms.assetid: f6ef2b76-8035-4a14-8195-aa221c46ef48
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68d585361b9797bf1df9c8b0b31f8a089e9de025
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632090"
---
# <a name="starttrackingcontextwithroot"></a>StartTrackingContextWithRoot

使用指定根标记的响应文件启动跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI StartTrackingContextWithRoot(LPCTSTR intermediateDirectory, LPCTSTR taskName, LPCTSTR rootMarkerResponseFile);
```

#### <a name="parameters"></a>参数

[in] `intermediateDirectory`

 存储跟踪日志的目录。

[in] `taskName`

 标识跟踪上下文。 此名称用于创建日志文件名。

[in] `rootMarkerResponseFile`

 包含根标记的响应文件的路径名称。 根名称用于将上下文的所有跟踪聚集在一起。

## <a name="return-value"></a>返回值

 如果跟踪上下文创建完成，则返回带 SUCCEEDED 位集的 HRESULT   。

## <a name="requirements"></a>要求

 **标头：** FileTracker.h 

## <a name="see-also"></a>请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)