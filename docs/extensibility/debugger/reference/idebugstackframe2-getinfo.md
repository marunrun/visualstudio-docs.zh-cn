---
title: IDebugStackFrame2::GetInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetInfo
helpviewer_keywords:
- IDebugStackFrame2::GetInfo
ms.assetid: 19c6870b-b94e-453c-bf19-82ce95b79d26
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad560386991a0545510e1b74a140d17cc35fcbe3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352117"
---
# <a name="idebugstackframe2getinfo"></a>IDebugStackFrame2::GetInfo
获取堆栈帧的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInfo ( 
   FRAMEINFO_FLAGS dwFieldSpec,
   UINT            nRadix,
   FRAMEINFO*      pFrameInfo
);
```

```csharp
int GetInfo ( 
   enum_FRAMEINFO_FLAGS dwFieldSpec,
   uint                 nRadix,
   FRAMEINFO[]          pFrameInfo
);
```

## <a name="parameters"></a>参数
`dwFieldSpec`\
[in]中的标志的组合[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)枚举，用于指定的哪些字段`pFrameInfo`参数是要填充。

`nRadix`\
[in]用于格式化数值的任何信息的基数。

`pFrameInfo`\
[out]一个[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)堆栈帧的说明使用填充的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)