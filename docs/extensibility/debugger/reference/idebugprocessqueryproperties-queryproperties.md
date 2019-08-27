---
title: IDebugProcessQueryProperties::QueryProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties::QueryProperties
ms.assetid: 976a9962-b689-45bb-afb6-16b2c5dbc3b8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a26cbb1781561b6fb4d54da3cfaea9a9fbae7699
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311586"
---
# <a name="idebugprocessquerypropertiesqueryproperties"></a>IDebugProcessQueryProperties::QueryProperties
此方法查询的调试过程指定的属性值。

## <a name="syntax"></a>语法

```cpp
HRESULT QueryProperties(
   ULONG                  celt,
   PROCESS_PROPERTY_TYPE *rgdwPropTypes,
   VARIANT               *rgtPropValues);
```

```csharp
int QueryProperties(
   uint                       celt,
   enum_PROCESS_PROPERTY_TYPE rgdwPropTypes,
   out object[ ]              rgtPropValues);
```

## <a name="parameters"></a>参数
`celt`\
[in]包含的属性定义和属性值的数组的大小。

`dwPropType`\
[in]一个数组，包含查询的属性的定义。 可能的值为：

- PROCESS_PROPERTY_COMMAND_LINE = 1

- PROCESS_PROPERTY_CURRENT_DIRECTORY = 2

- PROCESS_PROPERTY_ENVIRONMENT_VARIABLES = 3

`pvarPropValue`\
[out]包含属性值的数组。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 很少使用此方法。

## <a name="see-also"></a>请参阅
- [IDebugProcessQueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties.md)