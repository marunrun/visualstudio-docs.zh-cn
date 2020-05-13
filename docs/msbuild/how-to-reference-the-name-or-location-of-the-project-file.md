---
title: 如何：引用项目文件的名称或位置 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- locations, referencing
- locations
- MSBuildProjectName property
- MSBuild, referencing the project file
- names, referencing
- reserved properties
- project files, referencing
ms.assetid: c8fcc594-5d37-4e2e-b070-4d9c012043b5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b54a63b135f844ff20b45ffac430662c4df1f19
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633832"
---
# <a name="how-to-reference-the-name-or-location-of-the-project-file"></a>如何：引用项目文件的名称或位置

可以在项目文件自身中使用该项目的名称或位置，而无需创建你自己的属性。 MSBuild 提供引用项目文件名的保留属性和与项目相关的其他属性。 有关保留属性的详细信息，请参阅 [MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)。

## <a name="use-the-project-properties"></a>使用项目属性

 MSBuild 提供一些可在项目文件中使用而无需每次都对其进行定义的保留属性。 例如，保留属性 `MSBuildProjectName` 提供对项目文件名的引用。 保留属性 `MSBuildProjectDirectory` 提供对项目文件位置的引用。

#### <a name="to-use-the-project-properties"></a>使用项目属性

- 使用 $() 表示法在项目文件中引用属性，就像引用任何其他属性一样。 例如：

  ```xml
  <CSC Sources = "@(CSFile)"
      OutputAssembly = "$(MSBuildProjectName).exe"/>
  </CSC>
  ```

  使用保留属性的一个优点是对项目文件名所作的任何更改都将自动纳入。 下次生成项目时，输出文件将具有该新名称，而你不需要执行任何进一步的操作。

  有关如何在文件或项目引用中使用特殊字符的详细信息，请参阅 [MSBuild 特殊字符](../msbuild/msbuild-special-characters.md)。

> [!NOTE]
> 无法在项目文件中重新定义保留属性。

## <a name="example"></a>示例

 以下示例项目文件将项目名称作为保留属性引用，以指定输出的名称。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"
    DefaultTargets = "Compile">

    <!-- Specify the inputs -->
    <ItemGroup>
        <CSFile Include = "consolehwcs1.cs"/>
     </ItemGroup>
    <Target Name = "Compile">
        <!-- Run the Visual C# compilation using
        input files of type CSFile -->
        <CSC Sources = "@(CSFile)"
            OutputAssembly = "$(MSBuildProjectName).exe" >
            <!-- Set the OutputAssembly attribute of the CSC task
            to the name of the project -->
            <Output
                TaskParameter = "OutputAssembly"
                ItemName = "EXEFile" />
        </CSC>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is @(EXEFile)"/>
    </Target>
</Project>
```

## <a name="example"></a>示例

 以下示例项目文件使用 `MSBuildProjectDirectory` 保留属性来创建项目文件位置中文件的完整路径。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <!-- Build the path to a file in the root of the project -->
    <PropertyGroup>
        <NewFilePath>$([System.IO.Path]::Combine($(MSBuildProjectDirectory), `BuildInfo.txt`))</NewFilePath>
    </PropertyGroup>
</Project>
```

该示例使用[属性函数](property-functions.md)语法来调用静态 .NET Framework 方法 <xref:System.IO.Path.Combine*?displayProperty=fullName>。

## <a name="see-also"></a>请参阅

- [MSBuild](../msbuild/msbuild.md)
- [MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)
