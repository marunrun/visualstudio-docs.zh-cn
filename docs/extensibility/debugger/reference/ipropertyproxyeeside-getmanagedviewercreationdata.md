---
title: IPropertyProxyEESide::GetManagedViewerCreationData |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
helpviewer_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
ms.assetid: c4eb4d60-8816-4d52-bc8d-dffd4f066499
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 435f6924948ab1273abbded633bcce757b57d9b3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329517"
---
# <a name="ipropertyproxyeesidegetmanagedviewercreationdata"></a>IPropertyProxyEESide::GetManagedViewerCreationData
为了实例化该查看器中检索有关此属性类型的查看器的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetManagedViewerCreationData(
   BSTR*                  assemName,
   IEEDataStorage**       assemBytes,
   IEEDataStorage**       assemPdb,
   BSTR*                  className,
   ASSEMBLYLOCRESOLUTION* alr,
   BOOL*                  replacementOk
);
```

```csharp
int GetManagedViewerCreationData(
   out string                     assemName,
   out IEEDataStorage             assemBytes,
   out IEEDataStorage             assemPdb,
   out string                     className,
   out enum_ASSEMBLYLOCRESOLUTION alr,
   out int                        replacementOk
);
```

## <a name="parameters"></a>参数
`assemName`\
[out]返回包含此对象的程序集的名称。

`assemBytes`\
[out]返回[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象，其中包含此对象 （如果不可用的任何字节，这是一个 null 值） 的程序集字节。

`assemPdb`\
[out]返回`IEEDataStorage`对象包含的符号存储此对象的信息 （如果没有符号存储区可用，这是一个 null 值）。

`className`\
[out]返回包含此对象的类名称。

`alr`\
[out]返回一个值从[ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)枚举，指示程序集的位置。

`replacementOk`\
[out]返回非零值 (`TRUE`) 可以更改此对象的值; 如果为零 (`FALSE`) 如果对象是只读的。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 类型可视化工具使用此方法来实例化托管的查看器。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)