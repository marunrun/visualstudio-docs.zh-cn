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
ms.openlocfilehash: 36b48529f82a908ea765151561a71c58cd2c7bc5
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578415"
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