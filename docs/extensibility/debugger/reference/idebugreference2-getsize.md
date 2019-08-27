---
title: IDebugReference2::GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetSize
helpviewer_keywords:
- IDebugReference2::GetSize
ms.assetid: a404ddd9-d940-4513-97cd-f52b8ab6a560
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5512a9d07c859dc548f91611bfc8d0c05621c0ff
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329780"
---
# <a name="idebugreference2getsize"></a>IDebugReference2::GetSize
获取大小，以字节为单位的引用的值。 留待将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize ( 
   DWORD* pdwSize
);
```

```csharp
int GetSize ( 
   out uint pdwSize
);
```

## <a name="parameters"></a>参数
`pdwSize`\
[out]返回的大小，以字节为单位的引用的值。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)