---
title: 源代码管理插件 API 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 02e2c7ee92ab138de7bee0d58835898f3bd0a58b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160620"
---
# <a name="source-control-plug-in-api-functions"></a>源代码管理插件 API 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

源代码管理插件 API 提供以下函数，这些函数必须根据此 API 由源代码管理插件实现。 此参考中详细介绍了每个函数的签名以及与位标志和其他参数关联的语义。  
  
## <a name="initialization-and-housekeeping-functions"></a>初始化和内务处理功能  
  
|函数|说明|  
|--------------|-----------------|  
|[SccCloseProject](../extensibility/scccloseproject-function.md)|关闭项目。|  
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|提示用户输入给定命令的高级选项。|  
|[SccGetVersion](../extensibility/sccgetversion-function.md)|返回源代码管理插件的版本。|  
|[SccInitialize](../extensibility/sccinitialize-function.md)|初始化源代码管理插件。 对于插件的每个实例，将调用该方法一次。|  
|[SccOpenProject](../extensibility/sccopenproject-function.md)|打开项目。|  
|[SccSetOption](../extensibility/sccsetoption-function.md)|用于设置各种选项的泛型函数。 每个选项都以开头 `SCC_OPT_xxx` ，并且具有其自己定义的值集。|  
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|当需要拔出源代码管理插件时调用一次。|  
  
## <a name="core-source-control-functions"></a>核心源代码管理函数  
  
|函数|说明|  
|--------------|-----------------|  
|[SccAdd](../extensibility/sccadd-function.md)|将由完全限定的路径名称指定的文件数组添加到源代码管理系统中。|  
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|允许用户浏览源控制系统中已存在的文件，然后将这些文件设置为当前项目的一部分。|  
|[SccCheckin](../extensibility/scccheckin-function.md)|检查文件的数组。|  
|[SccCheckout](../extensibility/scccheckout-function.md)|签出文件的数组。|  
|[SccDiff](../extensibility/sccdiff-function.md)|显示由完全限定的路径名称和源代码管理下的版本指定的本地用户文件之间的差异。|  
|[SccGet](../extensibility/sccget-function.md)|检索一组文件的只读副本。|  
|[SccGetEvents](../extensibility/sccgetevents-function.md)|通过) 检查调用方已要求 (的文件的状态 `SccQueryInfo` 。|  
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|导致源代码管理插件提示用户提供对插件有意义的项目路径。|  
|[SccHistory](../extensibility/scchistory-function.md)|显示完全限定的本地文件名的数组的历史记录。|  
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|检查文件列表的当前状态。 此外， `pfnPopulate` 如果文件与的条件不匹配，则使用函数通知调用方 `nCommand` 。|  
|[SccProperties](../extensibility/sccproperties-function.md)|显示完全限定文件的属性。|  
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|检查当前状态的完全限定文件的列表。|  
|[SccRemove](../extensibility/sccremove-function.md)|从源控制系统中删除完全限定文件的数组。|  
|[SccRename](../extensibility/sccrename-function.md)|在源代码管理系统中将给定的文件重命名为新名称。|  
|[SccRunScc](../extensibility/sccrunscc-function.md)|访问源代码管理系统的各种功能。|  
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|撤消文件数组的签出。|  
  
## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>支持其他功能 (源代码管理插件 API 版本1.2 的函数)   
 此组函数定义源代码管理插件 API 版本1.2 中包含的附加功能。 它们提供对更高级源代码管理特性和功能的访问。  
  
|函数|说明|  
|--------------|-----------------|  
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|启动批处理操作。|  
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|在现有父项目下创建具有给定名称的子项目。|  
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|显示由完全限定的路径名称和源代码管理数据库位置指定的本地用户目录之间的差异。|  
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|检查当前状态的完全限定目录的列表。|  
|[SccEndBatch](../extensibility/sccendbatch-function.md)|结束批处理操作。|  
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|返回 (项目必须) 的给定项目的父路径。|  
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|检查是否允许在文件上进行多个签出。|  
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|检查插件是否会创建 MSSCCPRJ.SCC。SCC 文件。|  
  
## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>支持高级功能 (源代码管理插件 API 版本1.3 的函数)   
 此组函数定义源代码管理插件 API 版本1.3 中包含的附加功能。 它们提供对更高级源代码管理特性和功能的访问。  
  
|函数|说明|  
|--------------|-----------------|  
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|将源代码管理中的文件列表添加到当前项目中。|  
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|在没有用户界面的情况下从源控件中检索文件的列表。|  
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|检索源代码管理中与本地文件不同的文件的列表。|  
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|检索指定源代码管理插件支持的扩展功能的标志。|  
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|检索用户特定的选项。|  
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|检查项目或受源代码管理的项目中的目录和文件的列表。 找到的每个目录和文件名都将传递到回调函数。|  
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|检查对文件列表进行的名称更改。 每个文件名都将传递到其更改状态的回调函数。|  
  
## <a name="requirements"></a>要求  
 标头： scc。h  
  
 默认情况下，环境 SDK common 包含文件夹中提供 (*[drive]* \Program Files\VSIP 8.0 \ EnvSDK\common\inc;还在包含 MSSCCI 示例的 VSIP 文件夹中提供， *[drive]* \Program Files\VSIP 8.0 \ MSSCCI) 。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)   
 [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)
