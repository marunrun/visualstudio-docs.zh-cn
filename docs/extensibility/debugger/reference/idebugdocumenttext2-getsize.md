---
title: IDebug文档文本2：：获取大小 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: edc4a209537ca4bd54d3f6d9343d1496ab7c0e90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731590"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
检索文档中此位置的文本大小。

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
[出]返回文本行数。

`pcNumChars`\
[出]返回文本的字符数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注

 [仅C++]如果不需要特定值，则为参数传递 NULL。

 [仅 C]必须指定这两个参数。

## <a name="see-also"></a>请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
