---
title: 创建自定义项目和项目模板 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae404004f2660048ef7581a661d8f785495ed95a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739450"
---
# <a name="create-custom-project-and-item-templates"></a>创建自定义项目和项目模板

Visual Studio SDK 包括创建自定义项目模板的项目模板和自定义项目模板。 这些模板包括一些常见的参数替换，并生成为 zip 文件。 它们不是自动部署的，并且在实验实例中不可用。 您必须将生成的 zip 文件复制到用户模板目录。

模板创建模板允许您在较大的扩展中包含模板。 这允许您在源文件上实现版本控制，并将一组模板项目构建到一个 VSIX 包中。

您还可以配置模板以安装 NuGet 包。 有关详细信息，请参阅[Visual Studio 模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)。

对于基本模板创建方案，应使用**导出模板**向导，该向导输出到压缩文件。 有关基本模板创建的详细信息，请参阅[创建项目和项目模板](../ide/creating-project-and-item-templates.md)。

> [!NOTE]
> 从 Visual Studio 2017 开始，将不再执行自定义项目和项目模板的扫描。 相反，扩展必须提供描述这些模板的安装位置的模板清单文件。 您可以使用 Visual Studio 2017 更新 VSIX 扩展。 如果使用 MSI 部署扩展名，则必须手动生成模板清单文件。 有关详细信息，请参阅为[Visual Studio 2017 升级自定义项目和项目模板](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)。 模板清单架构记录在[可视化工作室模板清单架构引用](../extensibility/visual-studio-template-manifest-schema-reference.md)中。

## <a name="create-a-project-template"></a>创建项目模板

1. 创建项目模板项目。 您可以通过搜索"项目模板"并选择 C# 或 Visual Basic 版本，在 **"新项目**"对话框中找到项目模板。

     该模板生成类文件、图标 *、.vstemplate*文件、名为*ProjectTemplate.vbproj*或*ProjectTemplate.csproj*的可编辑项目文件，以及一些通常由其他项目类型（如*资源.resx*文件 *、AssemblyInfo*文件和 *.settings*文件）生成的文件。 每个代码文件都包含常见的参数替换（如果适用）。

![项目模板项目选择](media/project-template-selection.png)

2. 根据项目需要从项目添加和删除项目。 不要删除可编辑的项目文件 *、AssemblyInfo*文件或 *.vstemplate*文件。

3. 更新 *.vstemplate*文件以反映任何添加和删除。 [项目](../extensibility/project-element-visual-studio-templates.md)元素必须包含要包含在模板中的每个文件的[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)元素。

4. 修改代码文件和其他面向用户的内容，并添加适当的参数替换。

5. 根据需要修改生成的内容。

6. 生成项目。

     Visual Studio 创建包含模板的 *.zip*文件。 它不部署，并且在实验实例中不可用。

## <a name="create-an-item-template"></a>创建项模板

1. 创建项目模板项目。

     该模板生成类文件、图标 *、.vstemplate*文件和*AssemblyInfo*文件。 类文件包含一些常见的参数替换。

2. 根据项目需要从项目添加和删除项目。

3. 更新 *.vstemplate*文件以反映任何添加和删除。 [项目](../extensibility/project-element-visual-studio-templates.md)元素必须包含要包含在模板中的每个文件的[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)元素。

4. 修改代码文件和其他面向用户的内容，并添加适当的参数替换。

5. 根据需要修改生成的内容。

6. 生成项目。

     Visual Studio 会创建包含模板的压缩文件。 它不部署，并且在实验实例中不可用。

## <a name="deployment"></a>部署

### <a name="to-deploy-the-project-or-item-template"></a>部署项目或项目模板

1. 创建 VSIX 项目。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

2. 将 VSIX 项目设置为启动项目。 在**解决方案资源管理器**中，选择 VSIX 项目节点，右键单击，然后选择"**设置为启动项目**"。

3. 将项目模板项目设置为 VSIX 项目的资产。 打开 *.vsix清单*文件。 转到"**资产**"选项卡，然后单击 **"新建**"。

    1. 将 **"类型"** 字段设置为**Microsoft.VisualStudio.ProjectTemplate**或**Microsoft.VisualStudio.ItemTemplate**.

    2. 对于源，选择**当前解决方案选项中的 A 项目**，然后选择包含模板的项目。

4. 生成解决方案，然后按**F5**。 出现实验实例。

5. 对于项目模板项目，您应该在 Visual C# 或 Visual Basic 节点中看到**新项目**对话框（**文件** > **新项目** > **）中**列出的项目模板。 对于项目模板项目，您应该会看到"**添加新项目**"对话框中列出的项目模板。 要查看"**添加新项目**"对话框，请从**解决方案资源管理器中选择**项目节点，然后单击"**添加新** > **项**"。

## <a name="see-also"></a>请参阅

- [可视化工作室模板参考](../ide/creating-project-and-item-templates.md)
- [视觉工作室模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)
