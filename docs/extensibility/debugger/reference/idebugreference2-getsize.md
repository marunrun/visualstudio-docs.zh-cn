---
title: IDebugReference2：： GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetSize
helpviewer_keywords:
- IDebugReference2::GetSize
ms.assetid: a404ddd9-d940-4513-97cd-f52b8ab6a560
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d7ea57467c6bcc716226ac7075976a0fb9daf5f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80720363"
---
# <a name="idebugreference2getsize"></a>IDebugReference2::GetSize
获取引用的值的大小（以字节为单位）。 留待将来使用。

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
弄返回引用的值的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>另请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
