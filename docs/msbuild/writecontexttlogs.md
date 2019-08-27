---
title: WriteContextTLogs | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- WriteContextTLogs
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- WriteContextTLogs
ms.assetid: ffc6c7be-3f22-4624-9ffc-0122fe72b6ec
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 722d8c42786a7aaa2daae293b96f7926abcc90ca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62777839"
---
# <a name="writecontexttlogs"></a>WriteContextTLogs
写入当前上下文的日志文件。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI WriteContextTLogs(LPCTSTR intermediateDirectory, LPCTSTR tlogRootName);
```

#### <a name="parameters"></a>参数
[in] `intermediateDirectory`

 存储跟踪日志的目录。

[in] `tlogRootName`

 日志文件名的根名称。

## <a name="return-value"></a>返回值
 如果跟踪上下文创建完成，则返回带 SUCCEEDED 位集的 HRESULT   。

## <a name="requirements"></a>要求
 **标头：** FileTracker.h 

## <a name="see-also"></a>请参阅
- [WriteAllTLogs](../msbuild/writealltlogs.md)