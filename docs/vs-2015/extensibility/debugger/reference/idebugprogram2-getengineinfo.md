---
title: IDebugProgram2::GetEngineInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetEngineInfo
helpviewer_keywords:
- IDebugProgram2::GetEngineInfo
ms.assetid: 3a4f2dc0-e082-4d8d-aeaf-463ab09d279b
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b7a866730be3e6dfce8d68c655eb1f1b4d3f4da
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148712"
---
# <a name="idebugprogram2getengineinfo"></a>IDebugProgram2::GetEngineInfo
获取名称和运行此程序的调试引擎 (DE) 的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineInfo( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo( 
   out string pbstrEngine,
   out GUID   pguidEngine
);
```

#### <a name="parameters"></a>Parameters
 `pbstrEngine`

 [out]返回 DE 运行此程序的名称。

 `pguidEngine`

 [out]返回运行此程序 DE 的 GUID。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 每个 DE 定义其自己的标识的 GUID。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)