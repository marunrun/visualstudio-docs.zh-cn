---
title: 扩展生成过程
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d22bf8af86605d414d933d16cd5dd7f8d24a6154
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62945882"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>如何：扩展 Visual Studio 生成过程
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成过程由导入到项目文件中的一系列 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] .targets 文件定义。 可扩展其中一个导入文件 Microsoft.Common.targets，以便在生成过程中的几个点上运行自定义任务。 本文介绍两种可用于扩展 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成过程的方法：

- 重写 Microsoft.Common.targets 中定义的特定预定义目标。

- 重写 Microsoft.Common.targets 中定义的“DependsOn”属性。

## <a name="override-predefined-targets"></a>重写预定义目标
Microsoft.Common.targets 文件包含一组预定义的空目标，会在生成过程中调用一些主要目标之前和之后调用这些空目标。 例如，[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 会在主 `CoreBuild` 目标和 `AfterBuild` 目标之前和 `CoreBuild` 目标之后调用 `BeforeBuild`。 Microsoft.Common.targets 中的空目标默认不执行任何操作，但可通过定义导入 Microsoft.Common.targets 的项目文件中所需的目标，重写这些空目标的默认行为。 通过重写预定义目标，可以使用 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 任务，更好地控制生成过程。

#### <a name="to-override-a-predefined-target"></a>重写预定义的目标

1. 标识 Microsoft.Common.targets 中需要重写的预定义目标。 请参阅下表，了解可安全重写的目标的完整列表。

2. 在项目文件末尾（紧接在 `</Project>` 标记之前）定义一个或多个目标。 例如:

    ```xml
    <Project>
        ...
        <Target Name="BeforeBuild">
            <!-- Insert tasks to run before build here -->
        </Target>
        <Target Name="AfterBuild">
            <!-- Insert tasks to run after build here -->
        </Target>
    </Project>
    ```

3. 生成项目文件。

下表显示 Microsoft.Common.targets 中可以安全重写的所有目标。

|目标名称|说明|
|-----------------|-----------------|
|`BeforeCompile`， `AfterCompile`|插入到这些目标之一中的任务，在完成内核编译之前或之后运行。 大多数自定义均在这两个目标之一中完成。|
|`BeforeBuild`， `AfterBuild`|插入到这些目标之一中的任务，在生成中所有其他任务之前或之后运行。 **注意：**`BeforeBuild` 和 `AfterBuild` 目标已在大多数项目文件的注释末尾定义，使你能够轻松向项目文件添加预生成和生成后事件。|
|`BeforeRebuild`， `AfterRebuild`|插入到这些目标之一中的任务，在调用内核重新生成功能之前或之后运行。 Microsoft.Common.targets 中的目标执行顺序是：`BeforeRebuild`、`Clean`、`Build`、`AfterRebuild`。|
|`BeforeClean`， `AfterClean`|插入到这些目标之一中的任务，在调用内核清理功能之前或之后运行。|
|`BeforePublish`， `AfterPublish`|插入到这些目标之一中的任务，在调用内核发布功能之前或之后运行。|
|`BeforeResolveReferences`， `AfterResolveReferences`|插入到这些目标之一中的任务，在解析程序集引用之前或之后运行。|
|`BeforeResGen`， `AfterResGen`|插入到这些目标之一中的任务，在生成资源之前或之后运行。|

## <a name="override-dependson-properties"></a>重写 DependsOn 属性
重写预定义的目标是一种用于扩展生成过程的简单方法，但由于 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 按顺序计算目标的定义，任何方法都无法阻止已导入你的项目的另一个项目重写你已重写的目标。 因此，例如，在导入所有其他项目后，会在生成过程中使用项目文件中定义的最后一个 `AfterBuild` 目标。

通过重写在整个 Microsoft.Common.targets 文件的 `DependsOnTargets` 特性中使用的“DependsOn”属性，可防止目标被意外重写。 例如，`Build` 目标包含 `"$(BuildDependsOn)"` 的 `DependsOnTargets` 属性值。 以此为例：

```xml
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>
```

这一段 XML 指示运行 `Build` 目标之前，必须首先运行 `BuildDependsOn` 属性中指定的所有目标。 `BuildDependsOn` 属性的定义如下：

```xml
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

通过在项目文件末尾声明另一个名为 `BuildDependsOn` 的属性，可以重写此属性值。 通过在新属性中包括以前的 `BuildDependsOn` 属性，可以将新的目标添加到目标列表的开头和结尾。 例如:

```xml
<PropertyGroup>
    <BuildDependsOn>
        MyCustomTarget1;
        $(BuildDependsOn);
        MyCustomTarget2
    </BuildDependsOn>
</PropertyGroup>

<Target Name="MyCustomTarget1">
    <Message Text="Running MyCustomTarget1..."/>
</Target>
<Target Name="MyCustomTarget2">
    <Message Text="Running MyCustomTarget2..."/>
</Target>
```

导入你的项目文件的项目可以在不覆盖已实现的自定义的情况下重写这些属性。

#### <a name="to-override-a-dependson-property"></a>重写 DependsOn 属性

1. 标识 Microsoft.Common.targets 中需要重写的预定义 DependsOn 属性。 请参阅下表，获取经常重写的 DependsOn 属性列表。

2. 在项目文件末尾定义一个或多个属性的另一个实例。 在新属性中包括原始属性，例如 `$(BuildDependsOn)`。

3. 在属性定义之前或之后定义自定义目标。

4. 生成项目文件。

### <a name="commonly-overridden-dependson-properties"></a>经常重写的 DependsOn 属性

|属性名称|说明|
|-------------------|-----------------|
|`BuildDependsOn`|在要在整个生成过程之前或之后插入自定义目标的情况下，要重写的属性。|
|`CleanDependsOn`|在要从自定义生成过程中清理输出的情况下，要重写的属性。|
|`CompileDependsOn`|在要在编译步骤之前或之后插入自定义过程的情况下，要重写的属性。|

## <a name="see-also"></a>请参阅
- [Visual Studio 集成](../msbuild/visual-studio-integration-msbuild.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [.targets 文件](../msbuild/msbuild-dot-targets-files.md)
