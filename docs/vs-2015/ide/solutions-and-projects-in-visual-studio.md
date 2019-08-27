---
title: 解决方案和项目
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.savedeferredsaveprojectonclose
- vs.untrustedtemplateopeningdocuments
- Project Properties.FullPath
- vs.addnewsolutionitem
- vs.environment.projects
- vs.openproject
- vs.getopenfilename
- vs.addnewitem
- vs.encoding
- vs.addexistingitem
- Project Properties.URL
- VS.SolutionExplorer
- Project Properties.FileName
- SolutionProperties.Name
- VS.SaveChangesDlg
- vs.newproject
- VS.SolutionExplorer.Selection
- SolutionProperties.Path
- vs.getdirectoryname
- vs.addexistingsolutionitem
- SolutionProperties.Description
- vs.environment.solutions
- vs.saveordiscarddeferredsaveproject
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- vs.solutionpropertypages
- vs.solutionpropertypages.startupproject
- vs.solutionpropertypages.configurationsettings
- solution items, folder in Solution Explorer
- solution items, shared
- solutions [Visual Studio]
- project items [Visual Studio], about project items
- workspaces
- solutions [Visual Studio], designing
- projects [Visual Studio]
- solutions [Visual Studio], projects and
- vs.solutionpropertypages.projectdependencies
- applications [Visual Studio]
- projects [Visual Studio], setting up
- miscellaneous files
ms.assetid: aeaf56cb-c2dd-47f6-b012-23b84b7a7254
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 340fe819086d3cc18cb9c2dd6a4ca14129c6d8ad
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679882"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Visual Studio 中的解决方案和项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中创建应用、应用程序、网站、Web 应用、脚本、插件等时，会从 *项目*开始。 在逻辑意义上，项目包含所有源代码文件、图标、图像、数据文件以及将编译到可执行程序或网站中，或是执行编译所需的任何其他内容。  项目还包含所有编译器设置以及程序将与之通信的各种服务或组件需要的其他配置文件。

 在字面意义上，项目是 XML 文件（*.vbproj、\*.csproj、\*.vcxproj），它定义虚拟文件夹层次结构以及它“包含”的所有项和所有生成设置的路径。 在 Visual Studio 中，项目文件由解决方案资源管理器用于显示项目内容和设置。 编译项目时，MSBuild 引擎会使用项目文件创建可执行文件。 还可以自定义项目以生成其他类型的输出。

 在逻辑意义上和文件系统中，项目包含在 *解决方案*中，后者可能包含一个或多个项目，以及生成信息、Visual Studio 窗口设置和不与任何项目关联的任何杂项文件。 在字面意义上，解决方案是具有自己的唯一格式的文本文件；它通常不应进行手动编辑。

 解决方案具有关联的 *.suo 文件，该文件为处理过项目的每个用户存储设置、首选项和配置信息。

 下图显示项目与解决方案，以及它们在逻辑上包含的项之间的关系。

 ![Visual Studio 项目和解决方案](../ide/media/vs2015-project-diagram.png "vs2015_project_diagram")

 还可以创建自定义项目和项模板。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="creating-new-projects"></a>创建新项目
 创建新项目的最简单方法是从预定义的项目模板开始，该模板包含一组基本的预生成代码文件、配置文件、资产和设置，这些内容使你可以开始采用特定编程语言创建特定类型的应用程序或网站。 这些模板是从主菜单选择“文件”&#124;“新建”&#124;“项目”或“文件”&#124;“新建”&#124;“网站”，然后进行导航时在“新建项目对话框”中看到的内容。 有关详细信息，请参阅[创建解决方案和项目](../ide/creating-solutions-and-projects.md)和 [NIB Creating Projects from Templates](https://msdn.microsoft.com/7c36d86a-6b79-4480-8228-0f925f1204b2)（NIB 从模板创建项目）。

## <a name="managing-projects-in-solution-explorer"></a>在解决方案资源管理器中管理项目
 创建新项目之后，可使用 **“解决方案资源管理器”** 查看和管理项目和解决方案及其关联项。 下图显示具有一个包含两个项目的 C# 解决方案的服务器资源管理器。

 ![解决方案资源管理器](../ide/media/vs2015-solution-explorer.png "vs2015_solution_explorer")

## <a name="in-this-section"></a>本节内容

- [创建解决方案和项目](../ide/creating-solutions-and-projects.md)

- [添加和删除项目项](../ide/adding-and-removing-project-items.md)

- [管理项目和解决方案属性](../ide/managing-project-and-solution-properties.md)

- [管理项目中的引用](../ide/managing-references-in-a-project.md)

- [应用程序属性](../ide/application-properties.md)

- [管理程序集签名和清单签名](../ide/managing-assembly-and-manifest-signing.md)

- [如何：指定应用程序图标（Visual Basic、C#）](../ide/how-to-specify-an-application-icon-visual-basic-csharp.md)

- [面向特定的 .NET Framework 版本](../ide/targeting-a-specific-dotnet-framework-version.md)

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)

## <a name="see-also"></a>请参阅
 [Visual Studio IDE](../ide/visual-studio-ide.md)
