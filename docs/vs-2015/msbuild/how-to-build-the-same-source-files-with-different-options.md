---
title: 如何：使用不同选项生成相同的源文件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- source files, building with different options
- MSBuild, properties
- project properties, modifying
- Hello World example [Visual Studio]
ms.assetid: d14f1212-ddd9-434f-b138-f840011b0fb2
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8bf76967363f4c0d97d93c895fbeb6209c8503f0
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821673"
---
# <a name="how-to-build-the-same-source-files-with-different-options"></a>如何：使用不同选项生成相同的源文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在生成项目时，你经常使用不同的生成选项编译相同的组件。 例如，你可以使用符号信息创建调试版本，或者使用无符号信息但启用优化来创建发布版本。 或者，可以生成项目，在某个特定平台（例如，x86 或[!INCLUDE[vcprx64](../includes/vcprx64-md.md)]）上运行。 在所有这些情况下，大部分生成选项保持不变；只更改几个选项以控制生成配置。 利用 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]，你可以使用属性和条件来创建不同的生成配置。  
  
## <a name="using-properties-to-modify-projects"></a>使用属性来修改项目  
 `Property` 元素定义在项目文件中多次引用的变量，如临时目录的位置，或者设置在多项配置中使用的属性的值，如调试版本和发布版本。 有关属性的详细信息，请参阅 [MSBuild 属性](msbuild-properties1.md)。  
  
 属性可用于你的生成的配置更改，而无需更改项目文件。 `Property` 元素和 `PropertyGroup` 元素的 `Condition` 属性允许你更改属性的值。 有关 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 条件的详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。  
  
#### <a name="to-set-a-group-of-properties-based-on-another-property"></a>设置一组属性（基于另一个属性）  
  
- 在 `PropertyGroup` 元素中使用 `Condition` 属性，类似以下代码：  
  
    ```  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
    ```  
  
#### <a name="to-define-a-property-based-on-another-property"></a>定义属性（基于另一个属性）  
  
- 在 `Property` 元素中使用 `Condition` 属性，类似以下代码：  
  
    ```  
    <DebugType Condition="'$(Flavor)'=='DEBUG'">full</DebugType>  
    ```  
  
## <a name="specifying-properties-on-the-command-line"></a>在命令行上指定属性  
 你的项目文件编写为接受多个配置后，你需要能够在生成项目时更改这些配置。 通过允许在命令行上使用 **/property** 或 **/p** 开关来指定属性，[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 可以提供此功能。  
  
#### <a name="to-set-a-project-property-at-the-command-line"></a>在命令行中设置项目属性  
  
- 使用 **/property** 开关以及属性和属性值。 例如:  
  
    ```  
    msbuild file.proj /property:Flavor=Debug  
    ```  
  
     \- 或 -  
  
    ```  
    Msbuild file.proj /p:Flavor=Debug  
    ```  
  
#### <a name="to-specify-more-than-one-project-property-at-the-command-line"></a>在命令行上指定多个项目属性  
  
- 多次使用 **/property** 或 **/p** 开关以及属性和属性值，或者使用一个 **/property** 或 **/p** 开关并使用分号 (;) 分隔多个属性。 例如：  
  
  ```  
  msbuild file.proj /p:Flavor=Debug;Platform=x86  
  ```  
  
   \- 或-  
  
  ```  
  msbuild file.proj /p:Flavor=Debug /p:Platform=x86  
  ```  
  
  环境变量也被视为属性，并且由 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 自动合并。 有关使用环境变量的详细信息，请参阅[如何：在生成中使用环境变量](../msbuild/how-to-use-environment-variables-in-a-build.md)。  
  
  在命令行中指定的属性值将优先于任何在项目文件中为同一属性设置的值，而项目文件中的值优先于环境变量中的值。  
  
  你可以通过使用项目标记中的 `TreatAsLocalProperty` 属性更改此行为。 对于列出具有该特性的属性名称，在命令行上指定的属性值并不优先于项目文件中的值。 你在本主题后面找到示例。  
  
## <a name="example"></a>示例  
 以下代码示例“Hello World”项目，包含两个可用于创建调试版本和发布版本的新属性组。  
  
 若要此项目的调试版本，请键入：  
  
```  
msbuild consolehwcs1.proj /p:flavor=debug  
```  
  
 若要此项目的零售版本，请键入：  
  
```  
msbuild consolehwcs1.proj /p:flavor=retail  
```  
  
```  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <!-- Sets the default flavor of an environment variable called   
    Flavor is not set or specified on the command line -->  
    <PropertyGroup>  
        <Flavor Condition="'$(Flavor)'==''">DEBUG</Flavor>  
    </PropertyGroup>  
  
    <!-- Define the DEBUG settings -->  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
  
    <!-- Define the RETAIL settings -->  
    <PropertyGroup Condition="'$(Flavor)'=='RETAIL'">  
        <DebugType>pdbonly</DebugType>  
        <Optimize>yes</Optimize>  
    </PropertyGroup>  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldCS</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using input files  
        of type CSFile -->  
        <CSC  Sources = "@(CSFile)"  
            DebugType="$(DebugType)"  
            Optimize="$(Optimize)"  
            OutputAssembly="$(appname).exe" >  
  
            <!-- Set the OutputAssembly attribute of the CSC  
            task to the name of the executable file that is   
            created -->  
            <Output TaskParameter="OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>示例  
 以下示例介绍如何使用 `TreatAsLocalProperty` 属性。 `Color` 属性在项目文件中的值为 `Blue`，在命令行中的值为 `Green`。 借助项目标记中的 `TreatAsLocalProperty="Color"`，命令行属性 (`Green`) 不会替代项目文件中定义的属性 (`Blue`)。  
  
 若要生成项目，请输入以下命令：  
  
```  
msbuild colortest.proj /t:go /property:Color=Green  
```  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
ToolsVersion="4.0" TreatAsLocalProperty="Color">  
  
    <PropertyGroup>  
        <Color>Blue</Color>  
    </PropertyGroup>  
  
    <Target Name="go">  
        <Message Text="Color: $(Color)" />  
    </Target>  
</Project>  
  
<!--  
  Output with TreatAsLocalProperty="Color" in project tag:  
     Color: Blue  
  
  Output without TreatAsLocalProperty="Color" in project tag:  
     Color: Green  
-->  
```  
  
## <a name="see-also"></a>请参阅  
[MSBuild](msbuild.md)  
 [MSBuild 概念](../msbuild/msbuild-concepts.md)   
 [MSBuild 参考](../msbuild/msbuild-reference.md)   
 [Project 元素 (MSBuild)](../msbuild/project-element-msbuild.md)
