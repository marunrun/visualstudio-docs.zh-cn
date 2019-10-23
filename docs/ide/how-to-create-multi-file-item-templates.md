---
title: 创建多文件项模板
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-file item templates
- multi-file item templates
- item templates, creating multi-file item templates
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 82047b4a49db4edbea4ce965d1987f87a799a9f7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655945"
---
# <a name="how-to-create-multi-file-item-templates"></a>如何：创建多文件项模板

项模板仅能指定一个项，但有时该项由多个文件组成。 例如，Windows 窗体项模板需要下列三个文件：

- 包含用于窗体的代码的文件

- 包含用于窗体的设计器信息的文件

- 包含用于窗体的嵌入资源的文件

多文件项模板需要参数，确保创建该项时使用正确的文件扩展名。 如果使用“导出模板向导”创建多文件项模板，会自动生成这些参数，无需进一步编辑  。

## <a name="use-the-export-template-wizard"></a>使用“导出模板向导”

可按创建单文件项模板的方式创建多文件项模板。 请参阅[如何：创建项模板](../ide/how-to-create-item-templates.md)。 在向导的“选择要导出的项”页面中，选择具有相关文件（例如，“Windows 窗体”窗体文件）的文件  。 向导会自动在模板中含入任何相关文件，例如设计器和资源文件。

## <a name="manually-create-a-multi-file-item-template"></a>手动创建多文件项模板

1. 创建项模板与手动创建单文件项模板一样，但包括每个构成多文件项的文件。

1. 在 .vstemplate XML 文件中，为每个单独文件添加 `ProjectItem` 元素，并向此元素添加 `TargetFileName` 属性  。 将 `TargetFileName` 属性的值设为 $fileinputname$.FileExtension，此处 FileExtension 为模板中包含的文件的文件扩展名   。 例如:

    ```xml
    <ProjectItem TargetFileName="$fileinputname$.vb">
        Form1.vb
    </ProjectItem>
    <ProjectItem TargetFileName="$fileinputname$.Designer.vb">
        Form1.Designer.vb
    </ProjectItem>
    <ProjectItem TargetFileName="$fileinputname$.resx">
        Form1.resx
    </ProjectItem>
    ```

     > [!NOTE]
     > 当由此模板派生的项被添加到项目中时，文件名将从用户在“添加新项”对话框中输入的名称派生  。

1. 选择要包含在模板中的文件，右键单击所选文件，然后选择“发送至” > “压缩的文件夹（zip 格式）”   。

   所选的文件将压缩到一个 .zip 文件中  。

1. 将该 .zip 文件复制到用户项模板位置  。 默认情况下，该目录为 %USERPROFILE%\Documents\Visual Studio \<Version\>\Templates\ItemTemplates  。 有关详细信息，请参阅[如何：查找和组织模板](../ide/how-to-locate-and-organize-project-and-item-templates.md)。

1. 关闭 Visual Studio，然后重新打开它。

1. 创建一个新项目，或打开现有项目，然后选择“项目” > “添加新项”或按 Ctrl+Shift+A      。

   多文件项模板在“添加新项”对话框中显示  。

## <a name="example"></a>示例

下列示例显示了 Windows 窗体模板。 基于此模板创建项时，创建的三个文件的名称将与“添加新项”对话框中输入的名称相匹配  。

```xml
<VSTemplate Version="2.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-file Item Template</Name>
        <Icon>Icon.ico</Icon>
        <Description>An example of a multi-file item template</Description>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectItem TargetFileName="$fileinputname$.vb" SubType="Form">
            Form1.vb
        </ProjectItem>
        <ProjectItem TargetFileName="$fileinputname$.Designer.vb">
            Form1.Designer.vb
        </ProjectItem>
        <ProjectItem TargetFileName="$fileinputname$.resx">
            Form1.resx
        </ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建项模板](../ide/how-to-create-item-templates.md)
- [模板参数](../ide/template-parameters.md)
- [如何：替换模板中的参数](../ide/how-to-substitute-parameters-in-a-template.md)