---
title: FIELD_KIND_EX | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- FIELD_KIND_EX enumeration
ms.assetid: 922c3208-1e94-485f-b70a-3bc96affeff8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd481883c826ff21a82b52bdd82de087b6219b58
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309017"
---
# <a name="fieldkindex"></a>FIELD_KIND_EX
枚举其他类型的字段的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象可包含。 此枚举扩展[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)枚举。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
typedef DWORD FIELD_KIND_EX;
```

```csharp
public enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
```

## <a name="fields"></a>字段
`FIELD_KIND_EX_NONE`\
字段不包含扩展的类型。

`FIELD_TYPE_EX_METHODVAR`\
字段包含一个方法的变量。

`FIELD_TYPE_EX_CLASSVAR`\
字段包含一个类变量。

## <a name="requirements"></a>要求
标头：Sh.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)
