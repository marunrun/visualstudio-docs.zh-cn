---
title: IEEVisualizerDataProvider::CanSetObjectForVisualizer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::CanSetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::CanSetObjectForVisualizer method
ms.assetid: 70fd3c6f-2f82-43a3-993b-c1dc8aa080bf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 71fe6ed16bd1e80a13cfe97fe5ebcf84bc140da4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335613"
---
# <a name="ieevisualizerdataprovidercansetobjectforvisualizer"></a>IEEVisualizerDataProvider::CanSetObjectForVisualizer
此方法确定是否可以更新它所代表的数据对象可视化工具。

## <a name="syntax"></a>语法

```cpp
HRESULT CanSetObjectForVisualizer(
   BOOL* b
);
```

```csharp
int CanSetObjectForVisualizer(
   out int b
);
```

## <a name="parameters"></a>参数
`b`\
[out]非零值 (`TRUE`) 可更新可视化工具上的对象，如果零 (`FALSE`) 如果不能。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 对象可能不是如果例如绑定到只读的内存，则可更改。

## <a name="see-also"></a>请参阅
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)