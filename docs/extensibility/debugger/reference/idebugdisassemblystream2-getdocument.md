---
title: IDebugDisassemblyStream2::GetDocument |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetDocument
helpviewer_keywords:
- IDebugDisassemblyStream2::GetDocument
ms.assetid: 3d039a44-ebaa-4413-ac18-7cfd92c408bd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a043d5462ad206395cb7d70d28152c19a7df6460
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310435"
---
# <a name="idebugdisassemblystream2getdocument"></a>IDebugDisassemblyStream2::GetDocument
获取与此输入流关联的源文档。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDocument( 
   BSTR              bstrDocumentUrl,
   IDebugDocument2** ppDocument
);
```

```csharp
int GetDocument( 
   string              bstrDocumentUrl,
   out IDebugDocument2 ppDocument
);
```

## <a name="parameters"></a>参数
`bstrDocumentUrl`\
[in]文档 URL。

`ppDocument`\
[out]返回[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)对象，表示文档。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 有未存储在实际文件中的文本文档的调试引擎实现此方法。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)