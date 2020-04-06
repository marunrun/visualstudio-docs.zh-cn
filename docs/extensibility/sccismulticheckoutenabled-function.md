---
title: SccIs 多检出功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e91eb566a820f4fe11ceb629643e1815dcb87a8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700586"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 函数
此函数检查源代码管理插件是否允许在文件上进行多次签出。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文结构。

 pb 多签出

[出]指定是否为此项目启用了多个签出（非零表示支持多个签出）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|检查成功。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特异性故障。|

## <a name="remarks"></a>备注
 IDE 进行两次检查，以确定是否可以由多个用户同时签出文件。 首先，源代码管理系统必须支持多个签出。 源代码管理插件可以通过指定 在`SCC_CAP_MULTICHECKOUT`初始化期间指定此功能。 此后，作为第二次检查，IDE 调用此函数以确定当前项目是否支持多个签出。 如果所选项目支持多个签出，插件将返回一个成功代码，并将其设置`pbMultiCheckout`为非零 （）`TRUE`或`FALSE`。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
