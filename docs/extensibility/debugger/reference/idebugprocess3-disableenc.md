---
title: IDebugProcess3：:D可微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5b39bb448501bacd5ab458b7e61bb1a5044bc8a3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723731"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
此方法显式禁用此过程上的"编辑并继续"（以及它包含的所有程序）。 自定义端口供应商应始终返回`E_NOTIMPL`。

## <a name="syntax"></a>语法

```cpp
HRESULT DisableENC(
   EncUnavailableReason reason
);
```

```csharp
   EncUnavailableReason reason
);
```

## <a name="parameters"></a>参数
`reason`\
[在][来自 Enc不可用原因](../../../extensibility/debugger/reference/encunavailablereason.md)枚举的值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

> [!NOTE]
> 自定义端口供应商应始终返回`E_NOTIMPL`。

## <a name="remarks"></a>备注
 一旦进程禁用了"编辑并继续"，只能通过重新启动进程重新启用它。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
