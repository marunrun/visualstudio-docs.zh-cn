---
title: IDebugProgram2::CanDetach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0a7f8bbabbba54cc7705aedc6e7f12ca1bffc924
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187928"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
确定是否调试引擎 (DE) 可以从程序分离。

## <a name="syntax"></a>语法

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>返回值
 如果可以分离，请返回`S_OK`; 否则为返回错误代码。 返回`S_FALSE`如果 DE 无法从程序分离。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)