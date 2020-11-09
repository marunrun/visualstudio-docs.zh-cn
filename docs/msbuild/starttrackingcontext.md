---
title: StartTrackingContext | Microsoft Docs
description: 了解启动跟踪上下文的 MSBuild StartTrackingContext 的参数、要求和返回值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StartTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StartTrackingContext
ms.assetid: 720cd295-38e7-4974-86db-b8106b1207ba
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 13a22e3a20b69f62fe1e7d6c8e97eb80df6de1b6
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048154"
---
# <a name="starttrackingcontext"></a>StartTrackingContext

启动跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI StartTrackingContext(LPCTSTR intermediateDirectory, LPCTSTR taskName);
```

#### <a name="parameters"></a>参数

[in] `intermediateDirectory`

 存储跟踪日志的目录。

[in] `taskName`

 标识跟踪上下文。 此名称用于创建日志文件名。

## <a name="return-value"></a>返回值

 如果跟踪上下文创建完成，则返回带 SUCCEEDED 位集的 HRESULT 。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 
