---
title: SetWefProcessId 方法
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1352ccc9318061be4a2f9ad2da7d63715acd6721
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978349"
---
# <a name="setwefprocessid-method"></a>SetWefProcessId 方法
  提供将运行 Web 扩展框架 (WEF) 内容的进程标识符。

## <a name="syntax"></a>语法

```csharp
HRESULT SetWefProcessId(
    [in] DWORD dwProcessId
);
```

#### <a name="parameters"></a>参数

|参数|描述|
|---------------|-----------------|
|*dwProcessId*|将用于运行 WEF 内容进程标识符。|

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 创建的 WEF 内容过程之后但在任何 WEF 内容运行之前，必须调用此方法。

 如果你想要将调试器附加到 WEF 内容进程的开发环境，环境必须在实现此方法中执行此操作。
