---
title: IDebug文档位置2：：获取范围 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::GetRange
helpviewer_keywords:
- IDebugDocumentPosition2::GetRange
ms.assetid: 91a06ee7-253a-4215-be22-04bf57305aa8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a923691afdfe145931ab31d0e9bbc6142e7c8d1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731662"
---
# <a name="idebugdocumentposition2getrange"></a>IDebugDocumentPosition2::GetRange
获取此文档位置的范围。

## <a name="syntax"></a>语法

```cpp
HRESULT GetRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetRange( 
   TEXT_POSITION[] pBegPosition,
   TEXT_POSITION[] pEndPosition
);
```

## <a name="parameters"></a>参数
`pBegPosition`\
[进出]用起始位置填充[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。 如果不需要此信息，则此参数设置为 null 值。

`pEndPosition`\
[进出]用结束位置填充[的TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。 如果不需要此信息，则此参数设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调试引擎 （DE） 使用在位置断点的文档位置中指定的范围来提前搜索实际贡献代码的语句。 例如，考虑以下代码：

```
Line 5: // comment
Line 6: x = 1;
```

 第 5 行对正在调试的程序没有贡献任何代码。 如果在第 5 行上设置断点的调试器希望 DE 向前搜索一定数量的第一行贡献代码，则调试器将指定一个范围，其中包括可能正确放置断点的其他候选行。 然后，DE 会向前搜索这些行，直到找到可以接受断点的行。

## <a name="see-also"></a>请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
