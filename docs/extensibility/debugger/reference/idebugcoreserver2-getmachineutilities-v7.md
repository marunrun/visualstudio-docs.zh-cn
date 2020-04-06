---
title: IDebugCoreServer2：：GetMachineUtilities_V7 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 79eba6889583f1dfa482dab107ad31eaaacdbcc2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733150"
---
# <a name="idebugcoreserver2getmachineutilities_v7"></a>IDebugCoreServer2::GetMachineUtilities_V7
此方法获取服务器的计算机实用程序。

> [!NOTE]
> 此方法已过时：不使用 （[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]如果调用此方法，`E_NOTIMPL`则始终返回）。 由于历史原因，它被保留下来。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMachineUtilities_V7(
   IDebugMDMUtil2_V7** ppUtil
);
```

```csharp
int GetMachineUtilities_V7(
   out IDebugMDMUtil2_V7 ppUtil
);
```

## <a name="parameters"></a>参数
`ppUtil`\
[出]返回表示`IDebugMDMUtil2_V7`计算机实用程序信息的接口。

## <a name="return-value"></a>返回值
 始终返回`E_NOTIMPL`，指示该方法未实现。

## <a name="remarks"></a>备注
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]如果调用`E_NOTIMPL`此方法，则始终返回。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
