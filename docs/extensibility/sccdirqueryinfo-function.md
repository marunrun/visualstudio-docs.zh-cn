---
title: SccDirQuery信息功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700955"
---
# <a name="sccdirqueryinfo-function"></a>SccDirQueryInfo 功能
此函数检查完全限定的目录的列表，以检查其当前状态。

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

[在]源代码管理插件上下文结构。

 nDirs

[在]选择要查询的目录数。

 lpDirnames

[在]要查询的目录的完全限定路径的数组。

 lp状态

[进出]源代码管理插件的数组结构，用于返回状态标志（有关详细信息，请参阅[目录状态代码](../extensibility/directory-status-code-enumerator.md)）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|查询成功。|
|SCC_E_OPNOTSUPPORTED|源代码控制系统不支持此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特异性故障。|

## <a name="remarks"></a>备注
 函数用`SCC_DIRSTATUS`来自族的位掩码填充返回数组（请参阅[目录状态代码](../extensibility/directory-status-code-enumerator.md)），每个目录都有一个条目。 状态数组由调用方分配。

 IDE 在重命名目录之前使用此函数，通过查询目录是否具有相应的项目来检查该目录是否处于源代码管理之下。 如果目录不受源代码管理，IDE 可以向用户提供适当的警告。

> [!NOTE]
> 如果源代码管理插件选择不实现一个或多个状态值，则应将未实现位设置为零。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [目录状态代码](../extensibility/directory-status-code-enumerator.md)
