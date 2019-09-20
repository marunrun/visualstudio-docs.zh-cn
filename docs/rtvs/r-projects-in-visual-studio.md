---
title: R 项目
description: 如何在 Visual Studio 中创建一个包含属性、项目命令和模板的管理器 R 项目。
ms.date: 06/29/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: bcdef95935c0522c8b93a972d7f44fbd7632c53b
ms.sourcegitcommit: b02c40c1ba193e38b5ace14590a6d57590d3270f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71012624"
---
# <a name="create-r-projects-in-visual-studio"></a>在 Visual Studio 中创建 R 项目

R 项目（.rxproj 文件）可标识与项目关联的所有源和内容文件  。 其中还包含每个文件的生成信息，会维护与源代码管理系统集成的信息，并且帮助用户将应用程序整理为逻辑组件。 但是，与工作区相关的信息（如安装包的列表）由工作区自身单独进行维护。

项目始终在 Visual Studio 解决方案内进行管理，而解决方案中可包含可相互引用的项目，数量不限  。 请参阅[在 Visual Studio 中使用多个项目类型](#use-multiple-project-types-in-visual-studio)。

## <a name="creating-a-new-r-project"></a>创建新 R 项目

1. 打开 Visual Studio。
1. 选择“文件”>“新建”>“项目”(Ctrl+Shift+N     )
1. 选择“模板” > “R”   下的“R 项目”，指定项目的名称和位置，然后选择“确定”  ：

    ![Visual Studio 中 R（VS2017 中的 RTVS）的“新建项目”对话框](media/getting-started-01-new-project.png)

此命令会创建一个项目，并在编辑器中打开一个空的 script.R 文件  。 此外，请注意在“解决方案资源管理器”  中，项目中存在其他两个文件：

![从模板创建的 R 项目的内容](media/projects-template-results.png)

.Rhistory 记录用户在 [R 交互](interactive-repl-for-r-in-visual-studio.md)窗口中输入的所有命令  。 可使用“R 工具” > “窗口” > “历史记录”命令打开专用的历史记录窗口    。 该窗口具有可用于清除历史记录内容的工具栏按钮和上下文菜单项。

rproject.rproj 文件维护不由 Visual Studio 管理的某些 R 特定的项目设置  ：

| Property | 默认 | 说明 |
| --- | --- | --- |
| Version | 1.0 | 用于创建项目的针对 Visual Studio 的 R 工具的版本。 |
| RestoreWorkspace | 默认 | 自动从项目目录中的 `.RData` 文件加载以前的工作区变量。 |
| SaveWorkspace | 默认 | 关闭项目时，将当前工作区变量保存到项目目录中的 `.RData` 文件。 |
| AlwaysSaveHistory | 默认 | 关闭项目时，将当前“交互窗口”历史记录保存到项目目录中的 `.RHistory` 文件。 |
| EnableCodeIndexing | 是 | 确定是否运行后台索引任务，加快代码搜索速度。 |
| UseSpacesForTab | 是 | 确定在编辑器中按 Tab 键时是插入空格（是）还是制表符（否）  。 |
| NumSpacesForTab | 2 | 如果 UseSpacesForTab 为“是”，则表示要插入的空格数。 |
| 编码 | UTF-8 | `.R` 文件的默认编码。 |
| RnwWeave | Sweave | 编辑 Rnw 文件时使用的包。 |
| LaTeX | pdfLaTeX | 将 RMarkdown 转换为 PDF 时使用的库。 |

### <a name="converting-a-folder-of-files-to-an-r-project"></a>将包含文件的文件夹转换为 R 项目

如果现有文件夹中包含 .R 文件，并希望在项目中管理该文件夹，请执行以下步骤： 

1. 如上一节所述，在 Visual Studio 中创建一个新项目。
1. 将文件复制到项目文件夹。
1. 在 Visual Studio 解决方案资源管理器中，右键单击该项目，选择“添加” > “现有项”，然后浏览到要添加的文件   。 选择“确定”后，这些文件会出现在项目树中  。
1. 要将代码整理到子文件夹中，请右键单击该项目，选择“添加” > “新建文件夹”，然后将文件复制到该文件夹并添加步骤 3 中的现有项   。

## <a name="project-properties"></a>项目属性

要打开项目属性页，请在解决方案资源管理器中右键单击项目，然后选择“属性”，或选择“项目”>“（项目名称）属性”菜单项    。 打开的窗口会显示项目属性：

| Tab | Property | 说明 |
| --- | --- | --- |
| 运行 | 启动文件 | 使用“源启动文件”  命令、F5  、“调试”   > “启动调试”  或“调试”   > “启动但不调试”  运行的文件的文件名。 右键单击项目中的文件并选择“设置为启动 R 脚本”，也会将其设置为启动文件  。 |
| | 运行时重置 R 交互 | 运行项目时清除交互窗口工作区中的所有变量。 这样可确保没有以前运行产生的残留工作区内容。 |
| | 远程项目路径 | 远程工作区的路径。 |
| | 运行时传输文件 | 指示在每次运行时是否将项目文件按“要传输的文件”  筛选后，复制到远程工作区。 |
| | 要传输的文件 | 选中“运行时传输文件”  后，表示要复制到远程工作区的特定文件的文件名和通配符。 |
| 设置 | （Settings.R 文件） | R 项目设置源于项目内的 Settings.R 或 *.Settings.R 文件   。 如果没有设置文件，则可添加变量并保存页面，此时会创建一个默认的 Settings.R 文件  。 还可通过“文件” > “添加新项”菜单命令将设置文件添加到项目中   。 <br/> 将设置存储为 R 代码，并且在运行其他模块前可提供文件，因而可使用预定义的设置预先填充环境。 |

## <a name="r-specific-project-commands"></a>R 特定的项目命令

通过右键单击菜单和“项目”  菜单，Visual Studio 项目可支持多个常规命令。 有关这些常规功能的详细信息，请参阅 [Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)。 但是请注意，针对 Visual Studio 的 R 工具 (RTVS) 向 R 项目的右键单击菜单添加了许多自己的命令，还在项目中添加了文件和文件夹。

| 命令 | 说明 |
| --- | --- |
| 在此处设置工作目录 | 将 R 交互窗口的工作目录设置为项目文件夹，该操作还可对项目中的任何子文件夹执行。 |
| 打开包含的文件夹 | 在所选文件位置打开 Windows 资源管理器。 |
| 添加 R 脚本 | 使用默认名称创建一个新的 .R 文件并将其打开  。 还可使用“添加” > “新项”命令创建 .R 文件以及多种其他文件类型    。 请参阅 [R 特定的项模板](#r-specific-item-templates)。 |
| 添加 R Markdown | 使用默认名称创建一个新的 .rmd 文档并将其打开  。 还可使用“添加” > “新项”命令创建 .rmd 文件以及多种其他文件类型    。 请参阅 [R 特定的项模板](#r-specific-item-templates)。  |
| 发布存储过程 | 启动发布 R 脚本中包含的任何存储过程的进程。 请参阅[处理 SQL Server 存储过程](integrating-sql-server-with-r.md#work-with-sql-server-stored-procedures)。 |

## <a name="r-specific-item-templates"></a>R 特定的项模板

RTVS 包括多种用于特定文件类型的模板。 可通过以下方式访问模板：右键单击 R 项目并选择“添加” > “新项”、选择“项目” > “添加新项”，或者使用“文件” > “新建” > “文件”并选择“R”选项卡         。浏览模板的最佳方法是创建一个新项目，然后插入每种类型的文件。

> [!Note]
> 使用“添加” > “新项”命令也可显示未在表中列出的常规文件类型；通过“文件” > “新建” > “文件”命令可包含这些类型，无需转到“常规”选项卡       。

| 文件类型 | 说明 |
| --- | --- |
| R 脚本 | 包含可在 R 命令行中输入的相同命令的文本文件。 |
| R Markdown | 包含 [R Markdown](rmarkdown-with-r-in-visual-studio.md) 文档的文件。 |
| R 设置 | 保存 R 应用程序设置的文件。 |
| R 文档 | 只包含名称、别名和标题字段的通用 R 文档文件。 |
| R 文档（功能） | 包含许多字段的 R 文档文件，其中含有用于描述功能的注释。 |
| R 文档（数据集） | 包含许多字段的 R 文档文件，其中含有用于描述数据集的注释。 |
| SQL 查询 | 空白 .sql 文件  。 请参阅[使用 SQL Server 和 R](integrating-sql-server-with-r.md)。 |
| 使用 R 的存储过程 | 具有子 SQL 查询和子存储过程模板文件的 R 文件。 请参阅[使用 SQL Server 和 R](integrating-sql-server-with-r.md)。 |

## <a name="use-multiple-project-types-in-visual-studio"></a>在 Visual Studio 中使用多个项目类型

Visual Studio 解决方案可以在一个逻辑位置方便地收集和管理相关项目。 解决方案有助于保持代码组织有序，促进团队内的协作。

在以下示例中，此解决方案包含一个 R 项目（附带使用 R 和 Azure 机器学习生成的模型）、一个 Python/scikit-learn 项目，一个 C++ 项目（包含用于密集计算工作的模块）、一个用于管理数据的 SQL 项目，以及一个发布结果的网站的 Python/Bottle 项目：

![在解决方案中显示多个相关项目的 Visual Studio 解决方案资源管理器](media/projects-polyglot.png)

以粗体突出显示的项目是解决方案的“启动”项目；若要进行更改，请右键单击其他项目，然后选择“设置为启动项目”  。

> [!Note]
> 目前，没有任何明确可用的 R 与 C#/C++ 语言的集成（但有针对 Python 的集成，请参阅[创建适用于 Python 的 C++ 扩展](../python/working-with-c-cpp-python-in-visual-studio.md)）。  但有一些库可以为 R 提供 C# 和 C++ 桥接。

有关通常管理项目和解决方案的详细信息，请参阅 [Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)。
