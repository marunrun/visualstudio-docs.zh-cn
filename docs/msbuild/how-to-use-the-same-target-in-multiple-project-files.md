---
title: 如何：在多个项目文件中使用同一目标 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, importing
- MSBuild, using the same target in multiple project files
ms.assetid: 163734bd-1bfd-4093-a730-7741fc21742d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1b7b36a829e2e406ecd3f10ba3a2b588c6f7df25
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633754"
---
# <a name="how-to-use-the-same-target-in-multiple-project-files"></a>如何：在多个项目文件中使用同一目标

如果你创建了若干个 MSBuild 项目文件后，或许发现自己可能需要在不同项目文件中使用相同的任务和目标。 无需将这些任务或目标的完整说明包含在每个项目文件中，相反，你可以将目标保存在单独的项目文件中，然后将该项目导入任何需要使用该目标的其他项目。
## <a name="use-the-import-element"></a>使用 Import 元素

 `Import` 元素用于将一个项目文件插入另一个项目文件中。 导入的项目文件必须是有效的 MSBuild 项目文件，并包含格式标准的 XML。 `Project` 属性指定已导入的项目文件的路径。 有关 `Import` 元素的详细信息，请参阅 [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)。
`Import` 元素用于将一个项目文件插入另一个项目文件中。 导入的项目文件必须是有效的 MSBuild 项目文件，并包含格式标准的 XML。 `Project` 属性指定已导入的项目文件的路径。 有关 `Import` 元素的详细信息，请参阅 [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)。

#### <a name="to-import-a-project"></a>导入项目

1. 在正在导入的项目文件中，定义所有在已导入项目中作为属性和项的参数使用的属性和项。

2. 使用 `Import` 元素导入项目。 例如：

     `<Import Project="MyCommon.targets"/>`

3. 在 `Import` 元素之后定义所有属性和项，它们必须替代已导入项目中属性和项的默认定义。

## <a name="order-of-evaluation"></a>计算顺序

 当 MSBuild 到达 `Import` 元素后，已导入项目将有效地插入位于 `Import` 元素所处位置的正在导入的项目中。 因此，`Import` 元素的位置可能会影响属性和项的值。 请务必了解已导入项目所设置的属性和项，以及已导入项目所使用的属性和项。

 当项目生成时，将首先评估所有属性，然后对项进行评估。 例如，下面的 XML 定义了已导入的项目文件 MyCommon.targets  ：

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <Name>MyCommon</Name>
    </PropertyGroup>

    <Target Name="Go">
        <Message Text="Name=$(Name)"/>
    </Target>
</Project>
```

 下面的 XML 定义了 MyApp.proj，它将导入 MyCommon.targets   ：

```xml
<Project
    DefaultTargets="Go"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <Name>MyApp</Name>
    </PropertyGroup>
    <Import Project="MyCommon.targets"/>
</Project>
```

 当项目生成时，将显示以下消息：

 `Name="MyCommon"`

 由于是在 MyApp.proj 中定义了属性 `Name` 之后才导入项目，所以 MyCommon.targets 中 `Name` 的定义将替代 MyApp.proj 中的定义    。 如果在定义属性名称之前导入项目，生成将显示以下消息：

 `Name="MyApp"`

#### <a name="use-the-following-approach-when-importing-projects"></a>在导入项目时使用以下方法

1. 在项目文件中，定义所有在已导入项目中作为属性和项的参数使用的属性和项。

2. 导入项目。

3. 在项目文件中定义所有属性和项，它们必须替代已导入项目中属性和项的默认定义。

## <a name="example"></a>示例

 下面的代码示例演示了第二个代码示例所导入的 MyCommon.targets 文件  。 .targets 文件将评估正在导入的项目中的属性，以配置生成  。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <Flavor Condition="'$(Flavor)'==''">DEBUG</Flavor>
        <Optimize Condition="'$(Flavor)'=='RETAIL'">yes</Optimize>
        <appname>$(MSBuildProjectName)</appname>
    <PropertyGroup>
    <Target Name="Build">
        <Csc Sources="hello.cs"
            Optimize="$(Optimize)"
            OutputAssembly="$(appname).exe"/>
    </Target>
</Project>
```

## <a name="example"></a>示例

 下面的代码示例将导入 MyCommon.targets 文件  。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <Flavor>RETAIL</Flavor>
    </PropertyGroup>
    <Import Project="MyCommon.targets"/>
</Project>
```

## <a name="see-also"></a>请参阅

- [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)
- [目标](../msbuild/msbuild-targets.md)
