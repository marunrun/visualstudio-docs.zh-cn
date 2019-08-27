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
ms.openlocfilehash: 25a4b9b7d07b74047890c4ba56583cc09a394368
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353516"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 函数
此函数可获取所选文件受源代码管理的一组的状态信息。

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

[in]源控制插件上下文结构。

 nFiles

[in]中指定的文件数`lpFileNames`数组和长度的`lpStatus`数组。

 lpFileNames

[in]要查询的文件的名称的数组。

 lpStatus

[in、 out]数组中的源代码管理插件返回的每个文件的状态标志。 有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|查询已成功完成。|
|SCC_E_ACCESSFAILURE|出现与访问源代码管理系统、 网络或争用问题可能导致问题。 建议重试。|
|SCC_E_PROJNOTOPEN|不受源代码管理打开项目时。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 如果`lpFileName`是空字符串，目前没有要更新的状态信息。 否则，它是文件的为其状态信息可能已更改的完整路径名称。

 返回数组可以是一个位掩码的`SCC_STATUS_xxxx`位。 有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)。 源代码管理系统可能不支持所有位类型。 例如，如果`SCC_STATUS_OUTOFDATE`未提供，则只需不设置了位。

 使用此函数时签出文件，请注意以下`MSSCCI`状态要求：

- `SCC_STATUS_OUTBYUSER` 当前用户已签出文件时设置。

- `SCC_STATUS_CHECKEDOUT` 不能设置，除非`SCC_STATUS_OUTBYUSER`设置。

- `SCC_STATUS_CHECKEDOUT` 仅当该文件已签出到指定的工作目录设置。

- 如果该文件已签出由当前用户以外的工作目录的目录`SCC_STATUS_OUTBYUSER`设置，但`SCC_STATUS_CHECKEDOUT`不是。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)