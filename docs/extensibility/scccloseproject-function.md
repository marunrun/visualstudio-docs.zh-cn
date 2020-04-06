---
title: SccClose项目功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCloseProject
helpviewer_keywords:
- SccCloseProject function
ms.assetid: 259c2069-d349-4814-810f-1c3151b7fb84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 71df385bc0cf42c2437abfd117c2f84bda5b5432
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701049"
---
# <a name="scccloseproject-function"></a>SccClose项目功能
此函数关闭项目，标志着特定会话的结束。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCloseProject (
   LPVOID pvContext
);
```

### <a name="parameters"></a>参数
 pvContext 源代码管理插件上下文结构。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|项目已成功关闭。|
|SCC_E_PROJNOTOPEN|当前未打开任何项目。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 在此函数之前始终调用[SccOpenProject。](../extensibility/sccopenproject-function.md) 然后调用此函数后，调用`SccOpenProject`函数或[SccUn初始化](../extensibility/sccuninitialize-function.md)，从而完全结束与源代码管理系统的连接。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
