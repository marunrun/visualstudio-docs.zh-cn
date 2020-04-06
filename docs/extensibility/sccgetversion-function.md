---
title: SccGet 版本功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700680"
---
# <a name="sccgetversion-function"></a>SccGetVersion 函数
此功能获取源代码管理插件插件支持的源代码管理插件 API 的版本号。

## <a name="syntax"></a>语法

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 包含`LONG`受支持的源代码管理插件 API 的版本号的数据类型：

|WORD|描述|
|----------|-----------------|
|希WORD|主版本|
|洛沃|次版本|

## <a name="remarks"></a>备注
 例如，如果源代码管理插件支持源代码管理插件 API 的版本 1.3，则此功能将返回 0x0103。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
