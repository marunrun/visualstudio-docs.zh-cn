---
title: SccGetUserOption 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetUserOption
helpviewer_keywords:
- SccGetUserOption function
ms.assetid: 17863747-1901-4c53-a2b3-ed996085e120
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc7b68df3331c1240ad833048940e656da034ccf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700687"
---
# <a name="sccgetuseroption-function"></a>SccGetUserOption 函数
此功能检索各种特定于用户的选项。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetUserOption(
   LPVOID pContext,
   LONG nOption,
   LPLONG lpVal
);
```

#### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文指针。

 nOption

[在]要检索的选项（有关可能的选项，请参阅备注）。

 lpVal

[出]与选项关联的值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功检索选项。|
|SCC_E_OPNOTSUPPORTED|不支持选项。|
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|

## <a name="remarks"></a>备注
 此命令支持以下选项：

|用户选项|描述|
|-----------------|-----------------|
|`SCC_USEROPT_CHECKOUT_LOCALVER`|确定用户是否要签出文件的本地版本。 `lpVal`已分配`SCC_USEROPT_COLV_YES`（用户希望签出本地文件）或`SCC_USEROPT_COLV_NO`。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [错误代码](../extensibility/error-codes.md)
