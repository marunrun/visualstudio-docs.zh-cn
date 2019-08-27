---
title: 比较项目文件夹与源代码管理存储区 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d675868e10a99a192681c52495ad3b37e384d390
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350707"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>本地项目文件夹与源代码管理存储之间的可选比较
在源控制本地项目文件夹与源控件之间的比较通过使用函数来实现的插件 API 1.2 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)并[SccDirDiff](../../extensibility/sccdirdiff-function.md)。

 内**解决方案资源管理器**，如果而不是单个文件，选择文件夹**比较版本**快捷方式菜单调用的新[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和[SccDirDiff](../../extensibility/sccdirdiff-function.md)在源代码管理插件。

## <a name="new-capability-flags"></a>新的功能标志
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新的函数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 `SccDirQueryInfo`之前调用函数`SccDirDiff`以确定是否受源代码管理的工作目录。 `SccDirDiff`函数显示当前的本地目录与相应的源代码管理文件夹之间的差异。 此命令要求源代码管理插件的目录中显示更改的列表。 源代码管理插件提供了自己的 UI 显示差异。

> [!NOTE]
> 此函数使用相同的命令标志，作为[SccDiff](../../extensibility/sccdiff-function.md)。 作为源代码管理插件提供程序，你可能选择不支持目录的"快速 diff"操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)