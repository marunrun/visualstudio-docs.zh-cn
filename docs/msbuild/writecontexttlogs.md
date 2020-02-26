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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5c0793cc6d9f11cd1074c5cd0091687b154c069
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579456"
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