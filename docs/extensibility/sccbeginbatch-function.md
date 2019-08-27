---
title: SccBeginBatch 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6bb145358184117046e14b7b598ce6d4bb4586b0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333888"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 函数
此函数将启动批处理序列的源代码管理操作。 [SccEndBatch](../extensibility/sccendbatch-function.md)将调用以结束该批处理。 这些批不能嵌套。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|一批操作已成功开始。|
|SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 使用源控制批处理以跨多个项目或多个上下文中执行相同操作。 若要在批处理操作期间消除冗余的每个项目对话框从用户体验，可以使用批处理。 `SccBeginBatch`函数和[SccEndBatch](../extensibility/sccendbatch-function.md)作为函数对用于指示的开头和结尾的操作。 它们不能嵌套。 `SccBeginBatch` 设置一个标志，指示批处理操作正在进行。

 批处理操作生效时，源代码管理插件应为用户提供最多一个对话框中的任何问题，并对所有后续操作应用来自该对话框中的响应。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)