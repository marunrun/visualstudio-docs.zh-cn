---
title: IDebugEngine2::SetRegistryRoot |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetRegistryRoot
helpviewer_keywords:
- IDebugEngine2::SetRegistryRoot
ms.assetid: d0d81202-8a4a-4bc3-b297-30a047c5ec60
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f30a2fe4a239b76d9eb984cdc4cea6485b8dd5d5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352507"
---
# <a name="idebugengine2setregistryroot"></a>IDebugEngine2::SetRegistryRoot
设置调试引擎 (DE) 的注册表根目录。

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
[in]要使用的注册表根。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法允许[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]来指定备用的注册表根目录，DE 应使用以获得其他注册表设置; 例如，"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp"。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)