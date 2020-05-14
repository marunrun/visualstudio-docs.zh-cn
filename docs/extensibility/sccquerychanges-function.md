---
title: SccQuery 更改功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec335d808c287decb75bf759d5a3795d98962579
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700487"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 函数
此函数枚举给定的文件列表，提供有关通过回调函数更改每个文件的名称的信息。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccQueryChanges(
   LPVOID           pContext,
   LONG             nFiles,
   LPCSTR*          lpFileNames,
   QUERYCHANGESFUNC pfnCallback,
   LPVOID           pvCallerData
);
```

#### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文指针。

 n文件

[在]数组中`lpFileNames`的文件数。

 lpFile名称

[在]要获取有关信息的文件名数组。

 pfnCallback

[在]回调函数用于调用列表中的每个文件名（有关详细信息，请参阅[查询更改FUNC）。](../extensibility/querychangesfunc.md)

 pvCallerData

[在]将传递给回调函数的值保持不变。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|查询过程已成功完成。|
|SCC_E_PROJNOTOPEN|项目尚未在源代码管理中打开。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。|
|SCC_E_NONSPECIFICERROR|发生未指定或常规错误。|

## <a name="remarks"></a>备注
 查询的更改是命名空间：特别是重命名、添加和删除文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [错误代码](../extensibility/error-codes.md)
