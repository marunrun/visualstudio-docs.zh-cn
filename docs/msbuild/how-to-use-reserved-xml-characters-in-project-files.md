---
title: 如何：在项目文件中使用保留的 XML 字符 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, using reserved XML characters
- MSBuild, reserved XML characters
ms.assetid: 1ae37275-96bf-4e6e-897b-6b048e5bbe93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c79dfa33af5e0e80db682f272c5673856dbbcd8d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840377"
---
# <a name="how-to-use-reserved-xml-characters-in-project-files"></a>如何：在项目文件中使用保留的 XML 字符
在创作项目文件时，可能需要使用保留的 XML 字符，例如在属性值或任务参数值中。 但是，某些保留字符必须替换为命名实体，以便可以分析项目文件。

## <a name="use-reserved-characters"></a>使用保留字符
 下表介绍必须替换为相应命名实体的保留的 XML 字符，以便可以分析项目文件。

|保留字符|命名实体|
|------------------------|------------------|
|\<|&amp;lt;|
|>|&amp;gt;|
|&|&amp;amp;|
|"|&amp;quot;|
|'|&amp;apos;|

#### <a name="to-use-double-quotes-in-a-project-file"></a>在项目文件中使用双引号

- 将双引号替换为相应的命名实体 &amp;quot;。 例如，若要在 `EXEFile` 项列表两边放置双引号，请键入：

    ```xml
    <Message Text="The output file is &quot;@(EXEFile)&quot;."/>
    ```

## <a name="example"></a>示例
 在以下代码示例中，双引号用于在由项目文件输出的消息中突出显示文件名。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <!-- Set the application name as a property -->
    <PropertyGroup>
        <appname>"HelloWorldCS"</appname>
    </PropertyGroup>
    <!-- Specify the inputs -->
    <ItemGroup>
        <CSFile Include = "consolehwcs1.cs" />
    </ItemGroup>
    <Target Name = "Compile">
        <!-- Run the Visual C# compilation using input
        files of type CSFile -->
        <Csc Sources = "@(CSFile)">
            <!-- Set the OutputAssembly attribute of the CSC task
            to the name of the executable file that is created -->
            <Output
                TaskParameter = "OutputAssembly"
                ItemName = "EXEFile"/>
        </Csc>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is &quot;@(EXEFile)&quot;."/>
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
