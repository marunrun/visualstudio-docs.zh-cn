---
title: IDebugEngine2：：设置指标 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2:::SetMetric
helpviewer_keywords:
- IDebugEngine2:::SetMetric
ms.assetid: dcda4972-c32e-4693-a0e1-25d5c58b9782
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: caada8db1791d94e7a9632394cd4659bf8cec3a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730893"
---
# <a name="idebugengine2setmetric"></a>IDebugEngine2::SetMetric
此方法设置称为指标的注册表值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetMetric(
   LPCOLESTR pszMetric,
   VARIANT   varValue
);
```

```csharp
int SetMetric(
   string pszMetric,
   object varValue
);
```

## <a name="parameters"></a>参数
`pszMetric`\
[在]指标名称。

`varValue`\
[在]指定指标值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 指标是用于更改调试引擎的行为或通告支持的功能的注册表值。 此方法可以将调用转发到用于调试功能的 SDK[帮助器](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)的适当形式`SetMetric`。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
