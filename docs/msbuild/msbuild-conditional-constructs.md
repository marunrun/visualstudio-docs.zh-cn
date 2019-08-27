---
title: MSBuild 条件构造 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Choose> Element [MSBuild]
- Choose Element [MSBuild]
- conditional constructs [MSBuild]
- MSBuild, conditional constructs
- <When> Element [MSBuild]
- <Otherwise> Element [MSBuild]
- Otherwise Element [MSBuild]
- When Element [MSBuild]
ms.assetid: dd54258e-f4fb-448f-9da4-d1817e0cbaf2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 045a7366546e85ad2e9588ce2a14077f8b18a331
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842555"
---
# <a name="msbuild-conditional-constructs"></a>MSBuild 条件构造
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 为非此即彼的处理机制提供 [Choose](../msbuild/choose-element-msbuild.md)、[When](../msbuild/when-element-msbuild.md) 和 [Otherwise](../msbuild/otherwise-element-msbuild.md) 元素。

## <a name="use-the-choose-element"></a>使用 Choose 元素
 `Choose` 元素包含一系列具有 `Condition` 属性的 `When` 元素，这些元素按照从顶部到底部的顺序进行测试，直到一个元素的计算结果为 `true`。 如果多个 `When` 元素的计算结果为 `true`，则只使用第一个。 如果 `When` 元素的任何条件的计算结果均为 `true`，则评估 `Otherwise` 元素（如存在）。

 `Choose` 元素可用作 `Project`、`When` 和 `Otherwise` 元素的子元素。 `When` 和 `Otherwise` 元素可具有 `ItemGroup`、`PropertyGroup` 或 `Choose` 子元素。

## <a name="example"></a>示例
 以下示例使用 `Choose` 和 `When` 元素进行非此即彼的处理。 根据 `Configuration` 属性的值设置项目的属性和项。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <OutputType>Exe</OutputType>
        <RootNamespace>ConsoleApplication1</RootNamespace>
        <AssemblyName>ConsoleApplication1</AssemblyName>
        <WarningLevel>4</WarningLevel>
    </PropertyGroup>
    <Choose>
        <When Condition=" '$(Configuration)'=='Debug' ">
            <PropertyGroup>
                <DebugSymbols>true</DebugSymbols>
                <DebugType>full</DebugType>
                <Optimize>false</Optimize>
                <OutputPath>.\bin\Debug\</OutputPath>
                <DefineConstants>DEBUG;TRACE</DefineConstants>
            </PropertyGroup>
            <ItemGroup>
                <Compile Include="UnitTesting\*.cs" />
                <Reference Include="NUnit.dll" />
            </ItemGroup>
        </When>
        <When Condition=" '$(Configuration)'=='retail' ">
            <PropertyGroup>
                <DebugSymbols>false</DebugSymbols>
                <Optimize>true</Optimize>
                <OutputPath>.\bin\Release\</OutputPath>
                <DefineConstants>TRACE</DefineConstants>
            </PropertyGroup>
        </When>
    </Choose>
    <!-- Rest of Project -->
</Project>
```

## <a name="see-also"></a>请参阅
- [Choose 元素 (MSBuild)](../msbuild/choose-element-msbuild.md)
- [When 元素 (MSBuild)](../msbuild/when-element-msbuild.md)
- [Otherwise 元素 (MSBuild)](../msbuild/otherwise-element-msbuild.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)