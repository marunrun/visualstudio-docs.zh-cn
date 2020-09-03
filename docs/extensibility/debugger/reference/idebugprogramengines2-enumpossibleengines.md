---
title: IDebugProgramEngines2：： EnumPossibleEngines |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
helpviewer_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
ms.assetid: 993d70a4-f6a5-4e47-a603-0b162b9fde00
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45916edbef4368c58f83426d6c73f3c692236cb9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722441"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
返回可调试此程序的所有可能的调试引擎 (DE) 的 Guid。

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
中要返回的已释放 Guid 的数目。 这还指定数组的最大大小 `rgguidEngines` 。

`rgguidEngines`\
[in，out]要填充的 DE Guid 数组。

`pceltEngines`\
弄返回返回的已释放 Guid 的实际数目。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 如果缓冲区不够大，则返回 [c + +] `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` 或 [c #] 0x8007007A。

## <a name="remarks"></a>备注
 若要确定有多少个引擎，请调用此方法一次，将 `celtBuffer` 参数设置为0，并将 `rgguidEngines` 参数设置为 null 值。 这会返回 `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` c # )  (0x8007007A，并且 `pceltEngines` 参数将返回所需的缓冲区大小。

## <a name="see-also"></a>另请参阅
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
