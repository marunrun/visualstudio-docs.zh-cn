---
title: IDebug文档上下文2：：比较 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Compare
helpviewer_keywords:
- IDebugDocumentContext2::Compare
ms.assetid: 2327b1ba-52d0-42fb-a01e-63cb4b332d2f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b0e46f765c8e4c0e12c3bb9447e0713919fae7b8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731893"
---
# <a name="idebugdocumentcontext2compare"></a>IDebugDocumentContext2::Compare
将此文档上下文与给定的文档上下文数组进行比较。

## <a name="syntax"></a>语法

```cpp
HRESULT Compare( 
   DOCCONTEXT_COMPARE       compare,
   IDebugDocumentContext2** rgpDocContextSet,
   DWORD                    dwDocContextSetLen,
   DWORD*                   pdwDocContext
);
```

```csharp
int Compare( 
   enum_ DOCCONTEXT_COMPARE compare,
   IDebugDocumentContext2[] rgpDocContextSet,
   uint                     dwDocContextSetLen,
   out uint                 pdwDocContext
);
```

## <a name="parameters"></a>参数
`compare`\
[在][DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)枚举中指定比较类型的值。

`rgpDocContextSet`\
[在][IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对象的数组，表示要比较的文档上下文。

`dwDocContextSetLen`\
[在]要比较的文档上下文数组的长度。

`pdwDocContext`\
[出]将索引返回到满足比较`rgpDocContextSet`的第一个文档上下文的数组中。

## <a name="return-value"></a>返回值
 如果`S_OK`找到匹配项，则返回。 如果`S_FALSE`未找到匹配项，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 数组中传递的[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对象必须由实现所调用对象的同一`IDebugDocumentContext2`调试引擎实现;否则，比较无效。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)
