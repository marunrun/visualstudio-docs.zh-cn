---
title: 如何：选择要生成的文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, wildcards
- MSBuild, including files
- Include attribute [MSBuild]
ms.assetid: f5ff182f-7b3a-46fb-9335-37df54cfb8eb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a9ad869fc091035de711ec59e20d10fd0af5e21b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75574608"
---
# <a name="how-to-select-the-files-to-build"></a>如何：选择要生成的文件
如果生成包含多个文件的项目，可以在项目文件中分别列出每个文件，也可以使用通配符将一个目录或一组嵌套目录中的所有文件都包括进去。

## <a name="specify-inputs"></a>指定输入
项表示某个生成的输入。 有关项的详细信息，请参阅[项](../msbuild/msbuild-items.md)。

若要包括某个生成的文件，必须在 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目文件的项列表中包括这些文件。 通过逐个包括文件或使用通配符同时包括许多文件，可以将多个文件添加到项列表中。

#### <a name="to-declare-items-individually"></a>逐个声明各个项

- 使用 `Include` 属性，如下所示：

    `<CSFile Include="form1.cs"/>`

    or

    `<VBFile Include="form1.vb"/>`

    > [!NOTE]
    > 如果项集合中的项不在项目文件所在的同一目录中，则必须指定项的完整路径或相对路径。 例如：`Include="..\..\form2.cs"`。

#### <a name="to-declare-multiple-items"></a>声明多个项

- 使用 `Include` 属性，如下所示：

    `<CSFile Include="form1.cs;form2.cs"/>`

    or

    `<VBFile Include="form1.vb;form2.vb"/>`

## <a name="specify-inputs-with-wildcards"></a>使用通配符指定输入
还可以使用通配符以递归方式将子目录中的所有文件或某些特定文件包括在某个生成的输入中。 有关通配符的详细信息，请参阅[通配符](../msbuild/msbuild-items.md)

下面的示例基于一个项目，该项目包含下列目录和子目录中的图形文件，项目文件位于 Project 目录中  ：

Project\Images\BestJpgs 

Project\Images\ImgJpgs 

Project\Images\ImgJpgs\Img1 

#### <a name="to-include-all-jpg-files-in-the-images-directory-and-subdirectories"></a>包括 Images 目录和子目录中的所有 .jpg 文件  

- 使用下面的 `Include` 属性：

    `Include="Images\**\*.jpg"`

#### <a name="to-include-all-jpg-files-starting-with-img"></a>包括所有以“img”开头的 .jpg 文件  

- 使用下面的 `Include` 属性：

    `Include="Images\**\img*.jpg"`

#### <a name="to-include-all-files-in-directories-with-names-ending-in-jpgs"></a>包括目录中名称以“jpgs”结尾的所有文件 

- 使用以下 `Include` 属性之一：

    `Include="Images\**\*jpgs\*.*"`

    or

    `Include="Images\**\*jpgs\*"`

## <a name="pass-items-to-a-task"></a>将项传递给任务
在项目文件中，可以在任务中使用 @() 表示法，指定整个项列表作为生成的输入。 无论是分别列出所有文件还是使用通配符，均可以使用此表示法。

#### <a name="to-use-all-visual-c-or-visual-basic-files-as-inputs"></a>使用所有 Visual C# 或 Visual Basic 文件作为输入

- 使用 `Include` 属性，如下所示：

    `<CSC Sources="@(CSFile)">...</CSC>`

    or

    `<VBC Sources="@(VBFile)">...</VBC>`

> [!NOTE]
> 必须将通配符与项配合使用来指定生成的输入，不能使用 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 任务（如 [Csc](../msbuild/csc-task.md) 或 [Vbc](../msbuild/vbc-task.md)）中的 `Sources` 属性来指定输入。 下面的示例在项目文件中无效：
>
> `<CSC Sources="*.cs">...</CSC>`

## <a name="example"></a>示例
以下代码示例演示的项目单独包括所有输入文件。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Builtdir>built</Builtdir>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="Form1.cs"/>
        <CSFile Include="AssemblyInfo.cs"/>

        <Reference Include="System.dll"/>
        <Reference Include="System.Data.dll"/>
        <Reference Include="System.Drawing.dll"/>
        <Reference Include="System.Windows.Forms.dll"/>
        <Reference Include="System.XML.dll"/>
    </ItemGroup>

    <Target Name="PreBuild">
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>
    </Target>

    <Target Name="Compile" DependsOnTargets="PreBuild">
        <Csc Sources="@(CSFile)"
            References="@(Reference)"
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"
            TargetType="exe" />
    </Target>
</Project>
```

## <a name="example"></a>示例
以下代码示例使用通配符来包括所有 .cs 文件  。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <PropertyGroup>
        <builtdir>built</builtdir>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="*.cs"/>

        <Reference Include="System.dll"/>
        <Reference Include="System.Data.dll"/>
        <Reference Include="System.Drawing.dll"/>
        <Reference Include="System.Windows.Forms.dll"/>
        <Reference Include="System.XML.dll"/>
    </ItemGroup>

    <Target Name="PreBuild">
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>
    </Target>

    <Target Name="Compile" DependsOnTargets="PreBuild">
        <Csc Sources="@(CSFile)"
            References="@(Reference)"
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"
            TargetType="exe" />
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [如何：从生成中排除文件](../msbuild/how-to-exclude-files-from-the-build.md)
- [项](../msbuild/msbuild-items.md)
