---
title: IDebug文档上下文2：：获取来源范围 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 782cf230c38af77da09b49f69c093e2e95bf7199
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731799"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
获取此文档上下文的源代码范围。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSourceRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetSourceRange( 
   TEXT_POSITION[] pBegPosition,
   TEXT_POSITION[] pEndPosition
);
```

## <a name="parameters"></a>参数
`pBegPosition`\
[进出]用起始位置填充[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。 如果不需要此信息，则此参数设置为 null 值。

`pEndPosition`\
[进出]用结束位置填充[的TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。 如果不需要此信息，则此参数设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 源范围是源代码的整个范围，从当前语句回回，到上次提供代码的语句之后。 源范围通常用于将源语句（包括注释）与拆解窗口中的代码混合。

 要获取本文档上下文中包含的代码语句的范围，请调用[Get语句范围](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
