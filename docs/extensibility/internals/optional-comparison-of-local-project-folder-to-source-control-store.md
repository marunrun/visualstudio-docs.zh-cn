---
title: 将项目文件夹与源代码管理存储进行比较 |Microsoft Docs
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
ms.openlocfilehash: 45bd5b105a2fd24078bc85d8cf5b044351cd78be
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726128"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>本地项目文件夹与源代码管理存储之间的可选比较
在源代码管理插件 API 1.2 中，本地项目文件夹和源控件之间的比较是通过使用函数[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和[SccDirDiff](../../extensibility/sccdirdiff-function.md)来完成的。

 在**解决方案资源管理器**中，如果选择了文件夹而不是单个文件，则 "**比较版本**" 快捷菜单将在源代码管理插件中调用新的[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和[SccDirDiff](../../extensibility/sccdirdiff-function.md) 。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新函数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 @No__t_0 函数在 `SccDirDiff` 之前调用，以确定工作目录是否受源代码管理。 @No__t_0 函数显示当前本地目录与相应的源代码管理文件夹之间的差异。 此命令要求源代码管理插件显示对目录所做的更改的列表。 源代码管理插件提供自己的 UI 来显示差异。

> [!NOTE]
> 此函数使用与[SccDiff](../../extensibility/sccdiff-function.md)相同的命令标志。 作为源代码管理插件提供程序，你可以选择不支持目录的 "快速差异" 操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)