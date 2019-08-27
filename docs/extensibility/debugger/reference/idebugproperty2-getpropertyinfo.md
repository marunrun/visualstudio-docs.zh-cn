---
title: IDebugProperty2::GetPropertyInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetPropertyInfo
helpviewer_keywords:
- IDebugProperty2::GetPropertyInfo
ms.assetid: 39d6e942-df72-4c84-a5d9-a386d112714c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 96d291ed86d285316445e40e85c30806f3a42c83
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342916"
---
# <a name="idebugproperty2getpropertyinfo"></a>IDebugProperty2::GetPropertyInfo
获取[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)描述的属性的结构。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPropertyInfo ( 
   DEBUGPROP_INFO_FLAGS dwFields,
   DWORD                nRadix,
   DWORD                dwTimeout,
   IDebugReference2**   rgpArgs,
   DWORD                dwArgCount,
   DEBUG_PROPERTY_INFO* pPropertyInfo
);
```

```cpp
int GetPropertyInfo ( 
   enum_DEBUGPROP_INFO_FLAGS dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_PROPERTY_INFO[]     pPropertyInfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]中值的组合[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举，用于指定哪些字段是要填写`pPropertyInfo`结构。

`nRadix`\
[in]用于格式化数值的任何信息的基数。

`dwTimeout`\
[in]指定以毫秒为单位，此方法返回前等待的最长时间。 使用`INFINITE`无限期等待。

`rgpArgs`\
[in、 out]保留供将来使用;设置为 null 值。

`dwArgCount`\
[in]保留供将来使用;设置为零。

`pPropertyInfo`\
[out]一个[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)填充属性的说明的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)