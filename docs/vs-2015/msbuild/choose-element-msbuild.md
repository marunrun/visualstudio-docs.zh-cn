---
title: Choose 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Choose
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Choose> Element [MSBuild]
- Choose Element [MSBuild]
ms.assetid: 7b8b025a-d944-4f5c-9018-c89fc2ef146d
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 642a4996b9b7cb24ead5b58e8f3f98b8abf7657c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187001"
---
# <a name="choose-element-msbuild"></a>Choose 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

评估子元素，选择一组 `ItemGroup` 元素和/或 `PropertyGroup` 元素进行评估。  
  
 \<Project>  
 \<Choose>  
 \<When>  
 \<Choose>  
 ...  
 \<Otherwise>  
 \<Choose>  
 ...  
  
## <a name="syntax"></a>语法  
  
```  
<Choose>  
    <When Condition="'StringA'=='StringB'">... </When>  
    <Otherwise>... </Otherwise>  
</Choose>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Otherwise](../msbuild/otherwise-element-msbuild.md)|可选元素。<br /><br /> 当所有 `When` 元素的条件的计算结果为 `false` 时，指定要计算的代码块 `PropertyGroup` 和 `ItemGroup` 元素。 `Choose` 元素中可能没有或只有一个 `Otherwise` 元素，并且它必须是最后一个元素。|  
|[When](../msbuild/when-element-msbuild.md)|必需的元素。<br /><br /> 指定一个可能的代码块供 `Choose` 元素选择。 `Choose` 元素中可能有一个或多个 `When` 元素。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Otherwise](../msbuild/otherwise-element-msbuild.md)|当所有 `When` 元素的条件的计算结果为 `false` 时，指定要执行的代码块。|  
|[Project](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件必需的根元素。|  
|[When](../msbuild/when-element-msbuild.md)|指定一个可能的代码块供 `Choose` 元素选择。|  
  
## <a name="remarks"></a>备注  
 `Choose`、`When` 和 `Otherwise` 元素一起用来提供一种方式，通过这种方式选择代码的一部分来执行许多种可能的替代选择。 有关详细信息，请参阅[条件构造](../msbuild/msbuild-conditional-constructs.md)。  
  
## <a name="example"></a>示例  
 以下项目使用 `Choose` 元素来选择要在 `When` 元素中设置的属性值组。 如果两个 `When` 元素的 `Condition` 属性的计算结果均为 `false`，则将设置 `Otherwise` 元素中的属性值。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
    <PropertyGroup>  
        <Configuration Condition="'$(Configuration)' == ''">Debug</Configuration>  
        <OutputType>Exe</OutputType>  
        <RootNamespace>ConsoleApplication1</RootNamespace>  
        <AssemblyName>ConsoleApplication1</AssemblyName>  
        <WarningLevel>4</WarningLevel>  
    </PropertyGroup>  
    <Choose>  
        <When Condition=" '$(Configuration)'=='debug' ">  
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
        <Otherwise>  
            <PropertyGroup>  
                <DebugSymbols>true</DebugSymbols>  
                <Optimize>false</Optimize>  
                <OutputPath>.\bin\$(Configuration)\</OutputPath>  
                <DefineConstants>DEBUG;TRACE</DefineConstants>  
            </PropertyGroup>  
        </Otherwise>  
    </Choose>  
    <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [条件构造](../msbuild/msbuild-conditional-constructs.md)   
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
