---
title: IPropertyProxyEESide::ResolveAssemblyRef |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::ResolveAssemblyRef
helpviewer_keywords:
- IPropertyProxyEESide::ResolveAssemblyRef
ms.assetid: 662ca0a6-dad0-4c00-a718-bb3bbc5bd9da
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3d2fd21b39e171238319c857ad0384db1d7635d7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353461"
---
# <a name="ipropertyproxyeesideresolveassemblyref"></a>IPropertyProxyEESide::ResolveAssemblyRef
确定指定的托管程序集引用的位置。

## <a name="syntax"></a>语法

```cpp
HRESULT ResolveAssemblyRef(
   BSTR*                  assemName,
   IEEDataStorage**       assemBytes,
   IEEDataStorage**       assemPdb,
   BSTR*                  assemLocation,
   ASSEMBLYLOCRESOLUTION* alr
);
```

```csharp
int ResolveAssemblyRef(
   ref string                     assemName,
   out IEEDataStorage             assemBytes,
   out IEEDataStorage             assemPdb,
   out string                     assemLocation,
   out enum_ASSEMBLYLOCRESOLUTION alr
);
```

## <a name="parameters"></a>参数
`assemName`\
[in]要解析的程序集的名称。

`assemBytes`\
[out]返回[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象，其中包含与引用关联的程序集字节。

`assemPdb`\
[out]返回`IEEDataStorage`对象包含的符号存储与此引用关联的数据。

`assemLocation`\
[out]返回此引用的路径位置。

`alr`\
[out]返回一个值从[ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)枚举，指示此引用的程序集的位置。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法通常不实现自定义表达式计算器中。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)