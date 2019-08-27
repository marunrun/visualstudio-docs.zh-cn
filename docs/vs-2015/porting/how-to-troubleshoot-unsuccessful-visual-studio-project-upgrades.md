---
title: 如何：对不成功的项目的升级进行故障排除 |Microsoft Docs
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
ms.openlocfilehash: 1fe975fedb8237762d7dadffceff22203dcb899e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696381"
---
# <a name="how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades"></a>如何：升级不成功的 Visual Studio 项目进行故障排除
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 不能完全从早期版本的转换项目的有时[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 如果以下各节中的提示不能解决特定问题，您可能能够查找 TechNet 的详细信息[Wiki:开发门户](http://go.microsoft.com/fwlink/?LinkId=254808)。

## <a name="the-project-does-not-run-because-files-are-not-found"></a>项目不会运行，因为找不到文件
 项目文件包含硬编码文件路径的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]使用时按 F5 运行项目。 这些路径可能包括 devenv.exe 和其他所需的文件的位置。 中的升级版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，这些文件的路径已更改。

#### <a name="to-resolve-incorrect-file-paths"></a>若要解决不正确的文件路径

1. 在文本编辑器中打开项目文件。

2. 扫描的文件的路径可能不正确，尤其是那些包含[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]版本号。

3. 修改不正确的文件路径，使其指向新的目标。

## <a name="the-project-does-not-build-because-references-are-not-valid"></a>项目未生成因为引用无效
 当你升级[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，你可能还要升级[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]版本。 如果您的项目包含在更高版本中已不再使用的引用[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]版本，它们可能无法正确解析。 这是最有可能包括版本号，例如，引用`Microsoft.VisualStudio.Shell.Interop.8.0`。

 如果你的代码具有多个无效的引用，可能是最简单的解决方案使用的多目标功能[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]以面向早期版本的[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。

#### <a name="to-resolve-incorrect-references"></a>若要解决的错误参考

1. 在文本编辑器中打开项目文件。

2. 打开项目属性。

3. 选择正确**目标框架**值。 或者，可以修改的值`<TargetFrameworkVersion>`直接在项目文件中的元素。

   如果你希望项目在升级后运行[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]版本，必须更新项目的引用，并还更新任何`Imports`或`Using`调用所引用的语句。 如果你的项目加载在 IDE 中，您可以使用更新的引用**解决方案资源管理器**或**引用管理器**对话框。

## <a name="see-also"></a>请参阅
 [/ 升级 (devenv.exe)](../ide/reference/upgrade-devenv-exe.md) [将转换为 ASP.NET 4](https://msdn.microsoft.com/library/790147c6-36c1-41b5-a52d-30b9ccd2bd10)
