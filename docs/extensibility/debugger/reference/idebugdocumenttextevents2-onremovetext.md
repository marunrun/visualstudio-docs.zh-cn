---
title: IDebug文档文本事件2：：：打开删除文本 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnRemoveText
helpviewer_keywords:
- IDebugDocumentTextEvents2::onRemoveText
ms.assetid: 1ebeabb2-52a1-4ccc-83cd-9ae7c3541783
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 744a6c769673acdc383999392cde88d255ad8142
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731414"
---
# <a name="idebugdocumenttextevents2onremovetext"></a>IDebugDocumentTextEvents2::onRemoveText
通知调试包文本已从文档中删除。

## <a name="syntax"></a>语法

```cpp
HRESULT onRemoveText( 
   TEXT_POSITION pos,
   DWORD         dwNumToRemove
);
```

```csharp
int onRemoveText( 
   enum_TEXT_POSITION pos,
   uint               dwNumToRemove
);
```

## <a name="parameters"></a>参数
`pos`\
[在]指示文本删除位置[的TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。

`dwNumToRemove`\
[在]指定已删除的文本的字符数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
