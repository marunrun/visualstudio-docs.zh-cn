---
title: IDebugMethodField：： GetThis |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727163"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
获取 `this` `Me` [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 包含方法的对象) 指针中的 (。

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
弄返回表示 "this" 指针的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 在面向对象的语言中，通常是指向类的当前实例化的隐含指针。 这 `this` 在 c #/c + + 中称为，如 `Me` 中所示 [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
