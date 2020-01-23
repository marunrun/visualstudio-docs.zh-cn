---
title: 如何：从生成中排除文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, wildcards
- MSBuild, excluding files
- wildcards, MSBuild
ms.assetid: 1be36e45-01da-451c-972d-f9fc0e7d663c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3c55033d253b5c7dfeb2bed968f2418637ca3f0d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75576051"
---
# <a name="how-to-exclude-files-from-the-build"></a>如何：从生成中排除文件
在项目文件中，可以使用通配符将所有文件包括在一个目录或一组嵌套目录中，以作为生成的输入。 但是，对于目录中的某个文件或嵌套目录中的某个目录，你可能并不希望将其作为生成的输入包括在内。 你可以从输入列表中显示排除该文件或目录。 有些时候，你只希望在特定情况下才包括项目中的某个文件。 那么你可以显式声明将文件包括在生成中的条件。

## <a name="exclude-a-file-or-directory-from-the-inputs-for-a-build"></a>从生成的输入中排除文件或目录
 项列表是生成的输入文件。 要包括的项是使用 `Include` 属性单独或作为组声明的。 例如：

```xml
<CSFile Include="Form1.cs"/>
<CSFile Include ="File1.cs;File2.cs"/>
<CSFile Include="*.cs"/>
<JPGFile Include="Images\**\*.jpg"/>
```

 如果你已使用通配符将所有文件包括在一个目录或一组嵌套的目录中以作为生成的输入，但对于目录中的某个文件或嵌套目录中的某个目录，你可能并不希望将其包括在内。 若要从项列表中排除某个项，可使用 `Exclude` 属性。

#### <a name="to-include-all-cs-or-vb-files-except-form2"></a>包括除 Form2 以外的所有.cs 或.vb 文件   

- 使用以下 `Include` 和 `Exclude` 属性之一：

    ```xml
    <CSFile Include="*.cs" Exclude="Form2.cs"/>
    ```

    or

    ```xml
    <VBFile Include="*.vb" Exclude="Form2.vb"/>
    ```

#### <a name="to-include-all-cs-or-vb-files-except-form2-and-form3"></a>包括除 Form2 和 Form3 以外的所有.cs 或.vb 文件    

- 使用以下 `Include` 和 `Exclude` 属性之一：

    ```xml
    <CSFile Include="*.cs" Exclude="Form2.cs;Form3.cs"/>
    ```

    or

    ```xml
    <VBFile Include="*.vb" Exclude="Form2.vb;Form3.vb"/>
    ```

#### <a name="to-include-all-jpg-files-in-subdirectories-of-the-images-directory-except-those-in-the-version2-directory"></a>包括除 Version2 目录中的 .jpg 文件以外，图像目录子目录中的所有 .jpg 文件   

- 使用以下 `Include` 和 `Exclude` 属性：

    ```xml
    <JPGFile
        Include="Images\**\*.jpg"
        Exclude = "Images\**\Version2\*.jpg"/>
    ```

    > [!NOTE]
    > 必须指定这两个属性的路径。 如果你使用绝对路径在 `Include` 属性中指定文件位置，那么在 `Exclude` 属性中也必须使用绝对路径；如果你在 `Include` 属性中使用相对路径，那么在 `Exclude` 属性中也必须使用相对路径。

## <a name="use-conditions-to-exclude-a-file-or-directory-from-the-inputs-for-a-build"></a>使用条件从生成的输入中排除文件或目录
 如果你希望在调试生成中包括某些项，而不希望在发布生成中包括这些项，则可以使用 `Condition` 属性来指定包括该项的条件。

#### <a name="to-include-the-file-formulavb-only-in-release-builds"></a>仅在发布生成中包括文件 Formula.vb 

- 使用类似于如下的 `Condition` 属性：

    ```xml
    <Compile
        Include="Formula.vb"
        Condition=" '$(Configuration)' == 'Release' " />
    ```

## <a name="example"></a>示例
 以下代码示例生成一个项目，其中包括除 Form2.cs 以外目录中的所有 .cs 文件   。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <PropertyGroup>
        <builtdir>built</builtdir>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="*.cs" Exclude="Form2.cs"/>

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
- [项](../msbuild/msbuild-items.md)
- [MSBuild](../msbuild/msbuild.md)
- [如何：选择要生成的文件](../msbuild/how-to-select-the-files-to-build.md)
