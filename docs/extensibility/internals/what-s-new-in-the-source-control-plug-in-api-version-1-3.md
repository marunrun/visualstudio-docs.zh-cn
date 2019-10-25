---
title: 源代码&#39;管理插件 API 版本1.3 中的新增功能 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f45eeb3c57d5339b1e9fd66951dcbb60970e108
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721586"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>源代码&#39;管理插件 API 版本1.3 中的新增功能
源代码管理插件 API 版本1.3 引入了以下新函数来提供更高级的控件。

## <a name="changes"></a>Changes
 以下函数是源代码管理插件 API 版本1.3 中的新增功能：

|函数|概述|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|允许报告其他功能位|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|允许检查版本控制数据库中具有比本地磁盘更高的版本的文件|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|允许检查指定文件的名称更改状态（重命名、添加和删除）|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|允许检查版本控制数据库中的目录和文件|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|将版本控制数据库中指定的文件列表添加到当前项目|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|执行指定文件的无提示 "Get" （不显示用户界面）|
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|允许访问特定于用户的选项|

## <a name="see-also"></a>请参阅
- [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)