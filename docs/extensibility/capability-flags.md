---
title: 功能标志 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9660cbe5a18e82974858fa4d923a38fc73e773f2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739871"
---
# <a name="capability-flags"></a>功能标志
SCC_CAP_*xxx* 标志是用于指示源代码管理插件的功能的位标志。 SCC_EXCAP_*xxx* 标志是增量标志，指示扩展功能并解析为整数值。

|功能代码|值|说明|
|---------------------|-----------|-----------------|
|`SCC_CAP_REMOVE`|0x00000001L|支持 [SccRemove](../extensibility/sccremove-function.md) 和命令。|
|`SCC_CAP_RENAME`|0x00000002L|支持 [SccRename](../extensibility/sccrename-function.md) 和命令。|
|`SCC_CAP_DIFF`|0x00000004L|支持 [SccDiff](../extensibility/sccdiff-function.md) 和命令。|
|`SCC_CAP_HISTORY`|0x00000008L|支持 [SccHistory](../extensibility/scchistory-function.md) 和命令。|
|`SCC_CAP_PROPERTIES`|0x00000010L|支持 [SccProperties](../extensibility/sccproperties-function.md) 和命令。|
|`SCC_CAP_RUNSCC`|0x00000020L|支持 [SccRunScc](../extensibility/sccrunscc-function.md) 和命令。|
|`SCC_CAP_GETCOMMANDOPTIONS`|0x00000040L|支持 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) 和命令。|
|`SCC_CAP_QUERYINFO`|0x00000080L|支持 [SccQueryInfo](../extensibility/sccqueryinfo-function.md) 和命令。|
|`SCC_CAP_GETEVENTS`|0x00000100L|支持 [SccGetEvents](../extensibility/sccgetevents-function.md) 和命令。|
|`SCC_CAP_GETPROJPATH`|0x00000200L|支持 [SccGetProjPath](../extensibility/sccgetprojpath-function.md) 和命令。|
|`SCC_CAP_ADDFROMSCC`|0x00000400L|支持 [SccAddFromScc](../extensibility/sccaddfromscc-function.md) 和命令。|
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|在签出时支持注释。|
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|支持签入注释。|
|`SCC_CAP_COMMENTADD`|0x00002000L|支持添加注释。|
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|支持删除时的注释。|
|`SCC_CAP_TEXTOUT`|0x00008000L|将文本写入 IDE 提供的输出函数。|
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|支持存储无增量文件的文件。|
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|支持多个文件历史记录。|
|`SCC_CAP_IGNORECASE`|0x00800000L|支持不区分大小写的文件比较。|
|`SCC_CAP_IGNORESPACE`|0x01000000L|支持忽略空格的文件比较。|
|`SCC_CAP_POPULATELIST`|0x02000000L|支持查找额外文件。|
|`SCC_CAP_COMMENTPROJECT`|0x04000000L|支持有关创建项目的注释。|
|`SCC_CAP_DIFFALWAYS`|0x10000000L|如果在控件下，则支持所有状态的差异。|
|`SCC_CAP_GET_NOUI`|0x20000000L|插件不支持 Get 的 UI，但 IDE 仍可调用 [SccGet](../extensibility/sccget-function.md)。|
|`SCC_CAP_REENTRANT`|0x40000000L|插件是可重入和线程安全的。 在版本1.0 中，未假定插件可重入和线程安全。 如果1.1 插件设置此位，则允许主机并行打开多个项目。|

## <a name="capability-bits-added-in-version-12"></a>在版本1.2 中添加的功能位

|功能代码|值|说明|
|---------------------|-----------|-----------------|
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|支持 [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)。|
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|支持 [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)。|
|`SCC_CAP_BATCH`|0x00040000L|支持 [SccBeginBatch](../extensibility/sccbeginbatch-function.md) 和 [SccEndBatch](../extensibility/sccendbatch-function.md)。|
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|支持 [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)。|
|`SCC_CAP_DIRECTORYDIFF`|0x00100000L|支持 [SccDirDiff](../extensibility/sccdirdiff-function.md)。|
|`SCC_CAP_MULTICHECKOUT`|0x08000000L|支持对文件和 [SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)多次签出。|
|`SCC_CAP_SCCFILE`|0x80000000L|支持 *mssccprj.scc* 文件 (受制于用户/管理员覆盖) 和 [SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)。|

## <a name="capability-bits-added-in-version-13"></a>在版本1.3 中添加的功能位
 这些标志一次传递到 [SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md) 函数，以确定是否支持此功能。

|扩展的功能代码|值|说明|
|------------------------------|-----------|-----------------|
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|支持 `SCC_CHECKOUT_LOCALVER` 用于签出的选项。|
|`SCC_EXCAP_BACKGROUND_GET`|2|支持 [SccBackgroundGet](../extensibility/sccbackgroundget-function.md)。|
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|支持 [SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)。|
|`SCC_EXCAP_POPULATELIST_DIR`|4|支持查找其他目录。|
|`SCC_EXCAP_QUERYCHANGES`|5|支持枚举文件更改。|
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|支持 [SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)。|
|`SCC_EXCAP_GET_USER_OPTIONS`|7|支持 [SccGetUserOption](../extensibility/sccgetuseroption-function.md)。|
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|支持在多个线程上调用 SccQueryInfo。|
|`SCC_EXCAP_REMOVE_DIR`|9|支持 SccRemoveDir 函数。|
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|可删除已签出的文件。|
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|可重命名已签出的文件。|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
