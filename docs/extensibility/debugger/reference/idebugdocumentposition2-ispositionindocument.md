---
title: IDebug 文档位置2：：在文档中定位 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
helpviewer_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
ms.assetid: d5cf57cb-b93b-4e1d-bec9-185f4fe8668d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4d92dddda8fd9831f5d66b602cd48fdbbc3dbcf1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731653"
---
# <a name="idebugdocumentposition2ispositionindocument"></a>IDebugDocumentPosition2::IsPositionInDocument
确定文档位置是否包含在给定文档中。

## <a name="syntax"></a>语法

```cpp
HRESULT IsPositionInDocument( 
   IDebugDocument2* pDoc
);
```

```csharp
int IsPositionInDocument( 
   IDebugDocument2 pDoc
);
```

## <a name="parameters"></a>参数
`pDoc`\
[在]表示包含文档候选项的[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法主要用于在[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口中设置断点。 加载文档时，将调用断点位置以确定文档是否包含此位置。

## <a name="see-also"></a>请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
