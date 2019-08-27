---
title: 字符串长度限制 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, restrictions on string lengths
ms.assetid: 877173d2-ca27-43b3-b1f4-8379f7c5e268
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab797f76ec6f6118fe4f86a410dbfcfe1e61aa04
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334177"
---
# <a name="restrictions-on-string-lengths"></a>字符串长度限制
源控件插件 API 限制在各种不同的函数中使用的字符串的长度。

## <a name="string-length-values"></a>字符串长度值

|返回的常量|值|
|--------------|-----------|
|`SCC_NAME_LEN`|31|
|`SCC_AUXLABEL_LEN`|31|
|`SCC_USER_LEN`|31|
|`SCC_PRJPATH_LEN`|300|

> [!NOTE]
> 长度不包括终止`null`。 其他常量而不是"_LEN"的"大小) (_s"后缀与执行包含终止的空间`null`。

|返回的常量|值|
|--------------|-----------|
|SCC_NAME_SIZE|32|
|SCC_AUXLABEL_SIZE|32|
|SCC_USER_SIZE|32|
|SCC_PRJPATH_SIZE|301|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)