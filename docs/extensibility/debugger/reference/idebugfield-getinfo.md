---
title: IDebugField：： GetInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetInfo
helpviewer_keywords:
- IDebugField::GetInfo method
ms.assetid: 7d508200-89ce-400f-a8ea-f28e7610cb2b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1b3251db3426f87901ca0768800feaa36fef5373
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728841"
---
# <a name="idebugfieldgetinfo"></a>IDebugField::GetInfo
此方法获取有关字段的可显示信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInfo( 
   FIELD_INFO_FIELDS dwFields,
   FIELD_INFO* pFieldInfo
);
```

```csharp
int GetInfo(
   enum_FIELD_INFO_FIELDS dwFields,
   FIELD_INFO[] pFieldInfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
中选择要显示的信息 [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md) 常量的组合。 如果字段表示符号，则这通常是符号名称和类型。

`pFieldInfo`\
弄返回所提供的 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 结构中的信息。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
