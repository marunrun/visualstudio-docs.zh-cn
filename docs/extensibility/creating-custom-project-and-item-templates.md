---
title: 创建自定义项目和项模板 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: overview
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c702aaaa51d86e2b8aac18a6b55201be03a635f
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903318"
---
# <a name="create-custom-project-and-item-templates"></a>创建自定义项目和项模板

Visual Studio SDK 包括用于创建自定义项目模板和自定义项模板的项目模板。 这些模板包括一些常见参数替换，并构建为 zip 文件。 它们不会自动部署，并且在实验实例中不可用。 必须将生成的 zip 文件复制到用户模板目录。

模板创建模板使你可以在更大的扩展中包含模板。 这使您可以对源文件实现版本控制，并将一组模板项目生成到一个 VSIX 包中。

你还可以配置模板来安装 NuGet 包。 有关详细信息，请参阅[Visual Studio 模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)。

对于基本的模板创建方案，你应该使用 "**导出模板**" 向导，该向导将输出到压缩的文件。 有关创建基本模板的详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

> [!NOTE]
> 从 Visual Studio 2017 开始，将不再执行对自定义项目和项模板的扫描。 相反，该扩展插件必须提供描述这些模板安装位置的模板清单文件。 可以使用 Visual Studio 2017 更新 VSIX 扩展。 如果使用 MSI 部署扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅[升级 Visual Studio 2017 的自定义项目和项模板](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)。 [Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)中介绍了模板清单架构。

## <a name="create-a-project-template"></a>创建项目模板

1. 创建项目模板项目。 可以通过搜索 "项目模板" 并选择 "c #" 或 "Visual Basic" 版本，在 "**新建项目**" 对话框中找到项目模板。

     该模板将生成一个类文件、一个图标、一个 *.vstemplate*文件、一个名为*ProjectTemplate. .vbproj*或*ProjectTemplate*的可编辑项目文件，以及一些通常由其他项目类型生成的文件，如*资源 .resx*文件、 *AssemblyInfo*文件和一个文件。 *.settings* 每个代码文件都在适当的位置包含通用参数替换。

![项目模板项目选择](media/project-template-selection.png)

2. 根据项目的需要，在项目中添加和删除项。 请勿删除可编辑的项目文件、 *AssemblyInfo*文件或 *.vstemplate*文件。

3. 更新 *.vstemplate*文件以反映任何添加和删除操作。 对于要包含在模板中的每个文件，[项目](../extensibility/project-element-visual-studio-templates.md)[元素必须包含一个项目](../extensibility/projectitem-element-visual-studio-item-templates.md)项元素。

4. 修改代码文件和其他面向用户的内容，并添加相应的参数替换。

5. 根据需要修改生成的内容。

6. 生成项目。

     Visual Studio 将创建一个包含模板的 *.zip*文件。 它不会部署，并且在实验实例中不可用。

## <a name="create-an-item-template"></a>创建项模板

1. 创建项模板项目。

     该模板将生成一个类文件、一个图标、一个 *.vstemplate*文件和一个*AssemblyInfo*文件。 类文件包含一些常见参数替换。

2. 根据项目的需要，在项目中添加和删除项。

3. 更新 *.vstemplate*文件以反映任何添加和删除操作。 对于要包含在模板中的每个文件，[项目](../extensibility/project-element-visual-studio-templates.md)[元素必须包含一个项目](../extensibility/projectitem-element-visual-studio-item-templates.md)项元素。

4. 修改代码文件和其他面向用户的内容，并添加相应的参数替换。

5. 根据需要修改生成的内容。

6. 生成项目。

     Visual Studio 将创建包含你的模板的压缩文件。 它不会部署，并且在实验实例中不可用。

## <a name="deployment"></a>部署

### <a name="to-deploy-the-project-or-item-template"></a>部署项目或项模板

1. 创建 VSIX 项目。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

2. 将 VSIX 项目设置为启动项目。 在**解决方案资源管理器**中，选择 "VSIX 项目" 节点，右键单击，然后选择 "**设为启动项目**"。

3. 将项目模板项目设置为 VSIX 项目的资产。 打开*source.extension.vsixmanifest*文件。 请在 "**资产**" 选项卡上单击 "**新建**"。

    1. 将 "**类型**" 字段设置为 " **VisualStudio** " 或 " **VisualStudio**"。

    2. 对于 "源"，请选择 "**当前解决方案中的项目**" 选项，然后选择包含模板的项目。

4. 生成解决方案，然后按**F5**。 将显示实验实例。

5. 对于项目模板项目，应在 "**新建项目**" 对话框（"**文件**  >  " "**新建**  >  **项目**"）的 "Visual c #" 或 "Visual Basic" 节点中看到您的项目模板。 对于项模板项目，应看到 "**添加新项**" 对话框中列出的项模板。 若要查看 "**添加新项**" 对话框，请从 "**解决方案资源管理器**" 中选择项目节点，然后单击 "**添加**  >  **新项**"。

## <a name="see-also"></a>另请参阅

- [Visual Studio 模板参考](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)
