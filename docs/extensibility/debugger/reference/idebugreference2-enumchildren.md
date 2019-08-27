---
title: IDebugReference2::EnumChildren |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::EnumChildren
helpviewer_keywords:
- IDebugReference2::EnumChildren
ms.assetid: 35b3c2f3-69f4-4013-b555-f847221f62e8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 432a3c25722ae7adb966efa6998c42680bd60307
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335778"
---
# <a name="idebugreference2enumchildren"></a>IDebugReference2::EnumChildren
获取引用的选定子级的列表。 留待将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumChildren ( 
   DEBUGREF_INFO_FLAGS        dwFields,
   DWORD                      dwRadix,
   DBG_ATTRIB_FLAGS           dwAttribFilter,
   LPCOLESTR                  pszNameFilter,
   DWORD                      dwTimeout,
   IEnumDebugReferenceInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGREF_INFO_FLAGS     dwFields,
   uint                         dwRadix,
   enum_DBG_ATTRIB_FLAGS        dwAttribFilter,
   string                       pszNameFilter,
   uint                         dwTimeout,
   out IEnumDebugReferenceInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]中的标志的组合[DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)枚举，用于指定哪些字段中枚举[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构是必填。

`dwRadix`\
[in]用于格式化数值的任何信息的基数。

`dwAttribFilter`\
[in]中的标志的组合[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)作为筛选器结合使用的枚举`pszNameFilter`参数选择的结构是要枚举。

`pszNameFilter`\
[in]一个字符串，指定筛选器，例如"MyX"，与结合使用`dwAttribFilter`参数选择要枚举的结构。

`dwTimeout`\
[in]最大时间 （毫秒），此方法返回前等待。 使用`INFINITE`无限期等待。

`ppEnum`\
[out]返回[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)对象，其中包含请求的子属性的列表。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)