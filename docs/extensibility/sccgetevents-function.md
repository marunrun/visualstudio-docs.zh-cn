---
title: SccGetEvents 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 91b3debf0e686ceece3048cf3d92b629e3359edd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700822"
---
# <a name="sccgetevents-function"></a>SccGetEvents 函数
此函数检索排队状态事件。

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

中源代码管理插件上下文结构。

 lpFileName

[in，out]缓冲区，其中，源代码管理插件将返回的文件名 (最多 _MAX_PATH 个字符) 。

 lpStatus

[in，out]返回状态代码 (有关可能的值) ，请参阅 [文件状态代码](../extensibility/file-status-code-enumerator.md) 。

 pnEventsRemaining

[in，out]返回此调用之后队列中剩余的项数。 如果此数字较大，则调用方可能决定调用 [SccQueryInfo](../extensibility/sccqueryinfo-function.md) 来一次获取所有信息。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|获取事件成功。|
|SCC_E_OPNOTSUPPORTED|不支持此函数。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 在空闲处理期间调用此函数，以查看是否存在针对源代码管理下的文件的任何状态更新。 源代码管理插件维护它知道的所有文件的状态，并且每当插件记录状态的更改时，状态和相关文件将存储在队列中。 `SccGetEvents`调用时，将检索并返回队列的顶层元素。 此函数被约束为仅返回以前缓存的信息，并且必须具有非常快速的周转 (即，不读取磁盘或请求源代码管理系统的状态) ;否则，IDE 的性能可能会下降。

 如果没有要报告的状态更新，则源代码管理插件会将空字符串存储在指向的缓冲区中 `lpFileName` 。 否则，该插件存储状态信息已更改的文件的完整路径名称，并 ([文件状态代码](../extensibility/file-status-code-enumerator.md)) 中详细说明的值之一返回相应的状态代码。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
