---
title: Import 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Import
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Import element [MSBuild]
- <Import> element [MSBuild]
ms.assetid: 3bfecaf1-69fd-4008-b651-c9dafd4389d9
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 13ffaff052e672eb900d5ed3a1ce5ae7c2a370df
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75573988"
---
# <a name="import-element-msbuild"></a>Import 元素 (MSBuild)
将一个项目文件的内容导入其他项目文件中。

\<Project> \<Import>

## <a name="syntax"></a>语法

```xml
<Import Project="ProjectPath"
    Condition="'String A'=='String B'" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Project`|必需的特性。<br /><br /> 要导入的项目文件的路径。 该路径可以包含通配符。 匹配文件按排序顺序导入。 使用此功能时，只需通过将代码文件添加到目录，即可将代码添加到项目。|
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|
|`Sdk`| 可选特性。<br /><br /> 引用项目 SDK。|

### <a name="child-elements"></a>子元素
 None

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| - | - |
| [Project](../msbuild/project-element-msbuild.md) | [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目文件必需的根元素。 |
| [ImportGroup](../msbuild/importgroup-element.md) | 包含在可选条件下进行分组的 `Import` 元素的集合。 |

## <a name="remarks"></a>备注
 使用 `Import` 元素可以重复使用对许多项目文件通用的代码。 这样可以更轻松地维护代码，因为对共享的代码进行的任何更新都会传播到导入它的所有项目。

 按照约定，共享导入项目文件会保存为 .targets 文件，但它们是标准 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目文件  。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 不会阻止导入具有不同文件扩展名的项目，但是我们建议使用 .targets 扩展名以保持一致性  。

 导入项目中的相对路径会相对于导入项目的目录进行解释。 因此，如果项目文件导入位于不同位置的多个项目文件中，则导入项目文件中的相对路径对于每个导入项目会以不同方式进行解释。

 与导入项目中引用的项目文件相关的所有 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 保留属性（例如， `MSBuildProjectDirectory` 和 `MSBuildProjectFile`）都会基于导入项目文件进行赋值。

 如果导入项目没有 `DefaultTargets` 属性，则会按导入顺序检查导入项目，并使用发现的第一个 `DefaultTargets` 属性的值。 例如，如果 ProjectA 导入 ProjectB 和 ProjectC（按照该顺序），并且 ProjectB 导入 ProjectD，则 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 会首先查找 ProjectA 上指定的 `DefaultTargets` ，然后是 ProjectB，接下来是 ProjectD，最后是 ProjectC。

 导入项目的架构与标准项目相同。 虽然 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 可能能够生成导入项目，不过这不太可能，因为导入项目通常不包含有关要设置的属性或运行目标的顺序的信息。 导入项目依靠将它导入其中的项目来提供该信息。

## <a name="wildcards"></a>通配符
 在 .NET Framework 4 中，MSBuild 允许在项目属性中使用通配符。 存在通配符时，找到的所有匹配项会进行排序（实现可再现性），随后它们会按该顺序导入（如同显式设置了该顺序一样）。

 如果要提供一个扩展点，以便其他人可以导入文件而无需将文件名显式添加到导入文件，则这种行为十分有用。 因此，Microsoft.Common.Targets 在文件顶部包含以下行  。

```xml
<Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\$(MSBuildThisFile)\ImportBefore\*" Condition="'$(ImportByWildcardBeforeMicrosoftCommonTargets)' == 'true' and exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\$(MSBuildThisFile)\ImportBefore')"/>
```

## <a name="example"></a>示例
 下面的示例演示具有多个项和属性并导入常规项目文件的项目。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <resourcefile>Strings.resx</resourcefile>

        <compiledresources>
            $(O)\$(MSBuildProjectName).Strings.resources
        </compiledresources>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="*.cs" />

        <Reference Include="System" />
        <Reference Include="System.Data" />
    </ItemGroup>

    <Import Project="$(CommonLocation)\General.targets" />
</Project>
```

## <a name="see-also"></a>请参阅
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [如何：在多个项目文件中使用同一目标](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)
