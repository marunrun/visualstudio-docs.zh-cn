---
title: SccQueryInfo 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5807eb6b695e140350696436a8bba351687f4a24
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720833"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 函数
此函数获取源代码管理下所选文件集的状态信息。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccQueryInfo(
   LPVOID  pvContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPLONG  lpStatus
);
```

#### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 n

中在 `lpFileNames` 数组中指定的文件数和 `lpStatus` 数组的长度。

 lpFileNames

中要查询的文件的名称数组。

 lpStatus

[in，out]一个数组，其中的源代码管理插件为每个文件返回状态标志。 有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|查询成功。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由网络或争用问题引起的。 建议重试。|
|SCC_E_PROJNOTOPEN|未在源代码管理下打开该项目。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 如果 `lpFileName` 为空字符串，则当前没有要更新的状态信息。 否则，它是其状态信息可能已更改的文件的完整路径名称。

 返回数组可以是 `SCC_STATUS_xxxx` 位位掩码。 有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)。 源代码管理系统可能不支持所有位类型。 例如，如果未提供 `SCC_STATUS_OUTOFDATE`，则仅设置位。

 使用此函数签出文件时，请注意以下 `MSSCCI` 状态要求：

- 当当前用户签出文件时，将设置 `SCC_STATUS_OUTBYUSER`。

- 除非设置 `SCC_STATUS_OUTBYUSER`，否则不能设置 `SCC_STATUS_CHECKEDOUT`。

- 仅当文件签出到指定的工作目录时才设置 `SCC_STATUS_CHECKEDOUT`。

- 如果当前用户将该文件签出到工作目录以外的目录中，则 `SCC_STATUS_OUTBYUSER` 设置但 `SCC_STATUS_CHECKEDOUT` 不是。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)