---
title: 项目元素（可视化工作室项目模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
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
ms.openlocfilehash: 11052d8e585f1d06f6d787402001cfbbe2b6810f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701843"
---
# <a name="projectitem-element-visual-studio-project-templates"></a>项目项目元素（可视化工作室项目模板）
指定项目模板中包含的文件。

> [!NOTE]
> 元素`ProjectItem`接受不同的属性，具体取决于模板是针对项目还是项。 本主题介绍项目`ProjectItem`模板的元素。 有关项目模板`ProjectItem`元素的说明，请参阅[项目项目元素（可视化工作室项目模板）。](../extensibility/projectitem-element-visual-studio-item-templates.md)

 \<模板>\<模板内容>\<项目>\<项目项>

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

### <a name="attributes"></a>特性

| 特性 | 描述 |
|---------------------| - |
| `TargetFileName` | 可选特性。<br /><br /> 指定从模板创建项目时项目项的名称和路径。 此属性可用于创建不同于模板 *.zip*文件中的目录结构的目录结构，或者使用参数替换创建项名称。 |
| `ReplaceParameters` | 可选特性。<br /><br /> 布尔值，用于指定项是否具有从模板创建项目时必须替换的参数值。 默认值为 `false`。 |
| `OpenInEditor` | 可选特性。<br /><br /> Boolean 值，用于指定在从模板创建项目时是否应在其相应的编辑器[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]中打开该项目。<br /><br /> 和`OpenInWebBrowser``OpenInHelpBrowser`属性在`OpenInEditor`值 为 的`true`项上将被忽略。<br /><br /> 默认值为 `false`。 |
| `OpenInWebBrowser` | 可选特性。<br /><br /> Boolean 值，用于指定在从模板创建项目时是否应打开 Web 浏览器。<br /><br /> 只能在 Web 浏览器中打开项目本地的 HTML 文件和文本文件。 无法使用此属性打开外部 URL。<br /><br /> 默认值为 `false`。 |
| `OpenInHelpBrowser` | 可选特性。<br /><br /> Boolean 值，用于指定在从模板创建项目时是否应在帮助查看器中打开该项目。<br /><br /> 只能在帮助浏览器中打开项目本地的 HTML 文件和文本文件。 无法使用此属性打开外部 URL。<br /><br /> 默认值为 `false`。 |
| `OpenOrder` | 可选特性。<br /><br /> 指定表示项目将在其各自的编辑器中打开的顺序的数值。 所有值必须为 10 的倍数。 首先打开值`OpenOrder`较高的项。 |

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Project](../extensibility/project-element-visual-studio-templates.md)|指定要添加到项目的文件或目录。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 表示`string`模板 *.zip*文件中文件的名称或路径的 。

## <a name="remarks"></a>备注
 `ProjectItem`是`Project`的可选子项。

 该`TargetFileName`属性可用于创建不同于模板 *.zip*文件中的目录结构的目录结构。 例如，如果文件*MyFile.vb*存在于模板 *.zip*文件的根目录中，但您希望该文件放置在从模板创建的所有项目中名为*CustomFiles*的目录中，则可以使用以下 XML：

```xml
<ProjectItem TargetFileName="CustomFiles\MyFile.vb">MyFile.vb</ProjectItem>
```

 该`TargetFileName`属性还可用于重命名其文件名中包含国际字符的文件。 例如，模板 *.zip*文件不能包含具有 Unicode 字符的文件名，因此必须先重命名该文件，然后才能将其压缩为 *.zip*文件。 该`TargetFileName`属性可用于将文件名设置为原始 Unicode 文件名。

 该`TargetFileName`属性还可用于使用参数重命名文件。 以下过程说明如何将存在于模板 *.zip*文件的根目录中的文件*MyFile.vb*重命名为基于项目名的文件名。

### <a name="to-rename-files-with-parameters"></a>使用参数重命名文件

1. 在 *.vstemplate*文件中使用以下 XML：

   ```xml
   <ProjectItem TargetFileName="$safeprojectname$.vb">MyFile.vb</ProjectItem>
   ```

2. 在文本编辑器或[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)][!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]中打开项目文件（项目的 *.vbproj）。*

3. 在项目文件中查找类似于以下 XML 的行：

   ```xml
   <Compile Include="MyFile.vb">
   ```

4. 将代码行替换为以下 XML：

   ```xml
   <Compile Include="$safeprojectname$.vb">
   ```

    使用此模板创建项目时，文件名将基于用户在 **"新建项目**"对话框中输入的名称，并删除所有不安全字符和空格。 有关详细信息，请参阅[模板参数](../ide/template-parameters.md)。

## <a name="example"></a>示例
 下面的示例显示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]应用程序的项目模板的元数据。

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
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [模板参数](../ide/template-parameters.md)
- [项目项目元素（可视化工作室项目模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)
