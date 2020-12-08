---
title: EnsureVSTOComponent 函数
description: 了解 EnsureVSTOComponent API 如何支持 Office 基础结构，不应在代码中直接使用。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: a04cfc249efa4640df2b2e4b1c5f4b43ed52ace2
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846111"
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

|参数|描述|
|---------------|-----------------|
|*pProject*|请勿使用。|

## <a name="return-value"></a>返回值
 如果该函数成功，则它将返回 **S_OK**。 如果函数失败，则返回错误代码。
