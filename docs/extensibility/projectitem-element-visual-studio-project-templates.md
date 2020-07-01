---
title: 项目项元素（Visual Studio 项目模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- ProjectItem element [Visual Studio project templates]
- <ProjectItem> element [Visual Studio project templates]
ms.assetid: 82879fbe-7756-42cd-9a07-c10edf5b4673
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 943f50823892e3cd942709bdcd4556b65c006b58
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770305"
---
# <a name="projectitem-element-visual-studio-project-templates"></a>项目项元素（Visual Studio 项目模板）
指定项目模板中包含的文件。

> [!NOTE]
> `ProjectItem`元素根据模板是用于项目还是项来接受不同的属性。 本主题介绍 `ProjectItem` 项目模板的元素。 有关 `ProjectItem` 项模板元素的说明，请参阅项目项[元素（Visual Studio 项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)。

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<ProjectItem>

## <a name="syntax"></a>语法

```
<ProjectItem
    TargetFileName="TargetFileName.ext"
    ReplaceParameters="true/false"
    OpenInEditor="true/false"
    OpenInWebBrowser="true/false"
    OpenInHelpBrowser="true/false"
    OpenOrder="Value">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>属性

| 特性 | 说明 |
|---------------------| - |
| `TargetFileName` | 可选特性。<br /><br /> 指定从模板创建项目时项目项的名称和路径。 此属性用于创建与模板 *.zip*文件中的目录结构不同的目录结构，或用于创建项名称的。 |
| `ReplaceParameters` | 可选特性。<br /><br /> 一个布尔值，指定在从模板创建项目时，项是否具有必须替换的参数值。 默认值为 `false`。 |
| `OpenInEditor` | 可选特性。<br /><br /> 一个布尔值，指定在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 从模板创建项目时，是否应在其各自的编辑器中打开该项。<br /><br /> `OpenInWebBrowser` `OpenInHelpBrowser` 对于值为的项，将忽略和特性 `OpenInEditor` `true` 。<br /><br /> 默认值为 `false`。 |
| `OpenInWebBrowser` | 可选特性。<br /><br /> 一个布尔值，指定从模板创建项目时是否应在 Web 浏览器中打开该项。<br /><br /> 只有项目的本地 HTML 文件和文本文件才能在 Web 浏览器中打开。 不能用此属性打开外部 Url。<br /><br /> 默认值为 `false`。 |
| `OpenInHelpBrowser` | 可选特性。<br /><br /> 一个布尔值，指定在从模板创建项目时是否应在帮助查看器中打开该项。<br /><br /> 只有项目的本地 HTML 文件和文本文件才能在帮助浏览器中打开。 不能用此属性打开外部 Url。<br /><br /> 默认值为 `false`。 |
| `OpenOrder` | 可选特性。<br /><br /> 指定一个数字值，该值表示将在各自的编辑器中打开项的顺序。 所有值都必须是10的倍数。 `OpenOrder`将首先打开值较高的项。 |

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Project](../extensibility/project-element-visual-studio-templates.md)|指定要添加到项目中的文件或目录。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 `string`，它表示模板 *.zip*文件中的文件的名称或路径。

## <a name="remarks"></a>注解
 `ProjectItem`是的一个可选子级 `Project` 。

 `TargetFileName`特性可用于创建与模板 *.zip*文件中的目录结构不同的目录结构。 例如，如果文件*myfile.txt*位于模板 *.zip*文件的根目录中，但你希望将该文件放在从该模板创建的所有项目中名为*CustomFiles*的目录中，则可以使用以下 XML：

```xml
<ProjectItem TargetFileName="CustomFiles\MyFile.vb">MyFile.vb</ProjectItem>
```

 `TargetFileName`特性还可用于重命名文件名中包含国际字符的文件。 例如，模板 *.zip*文件不能包含带有 Unicode 字符的文件名，因此必须先重命名该文件，然后才能将其压缩为 *.zip*文件。 `TargetFileName`特性可用于将文件名称设置回原始 Unicode 文件名。

 `TargetFileName`特性还可用于重命名具有参数的文件。 下面的过程说明如何将位于模板 *.zip*文件的根目录中的*myfile.txt*文件重命名为基于项目名称的文件名称。

### <a name="to-rename-files-with-parameters"></a>用参数重命名文件

1. 在 *.vstemplate*文件中使用以下 XML：

   ```xml
   <ProjectItem TargetFileName="$safeprojectname$.vb">MyFile.vb</ProjectItem>
   ```

2. 在文本编辑器或中打开项目文件（项目的 *.vbproj* [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ） [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

3. 在项目文件中查找类似于以下 XML 的行：

   ```xml
   <Compile Include="MyFile.vb">
   ```

4. 将代码行替换为以下 XML：

   ```xml
   <Compile Include="$safeprojectname$.vb">
   ```

    从此模板创建项目时，文件名将基于用户在 "**新建项目**" 对话框中输入的名称，并删除所有不安全字符和空格。 有关详细信息，请参阅[模板参数](../ide/template-parameters.md)。

## <a name="example"></a>示例
 下面的示例演示应用程序的项目模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem ReplaceParameters="true">Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [模板参数](../ide/template-parameters.md)
- [项目项元素（Visual Studio 项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)
