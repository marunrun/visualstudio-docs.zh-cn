---
title: IDebugProgram引擎2：：枚举可能引擎 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722441"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
返回可以调试此程序的所有可能的调试引擎 （DE） 的 GUID。

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
[在]要返回的 DE GUID 的数量。 这还指定`rgguidEngines`数组的最大大小。

`rgguidEngines`\
[进出]要填写的 DE GUID 数组。

`pceltEngines`\
[出]返回返回的实际 DE GUID 数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果缓冲区不够大`HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`，则返回 [C++] 或 [C] 0x8007007A。

## <a name="remarks"></a>备注
 为了确定有多少引擎，使用`celtBuffer`参数设置为 0 和`rgguidEngines`参数设置为 null 值调用此方法一次。 这将返回`HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`（0x8007007A 表示 C#），`pceltEngines`并且参数返回缓冲区的必要大小。

## <a name="see-also"></a>请参阅
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
