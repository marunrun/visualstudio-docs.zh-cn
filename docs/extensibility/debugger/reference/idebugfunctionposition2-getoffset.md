---
title: IDebugFunctionPosition2::GetOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2::GetOffset
helpviewer_keywords:
- IDebugFunctionPosition2::GetOffset
ms.assetid: 60943782-aec7-4be2-b222-1984ed53a543
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 891707f5937085f69bf037abdec81e6c36315fa0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313310"
---
# <a name="idebugfunctionposition2getoffset"></a>IDebugFunctionPosition2::GetOffset
检索函数的源文档中的位置。

## <a name="syntax"></a>语法

```cpp
HRESULT GetOffset( 
   TEXT_POSITION* pPosition
);
```

```csharp
int GetOffset(
   TEXT_POSITION[] pPosition
);
```

## <a name="parameters"></a>参数
`pPosition`\
[in、 out]一个[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)填充函数的文档中的位置的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)