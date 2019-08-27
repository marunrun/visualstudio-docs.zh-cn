---
title: 如何：清理生成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, cleaning a build
- directories [.NET Framework], for output items
- output, removing items
ms.assetid: 999ba473-b0c4-45c7-930a-63ea7a510509
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f8c64bb19d65540f8c72be9acb1c5f59deb3c8f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156645"
---
# <a name="how-to-clean-a-build"></a>如何：清理生成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

清理生成时，将删除所有中间文件和输出文件，仅保留项目和组件文件。 然后，可以根据项目和组件文件生成中间文件和输出文件的新实例。 随 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 提供的常规任务库中包括一个 [Exec](../msbuild/exec-task.md) 任务，可以使用该任务运行系统命令。 有关任务库的详细信息，请参阅[任务参考](../msbuild/msbuild-task-reference.md)。  
  
## <a name="creating-a-directory-for-output-items"></a>创建输出项目录  
 默认情况下，编译项目时创建的 .exe 文件与项目文件和源文件放在同一个目录中。 但是，输出项通常在单独的目录中创建。  
  
#### <a name="to-create-a-directory-for-output-items"></a>创建输出项目录  
  
1. 使用 `Property` 元素定义目录的位置和名称。 例如，在包含项目文件和源文件的目录中创建一个名为 `BuiltApp` 的目录：  
  
     `<builtdir>BuiltApp</builtdir>`  
  
2. 如果目录不存在，使用 [MakeDir](../msbuild/makedir-task.md) 任务创建目录。 例如:  
  
     `<MakeDir Directories = "$(builtdir)"`  
  
     `Condition = "!Exists('$(builtdir)')" />`  
  
## <a name="removing-the-output-items"></a>删除输出项  
 在新建中间文件和输出文件的实例之前，可能需要清除这些文件以前的所有实例。 使用 [RemoveDir](../msbuild/removedir-task.md) 任务从磁盘上删除目录和该目录中包含的所有文件和目录。  
  
#### <a name="to-remove-a-directory-and-all-files-contained-in-the-directory"></a>删除目录和目录中包含的所有文件  
  
- 使用 `RemoveDir` 任务删除目录。 例如:  
  
     `<RemoveDir Directories="$(builtdir)" />`  
  
## <a name="example"></a>示例  
 以下代码示例项目包含一个新目标 `Clean`，该目标使用 `RemoveDir` 任务删除目录和该目录中包含的所有文件和目录。 此外，在此示例中，`Compile` 目标还将为清理生成时删除的输出项创建一个单独的目录。  
  
 由于 `Compile` 被定义为默认目标，因此，除非另外指定一个或多个目标，否则会自动使用该默认目标。 使用命令行开关 /target  另外指定一个目标。 例如:  
  
 `msbuild <file name>.proj /target:Clean`  
  
 /target  开关可以缩写为 /t  并可以指定多个目标。 例如，若要依次使用目标 `Clean` 和 `Compile`，请键入：  
  
 `msbuild <file name>.proj /t:Clean;Compile`  
  
```  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <PropertyGroup>  
        <!-- Set the application name as a property -->  
        <name>HelloWorldCS</name>  
  
        <!-- Set the output folder as a property -->  
        <builtdir>BuiltApp</builtdir>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <!-- Specify the inputs by type and file name -->  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Check whether an output folder exists and create  
        one if necessary -->  
        <MakeDir Directories = "$(builtdir)"   
            Condition = "!Exists('$(builtdir)')" />  
  
        <!-- Run the Visual C# compiler -->  
        <CSC Sources = "@(CSFile)"   
            OutputAssembly = "$(BuiltDir)\$(appname).exe">  
            <Output TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
  
    <Target Name = "Clean">  
        <RemoveDir Directories="$(builtdir)" />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Exec 任务](../msbuild/exec-task.md)   
 [MakeDir 任务](../msbuild/makedir-task.md)   
 [RemoveDir 任务](../msbuild/removedir-task.md)   
 [Csc 任务](../msbuild/csc-task.md)   
 [目标](../msbuild/msbuild-targets.md)
