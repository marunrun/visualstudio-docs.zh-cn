---
title: INTERCEPT_EXCEPTION_ACTION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- INTERCEPT_EXCEPTION_ACTION
helpviewer_keywords:
- INTERCEPT_EXCEPTION_ACTION enumeration
ms.assetid: e647f1eb-2932-4447-8c78-3b0d706fb972
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 265ed30272c959b6ee812a83f748888a5af15cab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350245"
---
# <a name="interceptexceptionaction"></a>INTERCEPT_EXCEPTION_ACTION
指定当截获异常时要执行的操作。

## <a name="syntax"></a>语法

```cpp
enum enum_INTERCEPT_EXCEPTION_ACTION
{
    IEA_INTERCEPT = 0x0001
}
typedef DWORD INTERCEPT_EXCEPTION_ACTION;
```

```csharp
public enum enum_INTERCEPT_EXCEPTION_ACTION
{
    IEA_INTERCEPT = 0x0001
}
```

## <a name="parameters"></a>参数

`IEA_INTERCEPT`\
启用截获当前异常。 这是目前支持的唯一值，必须指定。

## <a name="remarks"></a>备注
这些值传递到[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
