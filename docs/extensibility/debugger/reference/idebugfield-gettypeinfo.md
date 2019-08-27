---
title: IDebugField::GetTypeInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetTypeInfo
helpviewer_keywords:
- IDebugField::GetTypeInfo method
ms.assetid: bb5acfa3-04c3-4088-be84-9ff8926cd16f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc48442e27315e289c812c14e0ae70d8b8fd437a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333107"
---
# <a name="idebugfieldgettypeinfo"></a>IDebugField::GetTypeInfo
此方法获取的符号的类型的独立于类型的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeInfo( 
   TYPE_INFO* pTypeInfo
);
```

```csharp
int GetTypeInfo(
   TYPE_INFO[] pTypeInfo
);
```

## <a name="parameters"></a>参数
`pTypeInfo`\
[out]返回类型信息中提供[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 例如，独立于类型的信息将包括在 AppDomain、 模块和包含的符号的类。

## <a name="see-also"></a>请参阅
- [GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)