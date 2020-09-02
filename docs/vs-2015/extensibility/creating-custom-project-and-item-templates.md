---
title: 创建自定义项目和项模板
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
caps.latest.revision: 11
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c6875e13baa83d349020f50a3fe448a87ec5fd30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197397"
---
# <a name="creating-custom-project-and-item-templates"></a>创建自定义项目和项模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio SDK 包括用于创建自定义项目模板和自定义项模板的项目模板。 这些模板包含一些常见参数替代项，且以 zip 文件的形式生成。 它们不会自动部署，且不可用于实验实例。 将 zip 文件复制到你的位置。

通过“模板创建”模板，可在范围更广的扩展中包含模板。 通过在扩展中包括模板，你可以对源文件实现版本控制，并将一组模板项目生成到一个 VSIX 包中。

对于基本的模板创建方案，应使用“导出模板”向导，它将输出到压缩文件中。 有关创建基本模板的详细信息，请参阅 [创建项目和项模板](../ide/creating-project-and-item-templates.md)。

从 Visual Studio 2017 开始，将不再执行对自定义项目和项模板的扫描。 相反，扩展必须提供模板清单文件来描述这些模板的安装位置。 可以使用预览版2安装来更新 VSIX 扩展。 如果使用 MSI 部署扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅 [Upgrade Custom Visual Studio 项目和项模板 2017](/visualstudio/extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017?view=vs-2015)。 [Visual Studio 模板清单架构参考](/visualstudio/extensibility/visual-studio-template-manifest-schema-reference)中介绍了模板清单架构。

## <a name="create-a-project-template"></a>创建项目模板

1. 创建“项目模板”项目。 可以在 " **新建项目** " 对话框中的 "Visual Basic" 或 "Visual c # **扩展性** " 文件夹中找到项目模板。

     该模板会生成一个类文件、一个图标、一个 .vstemplate 文件、一个名为 ProjectTemplate.vbproj 或 ProjectTemplate.csproj 的可编辑项目文件，还会生成一些通常由其他项目类型生成的文件，例如 resources.resx 文件、AssemblyInfo 文件和 .settings 文件     。 每个代码文件都包含常见参数替代项（若适用）。

2. 根据项目的需要，添加项和从项目中删除项。 请勿删除可编辑的项目文件、AssemblyInfo 文件或 .vstemplate 文件 。

3. 请更新 .vstemplate 文件，使其反映出所有添加和删除的内容。 对于每个文件，[Project](../extensibility/project-element-visual-studio-templates.md) 元素都必须包含 [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) 元素才可包含在模板中。

4. 修改代码文件和其他面向用户的内容，并添加相应的参数替代项。

5. 根据需要修改生成的内容。

6. 生成项目。

     Visual Studio 会创建一个 .zip 文件，其中包含你的模板。 它不会部署，且不可用于实验实例。

## <a name="create-an-item-template"></a>创建项模板

1. 创建“项模板”项目。

     该模板会生成一个类文件、一个图标、一个 .vstemplate 文件和一个 AssemblyInfo 文件 。 类文件包含一些常见的参数替代项。

2. 根据项目的需要，添加项和从项目中删除项。

3. 请更新 .vstemplate 文件，使其反映出所有添加和删除的内容。 对于每个文件，[Project](../extensibility/project-element-visual-studio-templates.md) 元素都必须包含 [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) 元素才可包含在模板中。

4. 修改代码文件和其他面向用户的内容，并添加相应的参数替代项。

5. 根据需要修改生成的内容。

6. 生成项目。

     Visual Studio 会创建一个压缩文件，其中包含你的模板。 它不会部署，且不可用于实验实例。

## <a name="deploy-the-project-or-item-template"></a>部署项目或项模板

1. 创建 VSIX 项目。 有关详细信息，请参阅 [VSIX 项目模板](../extensibility/vsix-project-template.md)。

2. 将 VSIX 项目设置为启动项目。 在“解决方案资源管理器”中，选择 VSIX 项目节点，单击右键，然后选择“设为启动项目” 。

3. 将“项目模板”项目设置为 VSIX 项目的资产。 打开 .vsixmanifest 文件。 请在 " **资产** " 选项卡上单击 " **新建**"。

    1. 将“类型”字段设置为 Microsoft.VisualStudio.ProjectTemplate 或 Microsoft.VisualStudio.ItemTemplate  。

    2. 对于源，请选择“当前解决方案中的项目”选项，然后选择包含你的模板的项目。

4. 生成解决方案，然后按 F5。 这将显示实验实例。

5. 对于项目模板项目，应在 "新建项目" 对话框中的 " **新建项目** " 对话框中列出项目模板， (" **文件/新建/项目** ") 中的 "Visual c #" 或 "Visual Basic" 节点。 对于项模板项目，应看到 "添加新项" 对话框中列出的项模板 (在 **解决方案资源管理器**中，选择项目节点，然后单击 " **添加/新建项**) "。

## <a name="see-also"></a>另请参阅

- [Visual Studio 模板参考](../ide/visual-studio-template-reference.md)