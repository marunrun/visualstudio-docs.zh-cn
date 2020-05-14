---
title: IDebugPort供应商3：：：Can坚持端口 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2bf436d788b517300bee9a13b66b0ca3747bcc43
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724459"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
此方法确定端口供应商是否可以在调试器的调用之间（通过将它们写入磁盘）持久化端口。

## <a name="syntax"></a>语法

```cpp
HRESULT CanPersistPorts();
```

```csharp
int CanPersistPorts();
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 `S_OK`如果可以保留端口，或`S_FALSE`指示无法保留端口。

## <a name="remarks"></a>备注
 如果端口供应商可以保留端口，则应在端口被销毁时执行此操作，然后在再次实例化端口时重新加载它们。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
