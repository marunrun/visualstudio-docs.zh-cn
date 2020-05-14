---
title: SccGet事件功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700822"
---
# <a name="sccgetevents-function"></a>SccGet事件功能
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

[在]源代码管理插件上下文结构。

 lpFile名称

[进出]缓冲区，其中源代码管理插件放置返回的文件名（最多_MAX_PATH个字符）。

 lp状态

[进出]返回状态代码（有关可能的值，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)）。

 pn 事件剩余

[进出]返回此调用后队列中留下的条目数。 如果此号码很大，呼叫者可能会决定呼叫[SccQueryInfo](../extensibility/sccqueryinfo-function.md)以一次获取所有信息。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|使事件成功。|
|SCC_E_OPNOTSUPPORTED|不支持此函数。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 在空闲处理期间调用此功能，以查看源控制下的文件是否有任何状态更新。 源代码管理插件维护它所知道的所有文件的状态，每当插件注意到状态更改时，状态和关联的文件都存储在队列中。 调用`SccGetEvents`时，将检索并返回队列的顶部元素。 此函数受约束仅返回以前缓存的信息，并且必须有一个非常快速的周转（即，不读取磁盘或询问源代码管理系统的状态）;否则，IDE 的性能可能会开始下降。

 如果没有要报告的状态更新，源代码管理插件将空字符串存储在 指向 的`lpFileName`缓冲区中。 否则，插件将存储状态信息已更改的文件的完整路径名称，并返回相应的状态代码（[文件状态代码](../extensibility/file-status-code-enumerator.md)中详述的值之一）。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
