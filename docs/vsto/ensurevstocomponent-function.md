---
title: EnsureVSTOComponent 函数
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cf55fc6669edd33d1b8896ee85f33ab2c04e844f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543580"
---
# <a name="ensurevstocomponent-function"></a>EnsureVSTOComponent 函数
  此 API 支持 Office 基础结构，不应在代码中直接使用。

## <a name="syntax"></a>语法

```csharp
HRESULT EnsureVSTOComponent(
    IVSTProject *pProject
);
```

#### <a name="parameters"></a>参数

|参数|说明|
|---------------|-----------------|
|*pProject*|请勿使用。|

## <a name="return-value"></a>返回值
 如果该函数成功，则它将返回**S_OK**。 如果函数失败，则返回错误代码。
