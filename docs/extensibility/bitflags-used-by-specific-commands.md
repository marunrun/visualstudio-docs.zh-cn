---
title: 特定命令使用的 Bitflags |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ffa1fd8bf025d665977e87dc8b88da724ade5a8b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80740011"
---
# <a name="bitflags-used-by-specific-commands"></a>特定命令使用的 Bitflags
可以通过在一个值中设置一个或多个位来修改源代码管理插件 API 中许多函数的行为。 这些值称为 bitflags。 此处详细介绍了源代码管理插件 API 使用的各种 bitflags，并按使用它们的函数分组。

## <a name="checked-out-flag"></a>已签出标志
 可以为 [SccAdd](../extensibility/sccadd-function.md) 或 [SccCheckin](../extensibility/scccheckin-function.md)设置此标志。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|使文件保持签出状态。|

## <a name="add-flags"></a>添加标志
 [SccAdd](../extensibility/sccadd-function.md)使用这些标志。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|源代码管理插件应该会自动检测文件是文本还是二进制。|
|`SCC_FILETYPE_TEXT`|0x01|文件类型为 "文本"。|
|`SCC_FILETYPE_BINARY`|0x04|文件类型为 binary。 **注意：** `SCC_FILETYPE_TEXT`和 `SCC_FILETYPE_BINARY` 标志是互斥的。   仅设置一个或两个。|
|`SCC_ADD_STORELATEST`|0x02|仅存储最新版本， (没有增量) 。|

## <a name="diff-flags"></a>差异标志
 [SccDiff](../extensibility/sccdiff-function.md)使用这些标志来定义 diff 操作的作用域。 `SCC_DIFF_QD_xxx`标志互相排斥。 如果指定了其中任何一个，则不会提供任何视觉反馈。 在 "快速差异" (QD) 中，此插件不会确定文件的不同之处，这一点仅适用于不同的情况。 如果未指定这些标志中的任何一个，则完成 "可视差异"。计算并显示详细的文件差异。 如果请求的 QD 不受支持，则该插件将移到下一个最佳方案。 例如，如果 IDE 请求校验和，并且该插件不支持，则该插件执行全文检查 (仍比视觉显示) 快得多。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|忽略大小写差异。|
|`SCC_DIFF_IGNORESPACE`|0x0004|忽略空格差异。 **注意：** `SCC_DIFF_IGNORECASE` 和 `SCC_DIFF_IGNORESPACE` 标志是可选的 bitflags。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|通过比较整个文件内容来 QD。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|按校验和 QD。|
|`SCC_DIFF_QD_TIME`|0x0040|QD by file 日期/时间戳。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|这是一个用于检查所有 QD bitflags 的掩码。 不应将其传递到函数中;这三个 QD bitflags 是互斥的。 QD 始终意味着不显示 UI。|

## <a name="populatelist-flag"></a>PopulateList 标志
 参数中的 [SccPopulateList](../extensibility/sccpopulatelist-function.md) 使用此标志 `fOptions` 。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE 传递的是目录，而不是文件。|

## <a name="populatedirlist-flags"></a>PopulateDirList 标志
 参数中的 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 使用这些标志 `fOptions` 。

|选项值|值|说明|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|仅检查目录的一级目录 (这是默认) 。|
|SCC_PDL_RECURSIVE|0x0001|以递归方式检查每个给定目录下的所有目录。|
|SCC_PDL_INCLUDEFILES|0x0002|在检查过程中包括文件名。|

## <a name="openproject-flags"></a>OpenProject 标志
 参数中的 [SccOpenProject](../extensibility/sccopenproject-function.md) 使用这些标志 `dwFlags` 。

|选项值|值|说明|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|如果项目不在源代码管理中，请创建它。 如果未设置此标志，则提示用户输入项目以创建 (除非 `SCC_OP_SILENTOPEN`) 指定标志。|
|SCC_OP_SILENTOPEN|0x00000002L|不提示用户创建项目;只需要返回 `SCC_E_UNKNOWNPROJECT` 。|

## <a name="get-flags"></a>获取标志
 这些标志由 [SccGet](../extensibility/sccget-function.md) 和 [SccCheckout](../extensibility/scccheckout-function.md)使用。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE 传递的是目录，而不是文件：获取这些目录中的所有文件。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE 正在传递目录：获取这些目录及其所有子目录。|

## <a name="noption-values"></a>nOption 值
 参数中的 [SccSetOption](../extensibility/sccsetoption-function.md) 使用这些标志 `nOption` 。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|设置事件队列的状态。|
|`SCC_OPT_USERDATA`|0x00000002L|指定的用户数据 `SCC_OPT_NAMECHANGEPFN` 。|
|`SCC_OPT_HASCANCELMODE`|0x00000003L|IDE 可以处理取消。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|设置名称更改的回叫。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x00000005L|禁用源代码管理插件 UI 签出，并且不设置工作目录。|
|`SCC_OPT_SHARESUBPROJ`|0x00000006L|添加源代码管理系统以指定工作目录。 如果是直接后代，请尝试共享到关联的项目。|

## <a name="dwval-bitflags"></a>dwVal bitflags
 参数中的 [SccSetOption](../extensibility/sccsetoption-function.md) 使用这些标志 `dwVal` 。

|标志|值|说明|用于 `nOption` 值|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|挂起事件队列活动。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|启用事件队列日志记录。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L| (默认) 没有取消模式;插件必须提供（如果需要）。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE 处理取消。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L| (默认) "确定" 以从插件 UI 签出;设置工作目录。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|无插件 UI 签出，无工作目录。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
