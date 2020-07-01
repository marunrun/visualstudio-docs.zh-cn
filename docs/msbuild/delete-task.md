---
title: Delete 任务 | Microsoft Docs
ms.date: 06/11/2020
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Delete
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Delete task [MSBuild]
- MSBuild, Delete task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eddb9804378a4c32de9d1b68f952bc715f32ffd6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288905"
---
# <a name="delete-task"></a>Delete 任务

删除指定的文件。

## <a name="parameters"></a>参数

下表描述了 `Delete` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`DeletedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定已成功删除的文件。|
|`Files`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要删除的文件。|
|`TreatErrorsAsWarnings`|可选的 `Boolean` 参数<br /><br /> 如果为 `true`，错误将被记录为警告。 默认值为 `false`。|

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

> [!WARNING]
> 对 `Delete` 任务使用通配符时请务必小心。 可以使用 `$(SomeProperty)\**\*.*` 或 `$(SomeProperty)/**/*.*` 等表达式轻松删除错误的文件（尤其是当属性计算结果为空字符串时，`Files` 参数可能计算到驱动器的根目录，额外删除你不希望删除的内容）。

## <a name="example"></a>示例

下面的示例在生成 `DeleteDebugSymbolFile` 目标时删除 MyApp.pdb 文件。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

    <PropertyGroup>
        <AppName>ConsoleApp1</AppName>
    </PropertyGroup>

    <Target Name="DeleteDebugSymbolFile">
        <Message Text="Deleting $(OutDir)$(AppName).pdb"/>
        <Delete Files="$(OutDir)$(AppName).pdb" />
    </Target>
  
</Project>

```

如果需要跟踪已删除的文件，请将 `TaskParameter` 设置为带有项名称的 `DeletedFiles`，如下所示：

```xml
      <Target Name="DeleteDebugSymbolFile">
        <Delete Files="$(OutDir)$(AppName).pdb" >
              <Output TaskParameter="DeletedFiles" ItemName="DeletedList"/>
        </Delete>
        <Message Text="Deleted files: '@(DeletedList)'"/>
    </Target>
```

不要直接在 `Delete` 任务中使用通配符，而是创建一个文件 `ItemGroup`，以便删除该文件并在其上运行 `Delete` 任务。 不过，请务必仔细放置 `ItemGroup`。 如果将 `ItemGroup` 放置在项目文件的顶层，则会在生成开始之前提前进行评估，因此它不会包括生成过程中生成的任何文件。 因此，将创建要删除的项列表的 `ItemGroup` 添加到接近 `Delete` 任务的目标中。 还可以指定一个条件来检查属性是否不为空，这样就不会创建具有从驱动器根目录开始的路径的项列表。

`Delete` 任务用于删除文件。 如果要删除目录，请使用 [RemoveDir](removedir-task.md)。

`Delete` 任务未提供删除只读文件的选项。 若要删除只读文件，可以使用 `Exec` 任务运行 `del` 命令或等效项，并使用相应的选项启用删除只读文件。 必须注意输入项列表的长度，因为命令行上存在长度限制，并确保处理带有空格的文件名，如本示例所示：

```xml
<Target Name="DeleteReadOnly">
  <ItemGroup>
    <FileToDelete Include="read only file.txt"/>
  </ItemGroup>
  <Exec Command="del /F /Q &quot;@(FileToDelete)&quot;"/>
</Target>
```

通常，在编写生成脚本时，请考虑删除在逻辑上是否为 `Clean` 操作的一部分。 如果需要在常规 `Clean` 操作中设置一些要清理的文件，可以将这些文件添加到 `@(FileWrites)` 列表，它们将在下一个 `Clean` 上删除。 如果需要更多自定义处理，请定义一个目标，并通过设置属性 `BeforeTargets="Clean"` 或 `AfterTargets="Clean"` 指定其运行，或者定义 `BeforeClean` 或 `AfterClean` 目标的自定义版本。 请参阅[自定义生成](customize-your-build.md)。

## <a name="see-also"></a>请参阅

- [RemoveDir 任务](removedir-task.md)
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
