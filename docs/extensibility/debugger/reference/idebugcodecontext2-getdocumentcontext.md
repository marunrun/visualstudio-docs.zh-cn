---
title: IDebugCodeContext2::GetDocumentContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetDocumentContext
helpviewer_keywords:
- IDebugCodeContext2::GetDocumentContext
ms.assetid: d552cc92-963f-43c1-949f-ae6b63a427b8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a12838db0687fd7ebe20a5c576db0e06ece49107
ms.sourcegitcommit: 34807a6b6105ae7839adde8ff994c85182ad3aff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2019
ms.locfileid: "67342398"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
获取与此代码的上下文相对应的文档上下文。 文档上下文表示对应于源生成的代码，此指令的源文件中的位置。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDocumentContext( 
   IDebugDocumentContext2** ppSrcCxt
);
```

```csharp
int GetDocumentContext( 
   out IDebugDocumentContext2 ppSrcCxt
);
```

## <a name="parameters"></a>参数
`ppSrcCxt`\
[out]返回[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对应于代码上下文的对象。 如果`S_OK`返回，则此应为非`null`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 调试引擎应返回失败代码，例如`E_FAIL`时`out`参数是`null`等当代码上下文具有任何关联的源位置。

## <a name="remarks"></a>备注
 通常情况下，文档上下文可以认为的源文件中的位置的代码上下文时的代码指令中的执行流的位置。

## <a name="see-also"></a>请参阅
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
