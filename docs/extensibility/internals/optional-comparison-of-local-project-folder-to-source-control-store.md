---
title: 将项目文件夹与源控制存储进行比较 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: facb3b656e0ac50b50fdb0291307aa2fe98b1df4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706868"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>本地项目文件夹与源代码管理存储之间的可选比较
在源代码管理插件 API 1.2 中，使用函数[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和[SccDirDiff](../../extensibility/sccdirdiff-function.md)实现了本地项目文件夹和源代码管理之间的比较。

 在**解决方案资源管理器**中，如果选择了文件夹而不是单个文件，**则比较版本**快捷菜单将在源代码管理插件中调用新的[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和[SccDirDiff。](../../extensibility/sccdirdiff-function.md)

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新函数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 之前`SccDirQueryInfo``SccDirDiff`调用函数以确定工作目录是否受源代码管理。 该`SccDirDiff`函数显示当前本地目录和相应的源代码管理文件夹之间的差异。 此命令要求源代码管理插件显示目录的更改列表。 源代码管理插件提供其自己的 UI 来显示差异。

> [!NOTE]
> 此函数使用与[SccDiff](../../extensibility/sccdiff-function.md)相同的命令标志。 作为源代码管理插件提供程序，您可以选择不支持目录的"快速差异"操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
