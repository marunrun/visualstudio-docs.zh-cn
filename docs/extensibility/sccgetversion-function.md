---
title: SccGetVersion 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1ad37e30cfcf913477044e67baaa65dc3af5b9d3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353624"
---
# <a name="sccgetversion-function"></a>SccGetVersion 函数
此函数获取源代码管理插件支持的源控制插件 API 的版本号。

## <a name="syntax"></a>语法

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 一个`LONG`包含版本号的受支持的源控制插件 API 的数据类型：

|WORD|描述|
|----------|-----------------|
|HIWORD|主要版本|
|使用 LOWORD|次要版本|

## <a name="remarks"></a>备注
 例如，如果源代码管理插件支持的源控制插件 API 版本 1.3，此函数将返回 0x0103。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)