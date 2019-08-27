---
title: IDebugStackFrame2::GetDebugProperty | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetDebugProperty
helpviewer_keywords:
- IDebugStackFrame2::GetDebugProperty
ms.assetid: 02c2fa04-1424-4bca-9936-feaecd2afab6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4c520482d78b8630c639088ca98d66782f2e2d75
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321819"
---
# <a name="idebugstackframe2getdebugproperty"></a>IDebugStackFrame2::GetDebugProperty
获取堆栈帧的属性的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDebugProperty ( 
   IDebugProperty2** ppDebugProp
);
```

```csharp
int GetDebugProperty ( 
   out IDebugProperty2 ppDebugProp
);
```

## <a name="parameters"></a>参数
`ppDebugProp`\
[out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)介绍此堆栈帧的属性的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 调用[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)与适当的筛选器的方法可以检索本地变量、 方法参数、 寄存器以及与此堆栈帧相关联"this"指针。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)