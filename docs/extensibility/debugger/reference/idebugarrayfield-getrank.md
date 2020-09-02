---
title: IDebugArrayField：： GetRank |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 692f2f13d861d9688ba349fbc80cb1ca426582c1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736310"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
获取数组的秩或维度数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetRank( 
   DWORD* pdwRank
);
```

```csharp
int GetRank(
   out uint pdwRank
);
```

## <a name="parameters"></a>参数
`pdwRank`\
弄返回秩。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 数组的秩对应于维数。 在 c + + 和 c # 中，多维数组实际上是数组的数组，因此可以只将一维数组视为 (并且 `GetRank` 方法始终返回 1) 。 另一方面，在中， [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 多维数组的处理方式不同，此类数组的秩反映 (的维数， `GetRank` 方法始终返回) 的维度数。

## <a name="see-also"></a>另请参阅
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
