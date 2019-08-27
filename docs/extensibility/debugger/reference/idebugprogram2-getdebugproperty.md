---
title: IDebugProgram2::GetDebugProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDebugProperty
helpviewer_keywords:
- IDebugProgram2::GetDebugProperty
ms.assetid: d194224e-f0e6-46ab-85d4-9e2639e28946
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 109e3ac1267afb4097429aafc9264416f3c2dbf1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319358"
---
# <a name="idebugprogram2getdebugproperty"></a>IDebugProgram2::GetDebugProperty
获取该程序的属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDebugProperty( 
   IDebugProperty2** ppProperty
);
```

```csharp
int GetDebugProperty( 
   out IDebugProperty2 ppProperty
);
```

## <a name="parameters"></a>参数
`ppProperty`\
[out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象，表示该程序的属性。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的属性是特定于该程序。 如果该程序需要返回多个属性，则[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)此方法返回的对象是一个容器的其他属性和调用[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)方法将返回所有属性的列表。

 程序可能会公开任何数量和类型的其他属性，可以通过描述`IDebugProperty2`接口。 IDE 可能会显示通过泛型属性浏览器用户界面的其他程序属性。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)