---
title: 对字符串长度的限制 |Microsoft Docs
description: 了解由源代码管理插件 API 施加的各种函数所使用的字符串长度限制。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, restrictions on string lengths
ms.assetid: 877173d2-ca27-43b3-b1f4-8379f7c5e268
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5412e930937d029f803f5c6c2b4ddc9d396d9485
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715517"
---
# <a name="restrictions-on-string-lengths"></a>字符串长度限制
源代码管理插件 API 限制各种函数中使用的字符串的长度。

## <a name="string-length-values"></a>字符串长度值

|返回的常量|Value|
|--------------|-----------|
|`SCC_NAME_LEN`|31|
|`SCC_AUXLABEL_LEN`|31|
|`SCC_USER_LEN`|31|
|`SCC_PRJPATH_LEN`|300|

> [!NOTE]
> 长度不包括终止 `null` 。 具有 "_SIZE" 后缀而不是 "_LEN" 的其他常量都包含用于终止的空间 `null` 。

|返回的常量|Value|
|--------------|-----------|
|SCC_NAME_SIZE|32|
|SCC_AUXLABEL_SIZE|32|
|SCC_USER_SIZE|32|
|SCC_PRJPATH_SIZE|301|

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
