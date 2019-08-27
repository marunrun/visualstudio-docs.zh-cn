---
title: IDebugProcess3::GetEngineFilter | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetEngineFilter
- IDebugProcess3::GetEngineFilter
ms.assetid: ccb7ecb0-f189-4e80-b5b2-221a095e01f5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2b468f28e50b77edf4b35fbb7274767f773bd56
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313931"
---
# <a name="idebugprocess3getenginefilter"></a>IDebugProcess3::GetEngineFilter
检索可用的调试引擎的唯一标识符的数组。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineFilter(
   GUID_ARRAY *pEngineArray
);
```

```csharp
public int GetEngineFilter(
   out GUID_ARRAY[] pEngineArray
);
```

## <a name="parameters"></a>参数
`pEngineArray`\
[out]对包含的调试引擎的唯一标识符的结构的引用。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md)