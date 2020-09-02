---
title: SccGetVersion 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a563a7d1d65dc4c6564abd4e337242eea1aa9924
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700680"
---
# <a name="sccgetversion-function"></a>SccGetVersion 函数
此函数获取源代码管理插件支持的源代码管理插件 API 版本号。

## <a name="syntax"></a>语法

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 一个 `LONG` 数据类型，它包含受支持的源代码管理插件 API 的版本号：

|WORD|说明|
|----------|-----------------|
|HIWORD|主版本|
|LOWORD|次要版本|

## <a name="remarks"></a>备注
 例如，如果源代码管理插件支持源代码管理插件 API 版本1.3，则此函数将返回0x0103。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
