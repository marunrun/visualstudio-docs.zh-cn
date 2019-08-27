---
title: IDebugProgramNode2::GetEngineInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetEngineInfo
helpviewer_keywords:
- IDebugProgramNode2::GetEngineInfo
ms.assetid: 664e7fe5-9100-4b7d-9dc5-e5a4dd0d0451
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1e3e24c2c326f7ebc7427da3804f17f1f75aeef4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205732"
---
# <a name="idebugprogramnode2getengineinfo"></a>IDebugProgramNode2::GetEngineInfo
获取名称和标识符的运行程序的调试引擎 (DE)。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineInfo ( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo(
   out string pbstrEngine,
   out Guid pguidEngine
);
```

#### <a name="parameters"></a>Parameters
 `pbstrEngine`

 [out]返回的运行程序 DE 名称 (C++-特定： 这可以是 null 指针，该值指示调用方不希望该引擎的名称)。

 `pguidEngine`

 [out]返回运行程序 DE 的全局唯一标识符 (C++-特定： 这可以是 null 指针，该值指示调用方不感兴趣的引擎的 GUID)。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)