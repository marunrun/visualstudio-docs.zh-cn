---
title: IDebugDocumentContext2::Seek |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Seek
helpviewer_keywords:
- IDebugDocumentContext2::Seek
ms.assetid: 71501356-8a82-4d36-b354-6625bdd2baa0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 413b1416adcd4b20231666e25f6a8044e632198b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325428"
---
# <a name="idebugdocumentcontext2seek"></a>IDebugDocumentContext2::Seek
按给定数量的语句或行移动文档上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT Seek( 
   int                      nCount,
   IDebugDocumentContext2** ppDocContext
);
```

```cpp
int Seek( 
   int                        nCount,
   out IDebugDocumentContext2 ppDocContext
);
```

## <a name="parameters"></a>参数
`nCount`\
[in]语句或继续推行，具体取决于文档上下文的行数。

`ppDocContext`\
[out]返回一个新[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对象的新位置。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)