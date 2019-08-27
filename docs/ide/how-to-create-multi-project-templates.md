---
title: 创建多项目模板
ms.date: 04/17/2019
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-project
- project templates, multi-project
- multi-project templates
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f24a7c0d07c804ca45bb31058061cda714ef6a51
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62430492"
---
# <a name="how-to-create-multi-project-templates"></a>如何：创建多项目模板

多项目模板用作两个或多个项目的容器。 创建基于多项目模板的项目时，模板中的每个项目都会添加到解决方案中。

多项目模板包含两个或多个项目模板，以及一个 ProjectGroup 类型的根模板。

多项目模板的行为不同于单项目模板。 多项目模板具有以下独特特征：

- 使用多项目模板创建新项目时，无法向此模板中的各个项目分配名称。 请改用 vstemplate 文件中 ProjectTemplateLink 元素上的 ProjectName 属性为每个项目指定名称。

- 多项目模板可能包含不同语言的项目，但仅可将整个模板本身放置在一个类别中。 在 vstemplate 文件的 ProjectType 元素中指定模板类别。

多项目模板必须包括以下各项，并压缩为 .zip 文件：

- 整个多项目模板的根 vstemplate 文件。 此 vstemplate 根文件包含在创建新项目的对话框中显示的元数据。 它还指定在何处查找模板中项目的 vstemplate 文件。 此文件必须位于 .zip 文件的根目录中。

- 两个或多个文件夹，其中包含完整的项目模板所需的文件。 文件夹包含项目的所有代码文件，以及项目的 vstemplate 文件。

例如，具有两个项目的多项目模板 .zip 文件包含以下文件和目录：

- MultiProjectTemplate.vstemplate
- *\Project1\MyTemplate.vstemplate*
- \Project1\Project1.vbproj
- \Project1\Class.vb
- *\Project2\MyTemplate.vstemplate*
- \Project2\Project2.vbproj
- \Project2\Class.vb

多项目模板的根 vstemplate 文件不同于单项目模板，表现在以下方面：

- VSTemplate 元素的 Type 属性有 ProjectGroup 而没有 Project 值。 例如:

    ```xml
    <VSTemplate Version="2.0.0" Type="ProjectGroup"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    ```

- TemplateContent 元素包含 ProjectCollection 元素，它有一个或多个 ProjectTemplateLink 元素，这些元素定义了所包含项目的 vstemplate 文件的路径。 例如:

    ```xml
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink>
                Project1\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink>
                Project2\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
    ```

> [!TIP]
> 如果只需在“新建项目”对话框中显示多项目模板（而不是所包含的各个项目），请将内部模板标记为[隐藏](../extensibility/hidden-element-visual-studio-templates.md)。 例如:
>
> ```xml
> <VSTemplate Type="Project" ... >
>     <TemplateData>
>         ...
>         <Hidden>true</Hidden>
>     </TemplateData>
>     ...
> </VSTemplate>
> ```

## <a name="create-a-multi-project-template-from-an-existing-solution"></a>从现有解决方案中创建多项目模板

1. 创建一个解决方案，并添加两个或多个项目。

2. 自定义项目，直到可将其导出到模板。

   > [!TIP]
   > 如果使用的是[模板参数](template-parameters.md)并且想要引用父模板中的变量，请在参数名称前加上前缀 `ext_`。 例如 `$ext_safeprojectname$`。 此外，将“ProjectTemplateLink”元素的“CopyParameters”属性设置为“true”。
   >
   > ```xml
   > <ProjectTemplateLink ProjectName="MyProject" CopyParameters="true">...</ProjectTemplateLink>
   > ```

3. 在“项目”菜单上，选择“导出模板”。

   “导出模板向导”随即打开。

4. 在“选择模板类型”页上，选择“项目模板”。 选择要导出到模板的一个项目，然后选择“下一步”。 （你将针对解决方案中的每个项目重复这些步骤。）

5. 在“选择模板选项”页面上，输入模板的名称和可选说明、图标和预览图像。 选择“完成”。

   项目会导出到一个 .zip 文件中，并放在指定的输出位置。

   > [!NOTE]
   > 每个项目都必须单独导出到一个模板，因此请为解决方案中的每个项目重复上述步骤。

6. 为模板创建一个目录，并为每个项目提供一个子目录。

7. 将每个项目的 .zip 文件的内容提取到创建的相应子目录中。

8. 在基目录中，创建扩展名为“.vstemplate”的 XML 文件。 此文件包含多项目模板的元数据。 有关文件结构，请参阅以下示例。 确保为每个项目的 vstemplate 文件指定相对路径。

9. 选择基目录中的所有文件，然后通过右键单击或从上下文菜单中选择“发送至” > “压缩的文件夹（zip 格式）”。

   这些文件和文件夹会压缩到一个 .zip 文件中。

10. 将 .zip 文件复制到用户项目模板目录中。 默认情况下，此目录为 %USERPROFILE%\Documents\Visual Studio \<version\>\Templates\ProjectTemplates。

11. 在 Visual Studio 中，选择“文件” > “新建” > “项目”，并验证是否显示了模板。

## <a name="two-project-example"></a>两个项目的示例

此示例演示一个基本的多项目根 vstemplate 文件。 在此示例中，模板有两个项目：“我的 Windows 应用程序”和“我的类库”。 ProjectTemplateLink 元素上的 ProjectName 属性指定提供给项目的名称。

> [!TIP]
> 如果未指定 ProjectName 属性，则将 vstemplate 文件的名称用作项目名称。

```xml
<VSTemplate Version="2.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="example-with-solution-folders"></a>解决方案文件夹示例

此示例使用 SolutionFolder 元素将项目分为两组：“数学类”和“图形类”。 该模板包含四个项目，其中两个位于每个解决方案文件夹中。

```xml
<VSTemplate Version="2.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <SolutionFolder Name="Math Classes">
                <ProjectTemplateLink ProjectName="MathClassLib1">
                    MathClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="MathClassLib2">
                    MathClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
            <SolutionFolder Name="Graphics Classes">
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">
                    GraphicsClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">
                    GraphicsClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建项目模板](../ide/how-to-create-project-templates.md)
- [Visual Studio 模板架构引用（扩展性）](../extensibility/visual-studio-template-schema-reference.md)
- [SolutionFolder 元素（Visual Studio 模板）](../extensibility/solutionfolder-element-visual-studio-templates.md)
- [ProjectTemplateLink 元素（Visual Studio 模板）](../extensibility/projecttemplatelink-element-visual-studio-templates.md)