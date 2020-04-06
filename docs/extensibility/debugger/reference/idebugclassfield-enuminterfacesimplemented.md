---
title: IDebugClassfield：实现枚举界面 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 91d9cac6b695ba2a0d34da776fa79ba62ba2e015
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734483"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
为此类实现的接口创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumInterfacesImplemented( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumInterfacesImplemented(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[出]返回表示已实现接口列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象。 如果没有接口，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或返回S_FALSE如果此类上没有实现接口。 否则，返回错误代码。

## <a name="remarks"></a>备注
 枚举的每个元素都是描述接口的[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)对象。 请注意，非托管[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]代码不使用接口作为离散实体，因此此方法始终返回非托管[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]代码的 null 值。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
