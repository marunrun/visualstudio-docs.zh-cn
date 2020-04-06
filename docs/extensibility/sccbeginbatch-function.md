---
title: SccBeginBatch 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c7982d8c8c0d71f8c79e9b808be5453d384882d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701197"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 功能
此函数启动源控制操作的批处理序列。 将调用[SccEndBatch](../extensibility/sccendbatch-function.md)以结束批处理。 这些批次可能无法嵌套。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|批量操作已成功启动。|
|SCC_E_UNKNOWNERROR|非特异性故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于跨多个项目或多个上下文执行相同的操作。 批处理可用于在批处理操作期间从用户体验中消除每个项目的冗余对话框。 函数`SccBeginBatch`和[SccEndBatch](../extensibility/sccendbatch-function.md)用作函数对，以指示操作的开始和结束。 它们不能嵌套。 `SccBeginBatch`设置指示批处理操作正在进行的标志。

 当批处理操作生效时，源代码管理插件应最多向用户显示一个对话框，用于任何问题，并将该对话框的响应应用于所有后续操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
