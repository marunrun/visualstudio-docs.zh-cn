---
title: 如何：生成具有资源的项目 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- resource files, compiling with MSBuild
- resources [Visual Studio], compiling with MSBuild
- projects [.NET Framework], building
- MSBuild, building a project with resources
ms.assetid: d07ac73f-2c2d-4e9a-812a-6dcb632bafe2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 626db2638912c9eaa49ea74e702c9ba24f6fd33f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75576337"
---
# <a name="how-to-build-a-project-that-has-resources"></a>如何：生成具有资源的项目
如果你正在构建一个项目的本地化版本，则所有用户界面元素必须都分入不同语言的资源文件。 如果该项目仅使用字符串，则资源文件使用文本文件。 或者，可以将 .resx 文件用作资源文件  。

## <a name="compile-resources-with-msbuild"></a>使用 MSBuild 编译资源
随 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 提供的常见任务库包括可用于编译 .resx 或文本文件中资源的 `GenerateResource` 任务  。 此任务包括用于指定要编译的资源文件的 `Sources` 参数，以及用于指定输出资源文件名称的 `OutputResources` 参数。 有关 `GenerateResource` 任务的详细信息，请参阅 [GenerateResource 任务](../msbuild/generateresource-task.md)。

#### <a name="to-compile-resources-with-msbuild"></a>使用 MSBuild 编译资源

1. 确定项目的资源文件，并将它们作为项列表或文件名传递给 `GenerateResource` 任务。

2. 指定 `GenerateResource` 任务的 `OutputResources` 参数，这允许你设置输出资源文件的名称。

3. 使用该任务的 `Output` 元素来在一个项中存储 `OutputResources` 参数的值。

4. 将 `Output` 元素创建的项用作另一项任务的输入。

## <a name="example"></a>示例
以下代码示例演示 `Output` 元素如何指定 `GenerateResource` 任务的 `OutputResources` 属性将包含已编译的资源文件 alpha.resources 和 beta.resources，且这两个文件将放在 `Resources` 项列表内   。 通过将这些 .resources 文件识别为具有相同名称的项的集合，你可以轻松地将它们用作另一个任务（如 [Csc](../msbuild/csc-task.md) 任务）的输入  。

此任务相当于使用适用于 [Resgen.exe](/dotnet/framework/tools/resgen-exe-resource-file-generator) 的 **/compile** 开关：

`Resgen.exe /compile alpha.resx,alpha.resources /compile beta.txt,beta.resources`

```xml
<GenerateResource
    Sources="alpha.resx; beta.txt"
    OutputResources="alpha.resources; beta.resources">
    <Output TaskParameter="OutputResources"
        ItemName="Resources"/>
</GenerateResource>
```

## <a name="example"></a>示例
以下示例项目包含两个任务：用于编译资源的 `GenerateResource` 任务和用于编译源代码文件和已编译的资源文件的 `Csc` 任务。 `GenerateResource` 任务编译的资源文件存储在 `Resources` 项中，且传递给 `Csc` 任务。

```xml
<Project DefaultTargets = "Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <Target Name="Resources">
        <GenerateResource
            Sources="alpha.resx; beta.txt"
            OutputResources="alpha.resources; beta.resources">
            <Output TaskParameter="OutputResources"
                ItemName="Resources"/>
        </GenerateResource>
    </Target>

    <Target Name="Build" DependsOnTargets="Resources">
        <Csc Sources="hello.cs"
                Resources="@(Resources)"
                OutputAssembly="hello.exe"/>
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [MSBuild](../msbuild/msbuild.md)
- [GenerateResource 任务](../msbuild/generateresource-task.md)
- [Csc 任务](../msbuild/csc-task.md)
- [Resgen.exe（资源文件生成器）](/dotnet/framework/tools/resgen-exe-resource-file-generator)
