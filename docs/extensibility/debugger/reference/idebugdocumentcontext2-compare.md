---
title: IDebugDocumentContext2::Compare | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Compare
helpviewer_keywords:
- IDebugDocumentContext2::Compare
ms.assetid: 2327b1ba-52d0-42fb-a01e-63cb4b332d2f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0f21b338511890879d805ce49377554719070604
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344393"
---
# <a name="idebugdocumentcontext2compare"></a>IDebugDocumentContext2::Compare
比较此文档上下文到给定数组的文档上下文。

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
[in]中的值[DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)枚举，用于指定的比较类型。

`rgpDocContextSet`\
[in]一个数组[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对象表示要进行比较的文档上下文。

`dwDocContextSetLen`\
[in]文档上下文进行比较的数组的长度。

`pdwDocContext`\
[out]返回到索引`rgpDocContextSet`满足的比较的第一个文档上下文的数组。

## <a name="return-value"></a>返回值
 返回`S_OK`如果找到匹配项。 返回`S_FALSE`如果没有找到匹配。 否则，返回错误代码。

## <a name="remarks"></a>备注
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)数组中传递的对象必须由相同的调试引擎实现`IDebugDocumentContext2`对象; 否则为调用该比较不有效。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)