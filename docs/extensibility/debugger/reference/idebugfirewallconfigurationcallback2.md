---
title: IDebug防火墙配置回调2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFirewallConfigurationCallback2 interface
ms.assetid: 0827361c-b97c-4851-9898-ab6d88c81811
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 635771fc87326b28566058a43d4922b131ae1975
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728713"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
启用使用 DCOM 要求 UI 确保[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]防火墙不会阻止远程调试的调试引擎。

## <a name="syntax"></a>语法

```
IDebugFirewallConfigurationCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示了 的方法`IDebugFirewallConfigurationCallback2`。

|方法|描述|
|------------|-----------------|
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|请求防火墙不会阻止远程调试。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
