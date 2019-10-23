---
title: 创建项模板
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- item templates [Visual Studio], creating
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d213ef7cd1c45043efbaad9fca4317f7a693bf4f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655844"
---
# <a name="how-to-create-item-templates"></a>如何：创建项模板

本文介绍如何使用“导出模板向导”创建项模板  。 如果模板将由多个文件组成，请参阅[如何：创建多文件项模板](../ide/how-to-create-multi-file-item-templates.md)。

## <a name="add-an-item-template-to-the-add-new-item-dialog-box"></a>将项模板添加到“添加新项”对话框中

1. 在 Visual Studio 中创建或打开一个项目。

1. 向项目添加一项，并在需要时修改它。

1. 修改代码文件，以指示应进行参数替换的位置。 有关详细信息，请参阅[如何：替换模板中的参数](../ide/how-to-substitute-parameters-in-a-template.md)。

1. 在“项目”菜单上，选择“导出模板”   。

1. 在“选择模板类型”页上，选择“项模板”，选择包含项的项目，然后选择“下一步”    。

1. 在“选择要导出的项”页上，选择要为其创建模板的项，然后选择“下一步”   。

1. 在“选择项引用”页上，选择要包含在模板中的程序集引用，然后选择“下一步”   。

1. 在“选择模板选项”页上，输入模板的名称和可选说明、图标和预览图像，然后选择“完成”   。

    将模板文件添加到 .zip 文件中，并复制到在向导中指定的目录  。 默认位置是 %USERPROFILE%\Documents\Visual Studio \<version\>\My Exported Templates  。

1. 如果未在“导出模板向导”中选择“自动将模板导入 Visual Studio”选项，则找到已导出的模板   。 然后，将其复制到用户项模板目录中。 默认位置是 %USERPROFILE%\Documents\Visual Studio \<version\>\Templates\ItemTemplates  。

1. 关闭 Visual Studio，然后重新打开它。

1. 创建一个新项目，或打开现有项目，然后选择“项目” > “添加新项”或按 Ctrl+Shift+A      。

   项模板显示在“添加新项”对话框中  。 如果在“导出模板向导”中添加了说明，则说明会显示在对话框的右侧  。

## <a name="enable-the-item-template-to-be-used-in-a-universal-windows-app-project"></a>启用在“通用 Windows 应用”项目中使用的项模板

向导会完成创建基本模板时的大部分工作，但在许多情况下，需要在导出模板后手动修改 .vstemplate 文件  。 例如，如果希望该项显示在通用 Windows 应用项目的“添加新项”对话框中，则需执行一些其他步骤  。

1. 按照上节中的步骤导出项模板。

1. 提取创建的 .zip 文件，然后在 Visual Studio 中打开 .vstemplate 文件   。

1. 对于 C# 通用 Windows 项目，在 `<TemplateData>` 元素中添加以下 XML：

   ```xml
   <TemplateID>Microsoft.CSharp.Class</TemplateID>
   ```

1. 在 Visual Studio 中，保存 .vstemplate 文件并将其关闭  。

1. 复制 .vstemplate 文件并将其粘贴回 .zip 文件中   。

     如果出现“复制文件”  对话框，请选择“复制和替换”  选项。

现在，可从“添加新项”对话框将基于此模板的项添加到通用 Windows 项目  。

## <a name="enable-templates-for-specific-project-subtypes"></a>启用特定项目子类型的模板

可指定应仅对某些项目子类型（如 Windows、Office、数据库或 Web）显示模板。

1. 在项模板的 .vstemplate 文件中找到 `ProjectType` 元素  。

1. 在 `ProjectType` 元素之后添加一个 [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) 元素。

1. 将该元素的文本值设置为下列值之一：

    - Windows
    - Office
    - 数据库
    - Web

例如：`<ProjectSubType>Database</ProjectSubType>`。

以下示例演示可用于“Office”项目的项模板  。

```xml
<VSTemplate Version="2.0.0" Type="Item" Version="2.0.0">
   <TemplateData>
      <Name>Class</Name>
      <Description>An empty class file</Description>
      <Icon>Class.ico</Icon>
      <ProjectType>CSharp</ProjectType>
      <ProjectSubType>Office</ProjectSubType>
      <DefaultName>Class.cs</DefaultName>
   </TemplateData>
   <TemplateContent>
      <ProjectItem>Class1.cs</ProjectItem>
   </TemplateContent>
</VSTemplate>
```

## <a name="manually-create-an-item-template"></a>手动创建项模板

某些情况下，可能希望从头开始手动创建项模板。

1. 创建项目和项目项。

2. 修改项目项，直到可以将它另存为一个模板。

3. 修改代码文件以指示应进行参数替换的位置。 有关参数替换的详细信息，请参阅[如何：替换模板中的参数。](../ide/how-to-substitute-parameters-in-a-template.md)

4. 创建 XML 文件，并将其与 .vstemplate 文件扩展名保存在与项目文件相同的目录中  。

5. 编辑 .vstemplate XML 文件以提供项模板元数据  。 有关详细信息，请参阅[模板架构引用（扩展性）](../extensibility/visual-studio-template-schema-reference.md)以及上一节中的示例。

6. 保存 .vstemplate 文件并将其关闭  。

7. 在**个Windows资源管理器**中，选择要包含在模板中的文件。 右键单击所选文件，然后选择“发送至” > “压缩的文件夹（zip 格式）”   。 所选的文件将压缩到一个 .zip 文件中  。

::: moniker range="vs-2017"

8. 复制该 .zip 文件并将其粘贴到用户的项模板位置  。 默认目录是 %USERPROFILE%\Documents\Visual Studio 2017\Templates\ItemTemplates  。 有关详细信息，请参阅[如何：查找和组织项目和项模板](../ide/how-to-locate-and-organize-project-and-item-templates.md)。

::: moniker-end

::: moniker range=">=vs-2019"

8. 复制该 .zip 文件并将其粘贴到用户的项模板位置  。 默认目录是 %USERPROFILE%\Documents\Visual Studio 2019\Templates\ItemTemplates  。 有关详细信息，请参阅[如何：查找和组织项目和项模板](../ide/how-to-locate-and-organize-project-and-item-templates.md)。

::: moniker-end

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建多文件项模板](../ide/how-to-create-multi-file-item-templates.md)
- [Visual Studio 模板架构引用（扩展性）](../extensibility/visual-studio-template-schema-reference.md)
