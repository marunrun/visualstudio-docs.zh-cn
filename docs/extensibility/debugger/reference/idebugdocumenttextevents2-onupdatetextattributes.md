---
title: IDebugDocumentTextEvents2::onUpdateTextAttributes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnUpdateTextAttributes
helpviewer_keywords:
- IDebugDocumentTextEvents2::onUpdateTextAttributes
ms.assetid: eb68d69a-1ad9-4ce4-84e1-40979ef16634
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a1eb8d6d9f14fcad5358b4a358673e08f3395ff
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351370"
---
# <a name="idebugdocumenttextevents2onupdatetextattributes"></a>IDebugDocumentTextEvents2::onUpdateTextAttributes
通知调试包已在文档文本特性进行了更新。

## <a name="syntax"></a>语法

```cpp
HRESULT onUpdateTextAttributes( 
   TEXT_POSITION pos,
   DWORD         dwNumToUpdate
);
```

```csharp
int onUpdateTextAttributes( 
   enum_TEXT_POSITION pos,
   uint               dwNumToUpdate
);
```

## <a name="parameters"></a>参数
`pos`\
[in]一个[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)指示更新文本特性的结构。

`dwNumToUpdate`\
[in]指定已更新的文本的字符的数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)