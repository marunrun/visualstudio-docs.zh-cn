---
title: 本地项目文件夹与源代码管理存储区的可选比较 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: be26b4195e0db7b3b78fcc2223ff2a6f8bde47d3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438940"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>本地项目文件夹与源代码管理存储之间的可选比较
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在源控制本地项目文件夹与源控件之间的比较通过使用函数来实现的插件 API 1.2 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)并[SccDirDiff](../../extensibility/sccdirdiff-function.md)。  
  
 内**解决方案资源管理器**，如果而不是单个文件，选择文件夹**比较版本**快捷方式菜单调用的新[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和[SccDirDiff](../../extensibility/sccdirdiff-function.md)在源代码管理插件。  
  
## <a name="new-capability-flags"></a>新的功能标志  
 `SCC_CAP_DIRECTORYDIFF`  
  
 `SCC_CAP_DIRECTORYCHECKOUT`  
  
## <a name="new-functions"></a>新的函数  
 [SccDirDiff](../../extensibility/sccdirdiff-function.md)  
  
 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)  
  
 `SccDirQueryInfo`之前调用函数`SccDirDiff`以确定是否受源代码管理的工作目录。 `SccDirDiff`函数显示当前的本地目录与相应的源代码管理文件夹之间的差异。 此命令要求源代码管理插件的目录中显示更改的列表。 源代码管理插件提供了自己的 UI 显示差异。  
  
> [!NOTE]
> 此函数使用相同的命令标志，作为[SccDiff](../../extensibility/sccdiff-function.md)。 作为源代码管理插件提供程序，你可能选择不支持目录的"快速 diff"操作。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
