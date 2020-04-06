---
title: IPropertyProxyEEside：获取托管查看器创建数据 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
helpviewer_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
ms.assetid: c4eb4d60-8816-4d52-bc8d-dffd4f066499
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e72922b348c8744f10037e199e93f735ff4be8e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714967"
---
# <a name="ipropertyproxyeesidegetmanagedviewercreationdata"></a>IPropertyProxyEESide::GetManagedViewerCreationData
检索有关此属性类型的查看器的信息，以便实例化该查看器。

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
[出]返回保存此对象的程序集的名称。

`assemBytes`\
[出]返回包含此对象的程序集字节的[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象（如果没有可用的字节，则为空值）。

`assemPdb`\
[出]返回包含`IEEDataStorage`此对象符号存储信息的对象（如果没有可用的符号存储，则为空值）。

`className`\
[出]返回包含此对象的类名称。

`alr`\
[出]从["装配"](../../../extensibility/debugger/reference/assemblylocresolution.md)枚举中返回一个值，指示程序集的位置。

`replacementOk`\
[出]如果可以更改此`TRUE`对象的值，则返回非零 （ ）， 如果可以更改此对象的值。如果对象`FALSE`是只读的，则为零 （ ）。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法由类型可视化器用于实例化托管查看器。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
