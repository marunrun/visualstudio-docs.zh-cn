---
title: 错误代码 |Microsoft Docs
description: 本文包含源代码管理插件 API 函数的错误代码、值和说明的列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- error codes, source control plug-ins
- source control plug-ins, error codes
- errors [Visual Studio SDK]
ms.assetid: d9cbd1c4-719b-467a-8100-333c1e146d3b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a77f869936531dbc41cc3bd1d9b510bf44c35cec
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994714"
---
# <a name="error-codes"></a>错误代码
当源代码管理插件 API 函数返回错误时，它应为以下错误代码之一。 所有错误都是否定的、警告或信息错误代码为正值，成功为0。

|错误代码|值|说明|
|----------------|-----------|-----------------|
|`SCC_I_SHARESUBPROJOK`|7|插件支持通过两个步骤从源代码管理添加文件。 有关详细信息，请参阅 [SccSetOption](../extensibility/sccsetoption-function.md)。|
|`SCC_I_FILEDIFFERS`|6|本地文件不同于源代码管理数据库中的文件 (例如， [SccDiff](../extensibility/sccdiff-function.md) 可能会将此值返回) 。|
|`SCC_I_RELOADFILE`|5|在源代码管理操作期间更改了本地文件;IDE 应重新加载文件（如果可能）。|
|`SCC_I_FILENOTAFFECTED`|4|此文件不受影响。|
|`SCC_I_PROJECTCREATED`|3|项目是在源代码管理操作期间创建的 (例如，在调用 [SccOpenProject](../extensibility/sccopenproject-function.md) 时，如果 `SCC_OP_CREATEIFNEW`) 指定标志。|
|`SCC_I_OPERATIONCANCELED`|2|已取消操作。|
|`SCC_I_ADV_SUPPORT`|1|插件支持指定命令的高级选项。 有关详细信息，请参阅 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)。|
|`SCC_OK`|0|成功。|
|`SCC_E_INITIALIZEFAILED`|-1|错误：初始化失败。|
|`SCC_E_UNKNOWNPROJECT`|-2|错误：项目未知。|
|`SCC_E_COULDNOTCREATEPROJECT`|-3|错误：无法创建项目。|
|`SCC_E_NOTCHECKEDOUT`|-4|错误：文件未签出。|
|`SCC_E_ALREADYCHECKEDOUT`|-5|错误：该文件已签出。|
|`SCC_E_FILEISLOCKED`|-6|错误：文件被锁定。|
|`SCC_E_FILEOUTEXCLUSIVE`|-7|错误：文件以独占方式签出。|
|`SCC_E_ACCESSFAILURE`|-8|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|`SCC_E_CHECKINCONFLICT`|-9|错误：签入过程中出现冲突。|
|`SCC_E_FILEALREADYEXISTS`|-10|错误：该文件已存在。|
|`SCC_E_FILENOTCONTROLLED`|-11|错误：文件不受源代码管理。|
|`SCC_E_FILEISCHECKEDOUT`|rsync-3.0.6-12.el6.x86|错误：该文件已签出。|
|`SCC_E_NOSPECIFIEDVERSION`|-13|错误：没有指定的版本。|
|`SCC_E_OPNOTSUPPORTED`|-14|错误：操作不受支持。|
|`SCC_E_NONSPECIFICERROR`|checks.-15-minutes|不特定的错误。|
|`SCC_E_OPNOTPERFORMED`|-16|错误，未执行该操作。|
|`SCC_E_TYPENOTSUPPORTED`|-17|错误：源代码管理系统不支持文件的类型，例如，二进制。|
|`SCC_E_VERIFYMERGE`|-18|文件已自动合并，但尚未选中，因为它正在等待用户验证。|
|`SCC_E_FIXMERGE`|-19|由于必须手动解决的合并冲突，文件已自动合并但尚未签入。|
|`SCC_E_SHELLFAILURE`|-20|由于 shell 故障导致的错误。|
|`SCC_E_INVALIDUSER`|-21|错误：用户无效。|
|`SCC_E_PROJECTALREADYOPEN`|-22|错误：该项目已打开。|
|`SCC_E_PROJSYNTAXERR`|-23|项目语法错误。|
|`SCC_E_INVALIDFILEPATH`|-24|错误：文件路径无效。|
|`SCC_E_PROJNOTOPEN`|-25|错误：项目未打开。|
|`SCC_E_NOTAUTHORIZED`|-26|错误：用户无权执行此操作。|
|`SCC_E_FILESYNTAXERR`|-27|文件语法错误。|
|`SCC_E_FILENOTEXIST`|-28-preview|错误，本地文件不存在。|
|`SCC_E_CONNECTIONFAILURE`|-29|错误：连接失败。|
|`SCC_E_UNKNOWNERROR`|-30|未知错误。|
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|后台获取操作当前正在进行。|

## <a name="macros-provided-for-quick-checking"></a>为快速检查提供的宏

```cpp
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)
```

## <a name="remarks"></a>备注
 如果作为参数传递的本地文件在工作文件夹中不存在，则所有源代码管理插件 API 函数 (除 [SccAdd](../extensibility/sccadd-function.md)、 [SccCheckin](../extensibility/scccheckin-function.md)和 [SccDiff](../extensibility/sccdiff-function.md)) 应成功。 例如，IDE 可能会对工作文件夹中不存在但存在于源代码管理系统中的文件发出对 [SccCheckout](../extensibility/scccheckout-function.md) 或 [SccUncheckout](../extensibility/sccuncheckout-function.md) 的调用。 此调用将成功。 仅当工作文件夹或源代码管理系统中没有任何文件时，该函数才会失败。

 `SccAdd` `SccCheckin` `SCC_E_FILENOTEXIST` 当工作文件夹中的文件不存在时，某些函数（如和）应特别返回。 如果工作文件不存在，则其他函数应成功，前提是函数在源代码管理系统中对有效的文件名执行操作。

 源代码管理插件不应与工作文件夹中的文件的权限有关，即使插件在某些操作期间已将文件标记为只读。 可以移动、删除工作文件夹中的文件，还可以在插件的控件之外对其进行更改。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
