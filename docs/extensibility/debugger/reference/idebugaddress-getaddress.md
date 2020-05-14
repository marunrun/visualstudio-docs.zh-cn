---
title: IDebug地址：获取地址 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 162a64c9118bdcde23208082350005e607a237b8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736603"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
返回描述对象及其在其范围或容器中的位置的结构。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAddress (
   DEBUG_ADDRESS * pAddress
);
```

```csharp
int GetAddress(
   DEBUG_ADDRESS[] pAddress
);
```

## <a name="parameters"></a>参数
`pAddress`\
[进出]由此方法填充[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构传递给此方法，然后使用适当的信息填充它。 如何解释此信息取决于返回的信息类型和符号处理程序本身。 有关详细信息，请参阅[DEBUG_ADDRESS。](../../../extensibility/debugger/reference/debug-address.md)

## <a name="see-also"></a>请参阅
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
