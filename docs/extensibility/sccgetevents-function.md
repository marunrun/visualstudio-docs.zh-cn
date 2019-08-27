---
title: SccGetEvents 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c8c3c08311c8dd359acaed18decc046354e7f37
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332028"
---
# <a name="sccgetevents-function"></a>SccGetEvents 函数
此函数检索排队的状态事件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetEvents (
   LPVOID pvContext,
   LPSTR  lpFileName,
   LPLONG lpStatus,
   LPLONG pnEventsRemaining
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源控制插件上下文结构。

 lpFileName

[in、 out]缓冲区的源控件插件会将返回的文件名 （最多 _max_path(256 个字符）。

 lpStatus

[in、 out]将返回状态代码 (请参阅[状态代码的文件](../extensibility/file-status-code-enumerator.md)有关可能的值)。

 pnEventsRemaining

[in、 out]返回此调用后保留在队列的项数。 如果此数值较大，可能会决定调用方调用[SccQueryInfo](../extensibility/sccqueryinfo-function.md)若要获取的所有信息在一次。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|获取事件已成功。|
|SCC_E_OPNOTSUPPORTED|不支持此函数。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 若要查看是否已在源代码管理下的文件的任何状态更新，空闲处理过程中调用此函数。 源代码管理插件维护它了解的所有文件的状态，每当更改的状态记录了该插件的状态和关联的文件存储在队列中。 当`SccGetEvents`调用时，顶部检索并返回队列的元素。 此函数被约束为返回唯一以前缓存的信息，并且必须具有非常快速周转时间 （即，任何磁盘的读取或状态请求的源控制系统）;否则，IDE 的性能可能开始下降。

 如果不没有报告任何状态更新，源代码管理插件会将空字符串存储在通过指向的缓冲区`lpFileName`。 否则，该插件将存储该文件的完整路径名称为它的状态信息已更改并返回相应的状态代码 (中详述的值之一[状态代码的文件](../extensibility/file-status-code-enumerator.md))。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)