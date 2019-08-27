---
title: IDebugBinder3::GetEEService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3afc38551dc04e7fc7f6d55df81c5b7248127acd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327137"
---
# <a name="idebugbinder3geteeservice"></a>IDebugBinder3::GetEEService
此方法返回请求的服务。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEEService(
   [in] GUID        vendor,
   [in] GUID        language,
   [in] GUID        iid,
   [out] IUnknown** ppService
);
```

```csharp
Int GetEEService(
   Guid       vendor,
   Guid       language,
   Guid       iid,
   out object ppService
);
```

## <a name="parameters"></a>参数
`vendor`\
[in]`GUID` （空值是可接受） 的供应商。

`language`\
[in]`GUID` （空值是可接受） 的语言。

`iid`\
[in]`IID`要获取的服务。

`ppService`\
[out]一个指向请求的服务接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 传递`IID`有关[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)接口 (`IID_IEEVisualizerServiceProvider`) 类型可视化工具服务是否可用。 如果因此，表达式计算器可以获得[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)接口以支持类型可视化工具。 请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)有关详细信息。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)