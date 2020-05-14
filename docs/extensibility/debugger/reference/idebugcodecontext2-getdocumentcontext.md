---
title: IDebugCode上下文2：：获取文档上下文 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetDocumentContext
helpviewer_keywords:
- IDebugCodeContext2::GetDocumentContext
ms.assetid: d552cc92-963f-43c1-949f-ae6b63a427b8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 46510ce794ea30fdd365a77007b962a1eafd5d31
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734342"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
获取对应于此代码上下文的文档上下文。 文档上下文表示源文件中对应于生成此指令的源代码的位置。

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
[出]返回与代码上下文对应的[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对象。 如果`S_OK`返回，则 th 应是非`null`。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 调试引擎应返回故障代码，`E_FAIL``out`例如参数为`null`参数时，例如代码上下文没有关联的源位置。

## <a name="remarks"></a>备注
 通常，文档上下文可以被视为源文件中的位置，而代码上下文是执行流中代码指令的位置。

## <a name="see-also"></a>请参阅
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
