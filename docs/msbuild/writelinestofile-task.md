---
title: WriteLinesToFile 任务 | Microsoft Docs
ms.date: 09/20/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#WriteLinesToFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- WriteLinesToFile task [MSBuild]
- MSBuild, WriteLinesToFile task
ms.assetid: 9c8862ac-8da5-4437-9430-ecc30421f1c9
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b78ac2347a5143aeb532a4bcc294551430584b4a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77630660"
---
# <a name="writelinestofile-task"></a>WriteLinesToFile 任务

将指定项的路径写入指定的文本文件。

## <a name="task-parameters"></a>任务参数

 下表描述了 `WriteLinestoFile` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`File`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要将项写入到的文件。|
|`Lines`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要写入到文件的项。|
|`Overwrite`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，该任务覆盖文件中的任何现有内容。|
|`Encoding`|可选 `String` 参数。<br /><br /> 选择字符编码，例如“Unicode”。  另请参阅 <xref:System.Text.Encoding>。|
|`WriteOnlyWhenDifferent`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，便会指定目标文件（若有），并先读取它来与写入的任务进行比较。 如果完全相同，此文件就不会写入到磁盘中，并且会保留时间戳。|

## <a name="remarks"></a>备注

 如果 `Overwrite` 为 `true`，创建一个新文件，向其中写入内容，然后关闭文件。 如果目标文件已存在，则覆盖该文件。 如果 `Overwrite` 为 `false`会将内容追加到文件中，如果目标文件还不存在则创建该文件。

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

 以下示例使用 `WriteLinesToFile` 任务，将 `MyItems` 项集合中项的路径写入到 `MyTextFile` 项集合指定的文件中。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MyTextFile Include="Items.txt"/>
        <MyItems Include="*.cs"/>
    </ItemGroup>

    <Target Name="WriteToFile">
        <WriteLinesToFile
            File="@(MyTextFile)"
            Lines="@(MyItems)"
            Overwrite="true"
            Encoding="Unicode"/>
    </Target>

</Project>
```

在此示例中，我们使用具有嵌入换行符的属性来编写具有多行的文本文件。 如果 `Lines` 中的条目嵌入了换行符，则新行将包含在输出文件中。 由此，可引用多行属性。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <Target Name="WriteLaunchers" AfterTargets="CopyFilesToOutputDirectory">
      <PropertyGroup>
        <LauncherCmd>
@ECHO OFF
dotnet %~dp0$(AssemblyName).dll %*
        </LauncherCmd>
      </PropertyGroup>

      <WriteLinesToFile
        File="$(OutputPath)$(AssemblyName).cmd"
        Overwrite="true"
        Lines="$(LauncherCmd)" />
  </Target>
</Project>
```

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
