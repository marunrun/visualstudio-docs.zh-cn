---
title: IDebugEngine2：： SetRegistryRoot |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetRegistryRoot
helpviewer_keywords:
- IDebugEngine2::SetRegistryRoot
ms.assetid: d0d81202-8a4a-4bc3-b297-30a047c5ec60
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: beba304e846126b262c23c0fc8232f79de5fd794
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730867"
---
# <a name="idebugengine2setregistryroot"></a>IDebugEngine2::SetRegistryRoot
设置调试引擎的注册表根 (DE) 。

## <a name="syntax"></a>语法

```cpp
HRESULT SetRegistryRoot( 
   LPCOLESTR pszRegistryRoot
);
```

```csharp
int SetRegistryRoot( 
   string pszRegistryRoot
);
```

## <a name="parameters"></a>参数
`pszRegistryRoot`\
中要使用的注册表根目录。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法允许 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 指定应使用的备用注册表根以获取注册表设置，例如 "HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp"。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
