---
title: IDebugPortPicker::SetSite |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker::SetSite
ms.assetid: 7319e187-adfe-4b3f-aec9-521356fb5a8a
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6cd0b91491be365a4686265bd698717219df0afb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188398"
---
# <a name="idebugportpickersetsite"></a>IDebugPortPicker::SetSite
设置服务提供程序。

## <a name="syntax"></a>语法

```cpp
HRESULT SetSite(
   IServiceProvider * pSP
);
```

```csharp
public int SetSite(
   IServiceProvider pSP
);
```

#### <a name="parameters"></a>参数
 `pSP`

 [in]对服务提供程序的接口的引用。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 在调用任何其他方法之前，将调用此方法。

## <a name="see-also"></a>请参阅
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)