---
title: 如何：增量生成 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, incremental builds
- incremental builds
- MSBuild, building incrementally
ms.assetid: 8d82d7d8-a2f1-4df6-9d2f-80b9e0cb3ac3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e78ce202c04b8b2af60a7b3d09b149c7e02f2e50
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977366"
---
# <a name="how-to-build-incrementally"></a>如何：增量生成
生成一个大项目时，不重新生成以前生成过但仍然为最新状态的组件十分重要。 如果每次都生成所有目标，则每次生成都需要很长时间才能完成。 为了启用增量生成（这类生成仅重新生成以前未生成过或已过期的目标）， [!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] ([!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]) 可以对输入文件的时间戳和输出文件的时间戳进行比较，并确定是跳过、生成还是部分重新生成某个目标。 但是，在输入和输出之间必须存在一对一映射。 可以使用转换来使目标能够识别此直接映射。 有关转换的详细信息，请参阅[转换](../msbuild/msbuild-transforms.md)。

## <a name="specify-inputs-and-outputs"></a>指定输入和输出
如果项目文件中指定了输入和输出，可以增量生成目标。

#### <a name="to-specify-inputs-and-outputs-for-a-target"></a>指定目标的输入和输出

- 使用 `Target` 元素的 `Inputs` 和 `Outputs` 属性。 例如:

  ```xml
  <Target Name="Build"
      Inputs="@(CSFile)"
      Outputs="hello.exe">
  ```

  [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 可以对输入文件的时间戳和输出文件的时间戳进行比较，并确定是跳过、生成还是部分重新生成某个目标。 在下面的示例中，如果 `@(CSFile)` 项列表中有任何文件比 hello.exe 文件新，则 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 将运行该目标；否则将跳过它：

```xml
<Target Name="Build"
    Inputs="@(CSFile)"
    Outputs="hello.exe">

    <Csc
        Sources="@(CSFile)"
        OutputAssembly="hello.exe"/>
</Target>
```

当目标中指定了输入和输出时，要么每个输出只能映射到一个输入，要么在输出和输入之间不能有任何直接映射。 例如，在前面的 [Csc 任务](../msbuild/csc-task.md)中，输出 hello.exe 不能映射到任何单一输入，因为它依赖于所有输入。

> [!NOTE]
> 对于输入和输出之间不存在直接映射的目标，它的生成频率总是比每个输出只能映射到一个输入的目标高，因为如果某些输入发生了更改， [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 无法确定需要重新生成哪些输出。

输出和输入之间存在直接映射的任务（如 [LC 任务](../msbuild/lc-task.md)）最适合增量生成；而 [Csc](../msbuild/csc-task.md) 和 [Vbc](../msbuild/vbc-task.md) 等任务则与上述任务存在差异，对于此类任务，多个输入才能产生一个输出程序集。

## <a name="example"></a>示例
以下示例使用的项目为假设的帮助系统生成帮助文件。 执行该项目时，会将 .txt 源文件转换为 .content 中间文件，随后，.content 中间文件与 XML 元数据文件合并，生成帮助系统使用的 .help 最终文件。 该项目使用以下假设任务：

- `GenerateContentFiles`：将 .txt 文件转换成 .content 文件。

- `BuildHelp`：将 .content 文件与 XML 元数据文件合并，生成 .help 最终文件。

该项目通过转换过程来建立 `GenerateContentFiles` 任务中输入和输出之间的一一映射。 有关详细信息，请参阅[转换](../msbuild/msbuild-transforms.md)。 此外，设置了 `Output` 元素，以便自动将 `GenerateContentFiles` 任务的输出用作 `BuildHelp` 任务的输入。

此项目文件包含 `Convert` 和 `Build` 目标。 `GenerateContentFiles` 和 `BuildHelp` 任务分别位于 `Convert` 和 `Build` 目标中，以便可以增量生成每个目标。 通过使用 `Output` 元素，将 `GenerateContentFiles` 任务的输出放入 `ContentFile` 项列表中，这样，就可以将这些输出用作 `BuildHelp` 任务的输入。 通过按此方法使用 `Output` 元素，可自动将一个任务的输出作为另一个任务的输入，这样就不必在每个任务中手动列出各个项或项列表。

> [!NOTE]
> 尽管可增量生成 `GenerateContentFiles` 目标，但该目标的所有输出始终都需要作为 `BuildHelp` 目标的输入。 使用 `Output` 元素时，[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 会自动将一个目标中的所有输出作为另一个目标的输入提供。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <ItemGroup>
        <TXTFile Include="*.txt"/>
        <XMLFiles Include="\metadata\*.xml"/>
    </ItemGroup>

    <Target Name = "Convert"
        Inputs="@(TXTFile)"
        Outputs="@(TXTFile->'%(Filename).content')">

        <GenerateContentFiles
            Sources = "@(TXTFile)">
            <Output TaskParameter = "OutputContentFiles"
                ItemName = "ContentFiles"/>
        </GenerateContentFiles>
    </Target>

    <Target Name = "Build" DependsOnTargets = "Convert"
        Inputs="@(ContentFiles);@(XMLFiles)"
        Outputs="$(MSBuildProjectName).help">

        <BuildHelp
            ContentFiles = "@(ContentFiles)"
            MetadataFiles = "@(XMLFiles)"
            OutputFileName = "$(MSBuildProjectName).help"/>
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [目标](../msbuild/msbuild-targets.md)
- [Target 元素 (MSBuild)](../msbuild/target-element-msbuild.md)
- [转换](../msbuild/msbuild-transforms.md)
- [Csc 任务](../msbuild/csc-task.md)
- [Vbc 任务](../msbuild/vbc-task.md)
