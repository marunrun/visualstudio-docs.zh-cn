---
title: IDebugObject2：：Isc过时 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::IsEncOutdated
helpviewer_keywords:
- IDebugObject2::IsEncOutdated method
ms.assetid: d3a8c02d-895b-478c-9957-d663130f308e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a90ff97b87ec2abaab87dfece5b2a2ac1cabb28c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726098"
---
# <a name="idebugobject2isencoutdated"></a>IDebugObject2::IsEncOutdated
此方法确定此对象或父容器的"编辑并继续"状态是否已过期。 自定义表达式赋值器不实现此方法，并且始终返回`E_NOTIMPL`。

## <a name="syntax"></a>语法

```cpp
HRESULT IsEncOutdated(
   BOOL* pfEncOutdated
);
```

```csharp
int IsEncOutdated(
   out int pfEncOutdated
);
```

## <a name="parameters"></a>参数
`pfEncOutdated`\
[出]如果"编辑`TRUE`"和"继续"状态已过期，则非零 （`FALSE`） 如果不是。"

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

> [!NOTE]
> 自定义表达式赋值器应始终返回`E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
