---
title: IDebugEngine3：：设置我的代码状态 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9930f8ecf0c2f9b6fff4ce1c9e3edb935c5a7912
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730683"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
此方法向调试引擎介绍 JustMyCode 状态信息。

## <a name="syntax"></a>语法

```cpp
HRESULT SetJustMyCodeState(
   BOOL           fUpdate,
   DWORD          dwModules,
   JMC_CODE_SPEC* rgJMCSpec
);
```

```csharp
int SetJustMyCodeState(
   int             fUpdate,
   uint            dwModules,
   JMC_CODE_SPEC[] rgJMCSpec
);
```

## <a name="parameters"></a>参数
`fUpdate`\
[在]非零`TRUE`（ ） 更新当前信息，`FALSE`零 （ ） 以重置所有信息（忽略以前设置的任何信息）。

`dwModules`\
[在]中的信息结构数量`rgJMCSpec.`

`rgJMCSpec`\
[在][要使用的JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)结构数组。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 JustMyCode 是仅调试属于用户的代码并忽略所有中间代码（如系统代码）的概念，即使源代码可用于该系统代码也是如此。

## <a name="see-also"></a>请参阅
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)
