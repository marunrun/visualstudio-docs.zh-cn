---
title: 如何：排查项目升级失败问题 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
f1_keywords:
- VisualStudio.SourceControl.CannotOpenFromSourceControlDSW
- vs.UpgradeProjectSolution.8.0
helpviewer_keywords:
- upgrading applications, Visual Studio
- upgrading projects [Visual Studio]
- projects [Visual Studio], upgrading
- Visual Studio Conversion Wizard
- Conversion wizard
ms.assetid: 842fe448-c044-4343-8eae-d81711cf48ba
caps.latest.revision: 31
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 16232a72cd37f8d1d68760f032b6050e0bdf74c5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300358"
---
# <a name="how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades"></a>如何：升级 Visual Studio 项目失败疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有时，Visual Studio 不能从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的早期版本中完全转换项目。 如果以下部分中的提示不能解决你的特定问题，则可以在 TechNet [Wiki：开发门户](https://go.microsoft.com/fwlink/?LinkId=254808)中找到详细信息。

## <a name="the-project-does-not-run-because-files-are-not-found"></a>由于找不到文件，项目不会运行
 项目文件包含硬编码文件路径，当您按 F5 时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 使用该路径来运行项目。 这些路径可能包含 devenv 和其他所需文件的位置。 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的升级版本中，这些文件的路径可能已更改。

#### <a name="to-resolve-incorrect-file-paths"></a>解析错误的文件路径

1. 在文本编辑器中打开项目文件。

2. 扫描可能不正确的文件路径，特别是包含 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 版本号的文件路径。

3. 修改不正确的文件路径，使其指向新的目标。

## <a name="the-project-does-not-build-because-references-are-not-valid"></a>该项目不会生成，因为引用无效
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]升级时，可能也会升级 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本。 如果你的项目包含较新 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本中不再使用的引用，则可能无法正确解析。 这对于包含版本号的引用特别有用，例如 `Microsoft.VisualStudio.Shell.Interop.8.0`。

 如果你的代码具有许多无效引用，最简单的解决方案是使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的多目标功能，以 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]的早期版本为目标。

#### <a name="to-resolve-incorrect-references"></a>解析错误引用

1. 在文本编辑器中打开项目文件。

2. 打开项目属性。

3. 选择正确的 "**目标框架**" 值。 另外，还可以在项目文件中直接修改 `<TargetFrameworkVersion>` 元素的值。

   如果希望项目在升级的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本中运行，则必须更新项目的引用，并更新调用引用的任何 `Imports` 或 `Using` 语句。 如果你的项目在 IDE 中加载，则可以使用**解决方案资源管理器**或 "**引用管理器**" 对话框来更新这些引用。

## <a name="see-also"></a>请参阅
 [/Upgrade （devenv）](../ide/reference/upgrade-devenv-exe.md) [转换为 ASP.NET 4](https://msdn.microsoft.com/library/790147c6-36c1-41b5-a52d-30b9ccd2bd10)
