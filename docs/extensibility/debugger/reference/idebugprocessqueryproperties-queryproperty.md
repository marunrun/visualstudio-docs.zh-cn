---
title: IDebugProcessQueryProperties::QueryProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties::QueryProperty
ms.assetid: 9a91707d-a590-44ef-b122-69d9816a7a79
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b1a5a57cb0aa2e5173886b36a58da19a70aae707
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311578"
---
# <a name="idebugprocessquerypropertiesqueryproperty"></a>IDebugProcessQueryProperties::QueryProperty
此方法查询的调试过程的指定的属性值。

## <a name="syntax"></a>语法

```cpp
HRESULT QueryProperty(
   PROCESS_PROPERTY_TYPE  dwPropType,
   VARIANT               *pvarPropValue);
```

```csharp
int QueryProperty(
   enum_PROCESS_PROPERTY_TYPE dwPropType,
   out object                 pvarPropValue);
```

## <a name="parameters"></a>参数
`dwPropType`\
[in]查询的属性的定义。 该属性的值有：

- PROCESS_PROPERTY_COMMAND_LINE = 1

- PROCESS_PROPERTY_CURRENT_DIRECTORY = 2

- PROCESS_PROPERTY_ENVIRONMENT_VARIABLES = 3

`pvarPropValue`\
[out]属性的值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 很少使用此方法。

## <a name="see-also"></a>请参阅
- [IDebugProcessQueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties.md)