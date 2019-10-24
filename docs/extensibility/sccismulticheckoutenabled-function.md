---
title: SccIsMultiCheckoutEnabled 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd8fb5439ac68200ba1a3bbf3af665595528173e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721072"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 函数
此函数检查源代码管理插件是否允许对文件进行多次签出。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>参数
 pContext

中源代码管理插件上下文结构。

 pbMultiCheckout

弄指定是否为此项目启用多个签出（非零表示支持多个签出）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|检查已成功。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 IDE 进行两次检查以确定文件是否可由多个用户同时签出。 首先，源代码管理系统必须支持多个签出。 源代码管理插件可以在初始化期间通过指定 `SCC_CAP_MULTICHECKOUT` 来指定此功能。 此后，作为第二个检查，IDE 将调用此函数来确定当前项目是否支持多个签出。 如果所选项目支持多个签出，则插件将返回成功代码，并将 `pbMultiCheckout` 设置为非零（`TRUE`）或 `FALSE`。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)