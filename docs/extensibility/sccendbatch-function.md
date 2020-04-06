---
title: SccEndBatch 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccEndBatch
helpviewer_keywords:
- SccEndBatch function
ms.assetid: 100e7833-fe0a-45c0-9fca-3e61fd1165b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51fe7e0bc0d417ffa182fbc68fd2779ed0b625d9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700925"
---
# <a name="sccendbatch-function"></a>SccEndBatch 功能
此功能完成一批源代码管理操作。 这些批次可能无法嵌套。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccEndBatch(void);
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|一批操作成功结束。|
|SCC_E_UNKNOWNERROR|非特异性故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于跨多个项目或多个上下文执行相同的源代码管理操作。 批处理可用于在批处理操作期间从用户体验中消除冗余对话框。 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)和`SccEndBatch`函数用作一对，以指示操作的开始和结束。 它们不能嵌套。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
