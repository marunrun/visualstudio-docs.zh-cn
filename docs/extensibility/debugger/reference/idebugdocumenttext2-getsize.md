---
title: IDebugDocumentText2::GetSize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7f382b1d27a83e4493431ac8e6cca3d6aef9dd72
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337378"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
检索在此位置上的文档中的文本的大小。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   ULONG* pcNumLines,
   ULONG* pcNumChars
);
```

```csharp
int GetSize( 
   ref uint pcNumLines,
   ref uint pcNumChars
);
```

## <a name="parameters"></a>参数
`pcNumLines`\
[out]返回文本的行数。

`pcNumChars`\
[out]返回文本的字符数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注

 [C++仅]如果不需要特定的值，请将传递该参数为 NULL。

 [C#仅]必须指定这两个参数。

## <a name="see-also"></a>请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)