---
title: SccQueryChanges 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 617f07a11f92ab65f079c7d1b41773494e3d0c8b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720856"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 函数
此函数枚举给定的文件列表，并通过回调函数提供每个文件的名称更改的相关信息。

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

中源代码管理插件上下文指针。

 n

中@No__t_0 数组中的文件数。

 lpFileNames

中要获取其相关信息的文件名数组。

 pfnCallback

中为列表中的每个文件名调用的回调函数（有关详细信息，请参阅[QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) ）。

 pvCallerData

中将以不更改的形式传递给回调函数的值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|查询过程已成功完成。|
|SCC_E_PROJNOTOPEN|未在源代码管理中打开该项目。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。|
|SCC_E_NONSPECIFICERROR|出现未指定的错误或常规错误。|

## <a name="remarks"></a>备注
 查询的更改是命名空间：具体而言，即重命名、添加和删除文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [错误代码](../extensibility/error-codes.md)