---
title: IDebugDocumentContext2：： GetSourceRange |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
[in，out]用起始位置填充的 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 结构。 如果不需要此信息，请将此参数设置为 null 值。

`pEndPosition`\
[in，out]用结束位置填充的 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 结构。 如果不需要此信息，请将此参数设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 源范围是源代码的整个范围，从当前语句返回到紧邻提供代码的上一条语句之后。 源范围通常用于在 "反汇编" 窗口中使用代码来混合源语句（包括注释）。

 若要仅获取此文档上下文中包含的代码语句的范围，请调用 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
