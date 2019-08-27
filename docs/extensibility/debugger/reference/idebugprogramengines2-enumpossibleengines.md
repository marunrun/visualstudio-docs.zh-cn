---
title: IDebugProgramEngines2::EnumPossibleEngines | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
helpviewer_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
ms.assetid: 993d70a4-f6a5-4e47-a603-0b162b9fde00
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 532486c66b6feb5c397b9167e2b1cd6197513fa8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343381"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
返回的所有可能的调试引擎 (DE)，可以调试该程序的 Guid。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumPossibleEngines( 
   DWORD  celtBuffer,
   GUID*  rgguidEngines,
   DWORD* pceltEngines
);
```

```csharp
int EnumPossibleEngines( 
   uint      celtBuffer,
   GUID[]    rgguidEngines,
   ref DWORD pceltEngines
);
```

## <a name="parameters"></a>参数
`celtBuffer`\
[in]若要返回的 DE Guid 数目。 这还将指定的最大大小`rgguidEngines`数组。

`rgguidEngines`\
[in、 out]DE Guid 要填充的数组。

`pceltEngines`\
[out]返回 DE Guid 返回的实际的数目。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回 [C++]`HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`或 [C#] 0x8007007A 如果缓冲区不够大。

## <a name="remarks"></a>备注
 若要确定引擎数量，调用此方法一次替换`celtBuffer`参数设置为 0 和`rgguidEngines`参数设置为 null 值。 这将返回`HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`(适用于 C# 的 0x8007007A) 和`pceltEngines`参数返回所需的缓冲区的大小。

## <a name="see-also"></a>请参阅
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)