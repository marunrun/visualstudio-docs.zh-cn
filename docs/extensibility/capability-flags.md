---
title: 功能标志 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0d8f14be1922bb82c2a169e38f370c11231f59f0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321134"
---
# <a name="capability-flags"></a>功能标志
SCC_CAP_*xxx*标志是用来指示源代码管理插件的功能的位标志。 SCC_EXCAP_*xxx*标志是增量标志，指示扩展的功能并解析为整数值。

|功能代码|值|描述|
|---------------------|-----------|-----------------|
|`SCC_CAP_REMOVE`|0x00000001L|支持[SccRemove](../extensibility/sccremove-function.md)和命令。|
|`SCC_CAP_RENAME`|0x00000002L|支持[SccRename](../extensibility/sccrename-function.md)和命令。|
|`SCC_CAP_DIFF`|0x00000004L|支持[SccDiff](../extensibility/sccdiff-function.md)和命令。|
|`SCC_CAP_HISTORY`|0x00000008L|支持[SccHistory](../extensibility/scchistory-function.md)和命令。|
|`SCC_CAP_PROPERTIES`|0x00000010L|支持[SccProperties](../extensibility/sccproperties-function.md)和命令。|
|`SCC_CAP_RUNSCC`|0x00000020L|支持[SccRunScc](../extensibility/sccrunscc-function.md)和命令。|
|`SCC_CAP_GETCOMMANDOPTIONS`|0x00000040L|支持[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)和命令。|
|`SCC_CAP_QUERYINFO`|0x00000080L|支持[SccQueryInfo](../extensibility/sccqueryinfo-function.md)和命令。|
|`SCC_CAP_GETEVENTS`|0x00000100L|支持[SccGetEvents](../extensibility/sccgetevents-function.md)和命令。|
|`SCC_CAP_GETPROJPATH`|0x00000200L|支持[SccGetProjPath](../extensibility/sccgetprojpath-function.md)和命令。|
|`SCC_CAP_ADDFROMSCC`|0x00000400L|支持[SccAddFromScc](../extensibility/sccaddfromscc-function.md)和命令。|
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|支持在签出注释。|
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|支持在签入上一条注释。|
|`SCC_CAP_COMMENTADD`|0x00002000L|在添加支持注释。|
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|支持在删除上一条注释。|
|`SCC_CAP_TEXTOUT`|0x00008000L|将文本写入到 IDE 提供输出函数。|
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|将文件而无需增量存储的支持。|
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|支持多个文件历史记录。|
|`SCC_CAP_IGNORECASE`|0x00800000L|支持不区分大小写的文件比较。|
|`SCC_CAP_IGNORESPACE`|0x01000000L|支持文件比较会忽略空白区域。|
|`SCC_CAP_POPULATELIST`|0x02000000L|支持查找额外文件。|
|`SCC_CAP_COMMENTPROJECT`|0x04000000L|支持注释上的创建项目。|
|`SCC_CAP_DIFFALWAYS`|0x10000000L|如果在控件中的所有状态支持差异。|
|`SCC_CAP_GET_NOUI`|0x20000000L|插件不支持 UI 为 Get，但可能仍需调用 IDE [SccGet](../extensibility/sccget-function.md)。|
|`SCC_CAP_REENTRANT`|0x40000000L|插件是可重入且是线程安全。 在版本 1.0 中，任何插件已不假定为可重入且是线程安全。 如果插件的 1.1 设置此位，被可以同时打开多个项目的主机。|

## <a name="capability-bits-added-in-version-12"></a>在版本 1.2 中添加功能位

|功能代码|值|描述|
|---------------------|-----------|-----------------|
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|支持[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)。|
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|支持[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)。|
|`SCC_CAP_BATCH`|0x00040000L|支持[SccBeginBatch](../extensibility/sccbeginbatch-function.md)并[SccEndBatch](../extensibility/sccendbatch-function.md)。|
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|支持[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)。|
|`SCC_CAP_DIRECTORYDIFF`|0x00100000L|支持[SccDirDiff](../extensibility/sccdirdiff-function.md)。|
|`SCC_CAP_MULTICHECKOUT`|0x08000000L|支持多个签出文件并[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)。|
|`SCC_CAP_SCCFILE`|0x80000000L|支持*MSSCCPRJ.SCC*文件 （取决于用户/管理员或替代） 和[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)。|

## <a name="capability-bits-added-in-version-13"></a>在版本 1.3 中添加功能位
 这些标志传递到一次一个地[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)函数来确定是否支持此功能。

|扩展的功能的代码|值|描述|
|------------------------------|-----------|-----------------|
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|支持`SCC_CHECKOUT_LOCALVER`签出的选项。|
|`SCC_EXCAP_BACKGROUND_GET`|2|支持[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)。|
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|支持[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)。|
|`SCC_EXCAP_POPULATELIST_DIR`|4|支持查找额外的目录。|
|`SCC_EXCAP_QUERYCHANGES`|5|枚举文件更改的支持。|
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|支持[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)。|
|`SCC_EXCAP_GET_USER_OPTIONS`|7|支持[SccGetUserOption](../extensibility/sccgetuseroption-function.md)。|
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|支持多个线程上调用 SccQueryInfo。|
|`SCC_EXCAP_REMOVE_DIR`|9|支持 SccRemoveDir 函数。|
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|可以删除签出文件。|
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|可以重命名签出的文件。|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)