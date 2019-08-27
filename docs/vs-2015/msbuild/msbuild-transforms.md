---
title: MSBuild 转换 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bcfc3c-14fa-455e-805c-63ccffa4a3bf
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f9a6f7985e3ebb3e77dcc605157f75e00a0842b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426040"
---
# <a name="msbuild-transforms"></a>MSBuild 转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

转换是指采用一对一的方式将一个项列表转换为另一项列表。 通过转换，不仅项目可以转换项列表，而且目标还可以标识其输入和输出之间的直接映射。 本主题介绍转换以及 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 如何使用转换更有效地生成项目。  
  
## <a name="transform-modifiers"></a>转换修饰符  
 转换并不是任意的，而是受特殊语法的限制，其中所有的转换修饰符都必须采用 %(ItemMetaDataName) 格式。 任何项元数据都可用作转换修饰符。 这包括在创建每个项时为其分配的常见项元数据。 要获得常见项元数据的列表，请参阅[常见项元数据](../msbuild/msbuild-well-known-item-metadata.md)。  
  
 在以下示例中，.resx 文件列表会转换为 .resources 文件列表。 %(Filename) 转换修饰符指定每个 .resources 文件与相应的 .resx 文件具有相同的文件名。  
  
```  
@(RESXFile->'%(filename).resources')  
```  
  
> [!NOTE]
> 可以为转换后的项列表指定自定义分隔符，其采用的方式与为标准项列表指定分隔符的相同。 例如，要使用逗号 (,) 而非默认的分号 (;) 分隔转换后的项列表，请使用下面的 XML。  
  
```  
@(RESXFile->'Toolset\%(filename)%(extension)', ',')  
```  
  
 例如，如果 @(RESXFile) 项列表中的各项为 `Form1.resx`、`Form2.resx` 和 `Form3.resx`，则转换后的列表中的输出为 `Form1.resources`、`Form2.resources` 和 `Form3.resources`。  
  
## <a name="using-multiple-modifiers"></a>使用多个修饰符  
 转换表达式可包含多个修饰符，这些修饰符可按任何顺序组合，还可重复使用。 在以下示例中，包含文件的目录的名称会更改，但文件会保留原来的名称和文件扩展名。  
  
```  
@(RESXFile->'Toolset\%(filename)%(extension)')  
```  
  
 例如，如果 `RESXFile` 项列表中包含的各项为 `Project1\Form1.resx`、`Project1\Form2.resx` 和 `Project1\Form3.text`，则转换后的列表中的输出为 `Toolset\Form1.resx`、`Toolset\Form2.resx` 和 `Toolset\Form3.text`。  
  
## <a name="dependency-analysis"></a>依赖项分析  
 转换可保证在转换后的项列表和原来的项列表之间存在一对一的映射关系。 因此，如果目标创建的输出转换为输入，[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 就可分析输入和输出的时间戳，并确定是否跳过、生成或部分重新生成目标。  
  
 在以下示例的[复制任务](../msbuild/copy-task.md)中，`BuiltAssemblies` 项列表中的每个文件都会映射到该任务目标文件夹中的某个文件，使用 `Outputs` 属性中的转换可指定该文件。 如果 `BuiltAssemblies` 项列表中的某个文件发生更改，则 `Copy` 任务会仅针对已更改的文件运行，并跳过所有其他文件。 有关依赖项分析和如何使用转换的详细信息，请参阅[如何：以增量方式生成](../msbuild/how-to-build-incrementally.md)。  
  
```  
<Target Name="CopyOutputs"  
    Inputs="@(BuiltAssemblies)"  
    Outputs="@(BuiltAssemblies -> '$(OutputPath)%(Filename)%(Extension)')">  
  
    <Copy  
        SourceFiles="@(BuiltAssemblies)"  
        DestinationFolder="$(OutputPath)"/>  
  
</Target>  
```  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 以下示例演示使用转换的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件。 此示例假定 c:\sub0\sub1\sub2\sub3 目录中只存在一个 .xsd 文件，工作目录为 c:\sub0。  
  
### <a name="code"></a>代码  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Schema Include="sub1\**\*.xsd"/>  
    </ItemGroup>  
  
    <Target Name="Messages">  
        <Message Text="rootdir: @(Schema->'%(rootdir)')"/>  
        <Message Text="fullpath: @(Schema->'%(fullpath)')"/>  
        <Message Text="rootdir + directory + filename + extension: @(Schema->'%(rootdir)%(directory)%(filename)%(extension)')"/>  
        <Message Text="identity: @(Schema->'%(identity)')"/>  
        <Message Text="filename: @(Schema->'%(filename)')"/>  
        <Message Text="directory: @(Schema->'%(directory)')"/>  
        <Message Text="relativedir: @(Schema->'%(relativedir)')"/>  
        <Message Text="extension: @(Schema->'%(extension)')"/>  
    </Target>  
</Project>  
```  
  
### <a name="comments"></a>注释  
 本示例生成以下输出。  
  
```  
rootdir: C:\  
fullpath: C:\xmake\sub1\sub2\sub3\myfile.xsd  
rootdir + directory + filename + extension: C:\xmake\sub1\sub2\sub3\myfile.xsd  
identity: sub1\sub2\sub3\myfile.xsd  
filename: myfile  
directory: xmake\sub1\sub2\sub3\  
relativedir: sub1\sub2\sub3\  
extension: .xsd  
```  
  
## <a name="see-also"></a>请参阅  
 [MSBuild 概念](../msbuild/msbuild-concepts.md)   
 [MSBuild 参考](../msbuild/msbuild-reference.md)   
 [如何：增量生成](../msbuild/how-to-build-incrementally.md)
