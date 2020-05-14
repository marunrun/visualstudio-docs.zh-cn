---
title: SccQuery信息功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1efae18f15588f4dacf3409ea95e30af05397c6e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700479"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 函数
此函数获取源代码管理下的一组选定文件的状态信息。

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

[在]源代码管理插件上下文结构。

 n文件

[在]`lpFileNames`数组中指定的文件数和`lpStatus`数组的长度。

 lpFile名称

[在]要查询的文件的名称数组。

 lp状态

[进出]源控件插件返回每个文件的状态标志的数组。 有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|查询成功。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由网络或争用问题引起的。 建议重试。|
|SCC_E_PROJNOTOPEN|项目在源代码管理下不开放。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 如果是`lpFileName`空字符串，则当前没有要更新的状态信息。 否则，它是状态信息可能已更改的文件的完整路径名称。

 返回数组可以是`SCC_STATUS_xxxx`位掩码。 有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)。 源代码管理系统可能不支持所有位类型。 例如，如果未`SCC_STATUS_OUTOFDATE`提供，则仅设置位。

 使用此函数签出文件时，请注意以下`MSSCCI`状态要求：

- `SCC_STATUS_OUTBYUSER`当前用户签出文件时设置。

- `SCC_STATUS_CHECKEDOUT`除非已设置，`SCC_STATUS_OUTBYUSER`否则无法设置。

- `SCC_STATUS_CHECKEDOUT`仅在文件签出到指定的工作目录中时设置。

- 如果当前用户将文件签出到工作目录以外的目录中，`SCC_STATUS_OUTBYUSER`则设置为未`SCC_STATUS_CHECKEDOUT`设置。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
