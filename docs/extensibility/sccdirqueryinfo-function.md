---
title: SccDirQueryInfo 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 222b5d15a1e2bcd9bd3f27a5cd0e9904642d9786
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700955"
---
# <a name="sccdirqueryinfo-function"></a>SccDirQueryInfo 函数
此函数检查当前状态的完全限定目录的列表。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccDirQueryInfo(
LPVOID  pContext,
LONG    nDirs,
LPCSTR* lpDirNames,
LPLONG  lpStatus
);
```

### <a name="parameters"></a>参数
 pContext

中源代码管理插件上下文结构。

 nDirs

中选择要查询的目录数。

 lpDirNames

中要查询的目录的完全限定路径的数组。

 lpStatus

[in，out]用于返回状态标志 (源控件插件的数组结构。有关详细信息) ，请参阅 [目录状态代码](../extensibility/directory-status-code-enumerator.md) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|查询成功。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 函数使用家族中的位掩码来填充返回数组 `SCC_DIRSTATUS` (参阅 [目录状态代码](../extensibility/directory-status-code-enumerator.md)) ，为每个指定目录输入一个条目。 状态数组由调用方分配。

 在重命名目录之前，IDE 使用此函数来通过查询该目录是否具有相应的项目来检查该目录是否受源代码管理。 如果目录不受源代码管理，IDE 可以向用户提供正确的警告。

> [!NOTE]
> 如果源代码管理插件选择不实现一个或多个状态值，则未实现的位应设置为零。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [目录状态代码](../extensibility/directory-status-code-enumerator.md)
