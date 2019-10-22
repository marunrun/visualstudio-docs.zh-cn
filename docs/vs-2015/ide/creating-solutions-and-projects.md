---
title: 创建解决方案和项目 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.openprojectfromweb
- vs.newproject
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], deleting
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
ms.assetid: 836f8ca0-3fc9-4f4b-9090-45f2e4d2e9c8
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 47083fe3f496cb855a7fb7101a886290e53cfbce
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619131"
---
# <a name="creating-solutions-and-projects"></a>Creating Solutions and Projects
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

项目是生成应用程序所需的所有内容的逻辑容器。 从主菜单上选择“文件”|“新建”|“项目”  创建项目时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将创建一个解决方案来包含它。 如有必要，可以继续向解决方案添加更多新项目或现有项目。 可以从现有代码文件创建项目，也可创建在使用完毕后删除的临时项目（仅 .NET）。

> [!NOTE]
> 本主题中的说明基于 Visual Studio Community 版。 您看到的对话框和菜单命令可能与此处描述的有所不同，这取决于您的设置或 Visual Studio 版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="create-a-project-from-an-installed-project-template"></a>从已安装项目模板创建项目
 从主菜单上依次选择“文件”|“新建”|“项目”  ，打开“新建项目”对话框。 在“已安装”|“模板”  下的左侧窗格中，选择编程语言和平台或技术，然后在中间窗格中选择可用的模板。

 在 **“新建项目”** 对话框中，选择 **“解决方案”** 下拉列表中提供的选项，在新解决方案、现有解决方案或 Visual Studio 的新实例中创建新项目。

## <a name="create-a-project-from-existing-code-files"></a>从现有代码文件创建项目
 如果有一系列松散源文件，则可以轻松创建一个包含它们的项目。 选择“文件”|“新建”|“从现有代码新建项目”  ，启动“从现有代码文件创建项目向导”  ，并按照提示进行操作。

> [!TIP]
> 此选项最适合于相对简单的文件集合。

## <a name="create-a-temporary-project-c-and-visual-basic"></a>创建临时项目（C# 和 Visual Basic）
 使用临时项目时，你可以在不指定磁盘位置的情况下创建和试验 .NET 项目。 创建项目时，只需在 **“新建项目”** 对话框中选择项目类型和模板，并指定名称。 使用临时项目时，你可以随时保存或放弃它。

## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>创建面向 .NET Framework 特定版本的 .NET 项目
 通过使用 **“新建项目”** 对话框顶部的 **“.NET Framework”** 版本下拉菜单，您可以创建面向 .Net Framework 早期版本的项目。 在选择项目模板之前设置此值，因为只有与该 .NET Framework 版本兼容的模板将出现在列表中。

 您必须在您的系统上安装 .NET Framework 3.5，这样可以访问 framework 4.0 以前的版本。

## <a name="downloading-sample-solutions"></a>下载示例解决方案
 可使用 Visual Studio 下载和安装 [MSDN 代码库](http://go.microsoft.com/fwlink/?LinkId=254185)中的示例解决方案。

 您可单独下载示例，也可以下载包含共享技术或主题的相关示例的示例包。 在为下载的任何示例发布源代码更改时，您将收到通知。

 有关详细信息，请参阅 [Visual Studio 示例](../ide/visual-studio-samples.md)。

## <a name="adding-single-files-at-the-solution-level"></a>在解决方案级添加单个文件
 有时，一个文件可能会被多个项目引用，或者包含在逻辑上属于解决方案级而非特定项目下的文本或各种数据。  向解决方案添加单个项：

1. 在“解决方案资源管理器”  中右键单击解决方案节点，然后选择“添加”|“新建项”  或“添加”|“现有项”  。

## <a name="creating-empty-solutions"></a>创建空解决方案
 尽管一个项目必须驻留在一个解决方案中，您仍然可以创建无任何项目的解决方案。

#### <a name="to-create-an-empty-solution"></a>创建空解决方案

1. 在 **文件** 菜单上，单击 **新建** ，然后单击 **新建项目**。

2. 在左窗格中，选择 **“已安装”** ，再选择 **“其他项目类型”** ，然后从展开的列表中选择 **“Visual Studio 解决方案”** 。

3. 在中间窗格中，选择 **空白解决方案**。

4. 为您的解决方案设置 **名称** 和 **位置** 值，然后单击 **确定**。

   在创建一个空白解决方案后，您可以通过在 **项目** 菜单上单击 **添加新项** 或 **添加现有项** ，把新的或现有的项目或项添加到解决方案中。

### <a name="deleting-solutions"></a>删除解决方案
 您可以永久性删除解决方案，但不能使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]来删除解决方案。 在删除解决方案前，把您要再次使用的任何项目移动到其他解决方案中。 然后，使用文件资源管理器删除包含 .sln 和 .suo 解决方案文件的目录。

> [!NOTE]
> .suo 文件是隐藏文件，在默认的文件资源管理器设置下不会显示。

##### <a name="to-delete-a-solution"></a>要删除解决方案

1. 在 **“解决方案资源管理器”** 中，右键单击要删除的解决方案，然后选择 **“在文件资源管理器中打开文件夹”** 。

2. 在文件资源管理器中，导航到上一级。

3. 选择包含该解决方案的目录，然后按“删除”。

## <a name="see-also"></a>另请参阅
 [解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)[笔尖如何：创建多项目解决方案](https://msdn.microsoft.com/02ecd6dd-0114-46fe-b335-ba9c5e3020d6)
