---
title: IDebugMethodfield：获取此 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetThis
helpviewer_keywords:
- IDebugMethodField::GetThis method
ms.assetid: cc235bea-e909-4d8c-ab54-936736c803fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b29252d1586d039084ec1d21f1fc4967aea68baf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727163"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
获取`this`包含方法`Me`的对象[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]的指针。

## <a name="syntax"></a>语法

```cpp
HRESULT GetThis( 
   IDebugClassField** ppClass
);
```

```csharp
int GetThis(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>参数
`ppClass`\
[出]返回表示"此"指针的[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 在面向对象的语言中，通常存在指向类当前实例化的隐含指针。 这在 C#/C++ 和 中`this``Me`[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]称为 。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
