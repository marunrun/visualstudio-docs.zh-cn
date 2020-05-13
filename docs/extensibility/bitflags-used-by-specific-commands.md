---
title: 特定命令使用的位标志 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740011"
---
# <a name="bitflags-used-by-specific-commands"></a>特定命令使用的比特标志
可以通过在单个值中设置一个或多个位来修改源代码管理插件 API 中许多函数的行为。 这些值称为位标志。 此处详细介绍了源代码管理插件 API 使用的各种位标志，由使用它们的函数分组。

## <a name="checked-out-flag"></a>签出标志
 可以为[SccAdd](../extensibility/sccadd-function.md)或[SccCheckin](../extensibility/scccheckin-function.md)设置此标志。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|保持文件签出状态。|

## <a name="add-flags"></a>添加标志
 这些标志由[SccAdd](../extensibility/sccadd-function.md)使用。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|源代码管理插件应自动检测文件是文本还是二进制文件。|
|`SCC_FILETYPE_TEXT`|0x01|文件类型是文本。|
|`SCC_FILETYPE_BINARY`|0x04|文件类型是二进制的。 **注意：**  `SCC_FILETYPE_TEXT`和`SCC_FILETYPE_BINARY`标志是互斥的。 完全设置一个或两个。|
|`SCC_ADD_STORELATEST`|0x02|仅存储最新版本（无增量）。|

## <a name="diff-flags"></a>差异标志
 [SccDiff](../extensibility/sccdiff-function.md)使用这些标志来定义差异操作的范围。 标志`SCC_DIFF_QD_xxx`是互斥的。 如果指定了其中任何一个，则不提供视觉反馈。 在"快速差异"（QD）中，插件不会确定文件的不同方式，仅当文件不同时。 如果未指定这些标志，则执行"视觉差异";如果未指定这些标志，则执行"视觉差异"。""。"未指定任何标志。计算并显示详细的文件差异。 如果不支持请求的 QD，插件将移动到下一个最佳插件。 例如，如果 IDE 请求校验和，而插件不支持它，则插件执行完整内容检查（仍然比可视显示快得多）。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|忽略大小写差异。|
|`SCC_DIFF_IGNORESPACE`|0x0004|忽略空白差异。 **注：** `SCC_DIFF_IGNORECASE`和`SCC_DIFF_IGNORESPACE`标志是可选的位标志。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|通过比较整个文件内容进行 QD。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|按校验和进行 QD。|
|`SCC_DIFF_QD_TIME`|0x0040|按文件日期/时间戳的 QD。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|这是用于检查所有 QD 位标志的蒙版。 它不应传递到函数中;三个 QD 位标志是互斥的。 QD 始终表示不显示 UI。|

## <a name="populatelist-flag"></a>填充列表标志
 此标志由`fOptions`参数中的[SccPopulateList](../extensibility/sccpopulatelist-function.md)使用。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE 传递的是目录，而不是文件。|

## <a name="populatedirlist-flags"></a>填充 DirList 标志
 这些标志由`fOptions`参数中的[SccpopulateDirList](../extensibility/sccpopulatedirlist-function.md)使用。

|选项值|值|说明|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|只检查目录的一个级别（这是默认值）。|
|SCC_PDL_RECURSIVE|0x0001|递归地检查每个给定目录下的所有目录。|
|SCC_PDL_INCLUDEFILES|0x0002|在检查过程中包括文件名。|

## <a name="openproject-flags"></a>打开项目标志
 这些标志由`dwFlags`参数中的[SccOpenProject](../extensibility/sccopenproject-function.md)使用。

|选项值|值|说明|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|如果源控件中不存在项目，请创建它。 如果未设置此标志，则提示用户创建项目（除非`SCC_OP_SILENTOPEN`指定了标志）。|
|SCC_OP_SILENTOPEN|0x00000002L|不要提示用户创建项目;因此，不提示用户创建项目。只是返回`SCC_E_UNKNOWNPROJECT`。|

## <a name="get-flags"></a>获取标志
 这些标志由[SccGet](../extensibility/sccget-function.md)和[SccCheckout](../extensibility/scccheckout-function.md)使用。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE 传递目录，而不是文件：获取这些目录中的所有文件。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE 正在传递目录：获取这些目录及其所有子目录。|

## <a name="noption-values"></a>nOption 值
 这些标志由`nOption`参数中的[SccSetOption](../extensibility/sccsetoption-function.md)使用。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|设置事件队列的状态。|
|`SCC_OPT_USERDATA`|0x00000002L|为`SCC_OPT_NAMECHANGEPFN`指定 用户数据。|
|`SCC_OPT_HASCANCELMODE`|0x0000003L|IDE 可以处理取消。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|为名称更改设置回调。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x0000005L|禁用源代码管理插件 UI 签出，并且不设置工作目录。|
|`SCC_OPT_SHARESUBPROJ`|0x0000006L|从源代码管理系统添加以指定工作目录。 如果关联项目是直接的后代，请尝试共享到其中。|

## <a name="dwval-bitflags"></a>dwVal 位标志
 这些标志由`dwVal`参数中的[SccSetOption](../extensibility/sccsetoption-function.md)使用。

|标志|值|说明|按`nOption`值使用|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|挂起事件队列活动。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|启用事件队列日志记录。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L|（默认）没有取消模式;如果需要，插件必须提供。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE 句柄取消。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L|（默认）可以从插件 UI 签出;请从插件 UI 中签出。工作目录已设置。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|没有插件 UI 签出，没有工作目录。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
