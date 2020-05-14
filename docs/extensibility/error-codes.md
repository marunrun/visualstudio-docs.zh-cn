---
title: 错误代码 |微软文档
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
ms.openlocfilehash: 34072f6ddbd632f83dd308c6cb63427e02bb110b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711839"
---
# <a name="error-codes"></a>错误代码
当源代码管理插件 API 函数返回错误时，它应该是以下错误代码之一。 所有错误均为负数，警告或信息错误代码为正，成功为 0。

|错误代码|值|说明|
|----------------|-----------|-----------------|
|`SCC_I_SHARESUBPROJOK`|7|插件支持分两个步骤从源代码管理中添加文件。 有关详细信息，请参阅[SccSetOption](../extensibility/sccsetoption-function.md)。|
|`SCC_I_FILEDIFFERS`|6|本地文件与源代码管理数据库中的文件不同（例如[，SccDiff](../extensibility/sccdiff-function.md)可能会返回此值）。|
|`SCC_I_RELOADFILE`|5|在源代码管理操作期间更改了本地文件;如果可能，IDE 应重新加载该文件。|
|`SCC_I_FILENOTAFFECTED`|4|该文件不受影响。|
|`SCC_I_PROJECTCREATED`|3|项目是在源代码管理操作期间创建的（例如，在指定标志时调用[SccOpenProject](../extensibility/sccopenproject-function.md)时`SCC_OP_CREATEIFNEW`）。|
|`SCC_I_OPERATIONCANCELED`|2|已取消操作。|
|`SCC_I_ADV_SUPPORT`|1|插件支持指定命令的高级选项。 有关详细信息，请参阅[SccGet命令选项](../extensibility/sccgetcommandoptions-function.md)。|
|`SCC_OK`|0|成功。|
|`SCC_E_INITIALIZEFAILED`|-1|错误：初始化失败。|
|`SCC_E_UNKNOWNPROJECT`|-2|错误：项目未知。|
|`SCC_E_COULDNOTCREATEPROJECT`|-3|错误：无法创建项目。|
|`SCC_E_NOTCHECKEDOUT`|-4|错误：未签出该文件。|
|`SCC_E_ALREADYCHECKEDOUT`|-5|错误：文件已签出。|
|`SCC_E_FILEISLOCKED`|-6|错误：文件已锁定。|
|`SCC_E_FILEOUTEXCLUSIVE`|-7|错误：文件已完全签出。|
|`SCC_E_ACCESSFAILURE`|-8|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|`SCC_E_CHECKINCONFLICT`|-9|错误：签入期间存在冲突。|
|`SCC_E_FILEALREADYEXISTS`|-10|错误：该文件已存在。|
|`SCC_E_FILENOTCONTROLLED`|-11|错误：文件不受源代码管理。|
|`SCC_E_FILEISCHECKEDOUT`|-12|错误：文件已签出。|
|`SCC_E_NOSPECIFIEDVERSION`|-13|错误：没有指定的版本。|
|`SCC_E_OPNOTSUPPORTED`|-14|错误：不支持该操作。|
|`SCC_E_NONSPECIFICERROR`|-15|非特定错误。|
|`SCC_E_OPNOTPERFORMED`|-16|错误，未执行操作。|
|`SCC_E_TYPENOTSUPPORTED`|-17|错误：源代码控制系统不支持文件的类型，例如二进制文件。|
|`SCC_E_VERIFYMERGE`|-18|文件已自动合并，但未选中，因为它正在等待用户验证。|
|`SCC_E_FIXMERGE`|-19|文件已自动合并，但由于合并冲突必须手动解决，因此尚未签入。|
|`SCC_E_SHELLFAILURE`|-20|外壳故障导致错误。|
|`SCC_E_INVALIDUSER`|-21|错误：用户无效。|
|`SCC_E_PROJECTALREADYOPEN`|-22|错误：项目已打开。|
|`SCC_E_PROJSYNTAXERR`|-23|项目语法错误。|
|`SCC_E_INVALIDFILEPATH`|-24|错误：文件路径无效。|
|`SCC_E_PROJNOTOPEN`|-25|错误：项目未打开。|
|`SCC_E_NOTAUTHORIZED`|-26|错误：用户无权执行此操作。|
|`SCC_E_FILESYNTAXERR`|-27|文件语法错误。|
|`SCC_E_FILENOTEXIST`|-28|错误，本地文件不存在。|
|`SCC_E_CONNECTIONFAILURE`|-29|错误：连接失败。|
|`SCC_E_UNKNOWNERROR`|-30|未知错误。|
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|后台获取操作当前正在进行中。|

## <a name="macros-provided-for-quick-checking"></a>用于快速检查的宏

```cpp
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)
```

## <a name="remarks"></a>备注
 当作为参数传递的本地文件不存在时，所有源代码管理插件 API 函数[（SccAdd、SccCheckin](../extensibility/sccadd-function.md)和[SccDiff](../extensibility/sccdiff-function.md)除外）都有望成功。 [SccCheckin](../extensibility/scccheckin-function.md) 例如，IDE 可能会对工作文件夹中不存在但存在于源代码管理系统中的文件发出对[SccCheckout 或](../extensibility/scccheckout-function.md) [SccUn 签出的](../extensibility/sccuncheckout-function.md)调用。 此调用将成功。 只有在工作文件夹或源代码管理系统中没有文件时，该功能才应失败。

 当工作文件夹中的文件不存在`SccAdd`时`SccCheckin`，某些函数（`SCC_E_FILENOTEXIST`如 和 ）应特别返回。 如果函数对源代码管理系统中的有效文件名进行操作，则当工作文件不存在时，其他函数应成功。

 源代码管理插件不应对工作文件夹中的文件的权限做出任何假设，即使该插件在某些操作期间将文件标记为只读。 工作文件夹中的文件可以在插件控件之外移动、删除和更改。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
