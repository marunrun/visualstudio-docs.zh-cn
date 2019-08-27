---
title: 源代码管理插件 API 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9426d4f1f673d0d82c6ce3fd84c76a1c42d8ec4e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331932"
---
# <a name="source-control-plug-in-api-functions"></a>源代码管理插件 API 函数
源控件插件 API 提供了以下函数，必须由源代码管理插件根据此 API 实现。 每个函数和语义的签名与位标志，此参考中详细介绍其他参数。

## <a name="initialization-and-housekeeping-functions"></a>初始化和日常工作，

|函数|描述|
|--------------|-----------------|
|[SccCloseProject](../extensibility/scccloseproject-function.md)|关闭项目。|
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|提示用户输入给定命令的高级选项。|
|[SccGetVersion](../extensibility/sccgetversion-function.md)|返回的版本的源代码管理插件。|
|[SccInitialize](../extensibility/sccinitialize-function.md)|初始化源代码管理插件。 被调用一次为每个插件实例。|
|[SccOpenProject](../extensibility/sccopenproject-function.md)|打开一个项目。|
|[SccSetOption](../extensibility/sccsetoption-function.md)|泛型函数，用于设置各种选项。 每个选项开始`SCC_OPT_xxx`并具有其自己定义的值集。|
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|调用后源代码管理插件需要被拔掉。|

## <a name="core-source-control-functions"></a>核心的源代码管理功能

|函数|描述|
|--------------|-----------------|
|[SccAdd](../extensibility/sccadd-function.md)|添加文件到源代码管理系统的完全限定的路径名称由指定的数组。|
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|允许用户浏览源代码管理系统中已有的文件，然后使当前项目的文件部分。|
|[SccCheckin](../extensibility/scccheckin-function.md)|检查数组中的文件。|
|[SccCheckout](../extensibility/scccheckout-function.md)|签出的文件数组。|
|[SccDiff](../extensibility/sccdiff-function.md)|显示指定完全限定的路径名和源代码管理下的版本的本地用户的文件之间的差异。|
|[SccGet](../extensibility/sccget-function.md)|检索一组文件的只读副本。|
|[SccGetEvents](../extensibility/sccgetevents-function.md)|检查调用方具有要求有关的文件的状态 (通过`SccQueryInfo`)。|
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|将导致源代码管理插件，以提示用户输入的插件有意义的项目路径。|
|[SccHistory](../extensibility/scchistory-function.md)|显示完全限定的本地文件名称的数组的历史记录。|
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|检查以了解其当前状态的文件的列表。 此外，使用`pfnPopulate`函数，以通知调用方，当文件不匹配的条件时`nCommand`。|
|[SccProperties](../extensibility/sccproperties-function.md)|显示文件的完全限定的属性。|
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|检查以了解其当前状态的完全限定文件的列表。|
|[SccRemove](../extensibility/sccremove-function.md)|从源代码管理系统中删除完全限定的文件的数组。|
|[SccRename](../extensibility/sccrename-function.md)|重命名为新名称源代码管理系统中的给定的文件。|
|[SccRunScc](../extensibility/sccrunscc-function.md)|访问源代码管理系统的功能的完整范围。|
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|撤消签出的文件数组。|

## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>支持其他功能 （的源控制插件 API 版本 1.2） 的函数
 此组函数定义的源控制插件 API 1.2 版中包含的其他功能。 它们提供更高级源代码管理功能和功能的访问。

|函数|描述|
|--------------|-----------------|
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|启动批处理操作。|
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|具有给定名称的现有父项目下创建子项目。|
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|显示由完全限定的路径名称和源代码管理数据库位置指定的本地用户的目录之间的差异。|
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|检查以了解其当前状态的完全限定目录的列表。|
|[SccEndBatch](../extensibility/sccendbatch-function.md)|结束批处理操作。|
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|返回父路径的给定的项目 （项目必须存在）。|
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|检查是否允许多次签出文件。|
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|检查是否该插件将创建 MSSCCPRJ。SCC 文件。|

## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>支持高级的功能 （版本 1.3 的源控制插件 API） 的函数
 此组函数定义的源控制插件 API 版本 1.3 中包含的其他功能。 它们提供更高级源代码管理功能和功能的访问。

|函数|描述|
|--------------|-----------------|
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|向当前项目，从源代码管理中添加的文件的列表。|
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|从没有用户界面的源代码管理检索文件的列表。|
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|检索在源代码管理中不同于本地文件的文件的列表。|
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|检索标志，用于指定受源代码管理插件的扩展的功能。|
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|检索特定于用户的选项。|
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|检查目录和一个项目或项目受源代码管理中的文件的列表。 找到每个目录和文件名称传递给回调函数。|
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|检查名称对的文件的列表所做的更改。 每个文件名传递给回调函数，其更改状态。|

## <a name="requirements"></a>要求
 标头： scc.h

 (环境 SDK 中提供常见默认情况下中包含文件夹中， *[驱动器]* \Program Files\VSIP 8.0\EnvSDK\common\inc; MSSCCI 示例中，在 VSIP 文件夹中也提供 *[驱动器]* \ProgramFiles\VSIP 8.0\MSSCCI)。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)