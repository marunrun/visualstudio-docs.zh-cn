---
title: IDebugCanStopEvent2::GetDocumentContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetDocumentContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetDocumentContext
ms.assetid: 936a6c4e-30c5-4c7e-9ad5-910cc605a4b5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1c3d409b0fa4438331d1a798e5fd6e21b2c10ca9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349548"
---
# <a name="idebugcanstopevent2getdocumentcontext"></a>IDebugCanStopEvent2::GetDocumentContext
获取用于描述此事件的位置的文档上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDocumentContext ( 
   IDebugDocumentContext2** ppDocCxt
);
```

```csharp
int GetDocumentContext ( 
   out IDebugDocumentContext2 ppDocCxt
);
```

## <a name="parameters"></a>参数
`ppDocCxt`\
[out]返回[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)到当前代码位置表示对应一个源文件文档中的位置的接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 通常情况下，可以将文档上下文视为一个源文件中的位置。

 若要获取代码上下文，这是面向代码的说明，请调用[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)