---
title: GetVstoSolutionMetadata 函数
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
ms.openlocfilehash: d7714e78e897e6c8b391a6c30e9a548671ce80c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62796036"
---
# <a name="getvstosolutionmetadata-function"></a>GetVstoSolutionMetadata 函数
  此 API 支持 Office 基础结构，不应在代码中直接使用。

## <a name="syntax"></a>语法

```csharp
HRESULT WINAPI GetVstoSolutionMetadata(
    LPCWSTR lpwszSolutionMetadataKey,
    ISolutionMetadata** ppSolutionInfo
);
```

### <a name="parameters"></a>参数

|参数|描述|
|---------------|-----------------|
|*lpwszSolutionMetadataKey*|不要使用。|
|*ppSolutionInfo*|不要使用。|

## <a name="return-value"></a>返回值
 如果函数成功，它将返回 **，则为 S_OK**。 如果函数失败，则返回错误代码。
