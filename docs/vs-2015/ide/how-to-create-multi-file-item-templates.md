---
title: 如何：创建多文件项模板 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-file item templates
- multi-file item templates
- item templates, creating multi-file item templates
ms.assetid: fe3c4257-e383-4c80-b8af-c5c521959c33
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e70039f361ac3410a8ddcccb0f139d8bdcb32ed9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668090"
---
# <a name="how-to-create-multi-file-item-templates"></a>如何：创建多文件项模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

项模板仅能指定一个项，但有时该项由多个文件组成。 例如，适用于 Visual Basic 的 Windows 窗体项模板需要下列三个文件：

- 包含用于窗体的代码的 .vb 文件。

- 包含用于窗体的设计器信息的设计器 .vb 文件。

- 包含用于窗体的嵌入资源的 .resx 文件。

  多文件项模板需要参数，用于确保在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中创建该项时使用正确的文件扩展名。 如果使用“导出模板”向导创建项模板，会自动生成这些参数，无需进一步编辑。 下列步骤解释如何使用参数来确保创建正确的文件扩展名。

### <a name="to-manually-create-a-multi-file-item-template"></a>手动创建多文件项模板

1. 以创建单文件项模板的方式创建项模板。 有关详细信息，请参阅[如何：创建项模板](../ide/how-to-create-item-templates.md)。

2. 将 `TargetFileName` 属性添加至每一个 `ProjectItem` 元素。 将 `TargetFileName` 属性的值设为 $fileinputname$.FileExtension，此处 FileExtension 为模板中包含的文件的文件扩展名。 例如:

    ```
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

     当由此模板派生的项被添加到项目中时，文件名将以用户在“添加新项”对话框中键入的名称为依据。

3. 选择要包含在模板中的文件，右键单击所选文件，单击“发送至”，然后单击“压缩的文件夹（zip 格式）”。 所选的文件被压缩到一个 .zip 文件中。

4. 将该 .zip 文件放到用户项模板位置。 默认情况下，该目录为 \My Documents\Visual Studio Version\Templates\ItemTemplates\\。 有关详细信息，请参阅[如何：查找和组织模板](../ide/how-to-locate-and-organize-project-and-item-templates.md)。

## <a name="example"></a>示例
 下列示例显示了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Windows 窗体模板。 基于此模板创建项时，创建的三个文件的名称将与“添加新项”对话框中输入的名称相匹配。

```
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
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)[如何：创建项模板](../ide/how-to-create-item-templates.md)[模板参数](../ide/template-parameters.md)[如何：替换模板中的参数](../ide/how-to-substitute-parameters-in-a-template.md)
