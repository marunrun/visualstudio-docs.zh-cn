---
title: 使用特定命令的位标志 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 47dd3b1c75ab7ff206714509a82449d744a02952
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333523"
---
# <a name="bitflags-used-by-specific-commands"></a>使用特定命令的位标志
可以通过设置单个值的一个或多个位修改多个源控制插件 API 中的函数的行为。 这些值称为位标志。 使用源控制插件 API 的各种位标志下面详细介绍，通过使用这些函数进行分组。

## <a name="checked-out-flag"></a>签出标志
 可以为设置此标志[SccAdd](../extensibility/sccadd-function.md)或[SccCheckin](../extensibility/scccheckin-function.md)。

|Flag|值|描述|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|保持签出该文件。|

## <a name="add-flags"></a>添加标志
 通过使用这些标志[SccAdd](../extensibility/sccadd-function.md)。

|Flag|值|描述|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|源代码管理插件会自动检测文件是否是文本或二进制文件。|
|`SCC_FILETYPE_TEXT`|0x01|文件类型为文本。|
|`SCC_FILETYPE_BINARY`|0x04|文件类型为二进制。 **注意：** `SCC_FILETYPE_TEXT`和`SCC_FILETYPE_BINARY`标志是互相排斥。 设置一个还是两者皆否。|
|`SCC_ADD_STORELATEST`|0x02|存储仅最新版本 （没有差异）。|

## <a name="diff-flags"></a>比较标志
 [SccDiff](../extensibility/sccdiff-function.md)使用这些标志来定义 diff 运算的作用域。 `SCC_DIFF_QD_xxx`标志是互相排斥。 如果指定了其中的任意一个，则没有可视反馈是获得。 在"快速 diff"(QD)，该插件不会不确定该文件的不同，仅当它是不同的方式。 如果没有指定这些标志，完成"visual diff";详细的文件差异是计算和显示。 如果不支持请求的 QD，插件将移到下一步最好的一个。 例如，如果 IDE 请求校验和，而该插件不支持它，插件会完整内容检查 （仍速度快于可视显示）。

|Flag|值|描述|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|忽略大小写差异。|
|`SCC_DIFF_IGNORESPACE`|0x0004|忽略空白差异。 **注意：** `SCC_DIFF_IGNORECASE`和`SCC_DIFF_IGNORESPACE`标志是可选的位标志。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|通过比较整个文件内容 QD。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|QD 通过校验和。|
|`SCC_DIFF_QD_TIME`|0x0040|按文件日期/时间戳 QD。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|这是用于检查所有 QD 位标志的掩码。 它不应传递到函数;三个 QD 位标志是互斥的。 QD 始终表示不显示 UI。|

## <a name="populatelist-flag"></a>PopulateList 标志
 通过使用此标志[SccPopulateList](../extensibility/sccpopulatelist-function.md)中`fOptions`参数。

|Flag|值|描述|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE 传递不是文件的目录。|

## <a name="populatedirlist-flags"></a>PopulateDirList 标志
 通过使用这些标志[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)中`fOptions`参数。

|选项值|值|描述|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|检查只有一个级别的 （这是默认值） 的目录的目录。|
|SCC_PDL_RECURSIVE|0x0001|以递归方式检查每个给定目录下的所有目录。|
|SCC_PDL_INCLUDEFILES|0x0002|在检查过程中包含文件的名称。|

## <a name="openproject-flags"></a>打开项目标志
 通过使用这些标志[SccOpenProject](../extensibility/sccopenproject-function.md)中`dwFlags`参数。

|选项值|值|描述|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|如果项目不存在在源代码管理中，创建它。 如果未设置此标志，提示用户输入项目以创建 (除非`SCC_OP_SILENTOPEN`指定标志)。|
|SCC_OP_SILENTOPEN|0x00000002L|不提示用户创建一个项目;只需返回`SCC_E_UNKNOWNPROJECT`。|

## <a name="get-flags"></a>获取标志
 通过使用这些标志[SccGet](../extensibility/sccget-function.md)并[SccCheckout](../extensibility/scccheckout-function.md)。

|Flag|值|描述|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE 传递不是文件的目录：获取这些目录中的所有文件。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE 传递目录：获取这些目录和所有子目录。|

## <a name="noption-values"></a>nOption 值
 通过使用这些标志[SccSetOption](../extensibility/sccsetoption-function.md)中`nOption`参数。

|Flag|值|描述|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|设置事件队列的状态。|
|`SCC_OPT_USERDATA`|0x00000002L|指定的用户数据`SCC_OPT_NAMECHANGEPFN`。|
|`SCC_OPT_HASCANCELMODE`|0x00000003L|IDE 可处理取消。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|设置的名称更改的回调。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x00000005L|禁用源代码管理插件 UI 签出并且未设置工作目录。|
|`SCC_OPT_SHARESUBPROJ`|0x00000006L|添加从源代码管理系统，以指定工作目录。 尝试共享到关联的项目，如果它是直接子代。|

## <a name="dwval-bitflags"></a>dwVal 位标志
 通过使用这些标志[SccSetOption](../extensibility/sccsetoption-function.md)中`dwVal`参数。

|Flag|值|描述|由`nOption`值|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|事件队列活动挂起。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|启用事件队列日志记录。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L|（默认值）有没有取消模式;如果需要，必须提供插件。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE 处理取消。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L|（默认值）确定以从插件 UI，则签出设置工作目录。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|无插件的 UI 签出，没有工作目录。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)