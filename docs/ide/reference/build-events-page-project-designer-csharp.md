---
title: “项目设计器”->“生成事件”页 (C#)
ms.date: 10/17/2019
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 6629f41657a546ffb5fb48e0b6efb5f4f0dd50cb
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596874"
---
# <a name="build-events-page-project-designer-c"></a>“项目设计器”->“生成事件”页 (C#)

使用“项目设计器”的“生成事件”页指定生成配置说明   。 还可以指定任何生成后事件运行的条件。 有关详细信息，请参阅[如何：指定生成事件 (C#)](../../ide/how-to-specify-build-events-csharp.md) 以及[如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)。

## <a name="uielement-list"></a>UIElement 列表

**配置**

此控件在本页不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

**平台**

此控件在本页面上不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

预生成事件命令行 

在生成开始之前，指定要执行的任何命令。 要键入长命令，单击“编辑预生成”，显示[预生成事件/生成后事件命令行对话框](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)  。

> [!NOTE]
> 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。

生成后事件命令行 

在生成结束之后，指定要执行的任何命令。 要键入长命令，单击“编辑生成后”，显示“预生成事件/生成后事件命令行对话框”   。

> [!NOTE]
> 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。

运行生成后事件 

指定以下生成后事件运行的条件，如下表所示。

|选项|结果|
|------------|------------|
|始终 |无论生成是否成功，均运行生成后事件。|
|成功生成时 |如果生成成功，则运行生成后事件。 因此，即使项目已为最新状态，但只要生成成功，就会运行该事件。|
|生成更新项目输出时 |生成后事件仅在编译器的输出文件 (.exe or .dll) 不同于之前的编译器输出文件时才运行。 因此，如果项目为最新状态，则不会运行生成后事件。|

## <a name="in-the-project-file"></a>在项目文件中

在早期版本的 Visual Studio 中，当你更改 IDE 中的 PreBuildEvent 或 PostBuildEvent 设置时，Visual Studio 会将 `PreBuildEvent` 或 `PostBuildEvent` 属性添加到项目文件   。 例如，如果 IDE 中的 PreBuildEvent 命令行设置如下  ：

```input
"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)"
```

则项目文件设置为：

```xml
<PropertyGroup>
    <PreBuildEvent>"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)" />
</PropertyGroup>
```

对于 .NET Core 项目，Visual Studio 2019（以及较新更新中的 Visual Studio 2017）为 PreBuildEvent 和 PostBuildEvent 设置添加了名为 `PreBuild` 或 `PostBuild` 的 MSBuild 目标   。 这些目标使用 BeforeTargets 和 AfterTargets 属性，它们是 MSBuild 可识别的属性   。 例如，对于前面的示例，Visual Studio 现在生成以下代码：

```xml
<Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="&quot;$(ProjectDir)PreBuildEvent.bat&quot; &quot;$(ProjectDir)..\&quot; &quot;$(ProjectDir)&quot; &quot;$(TargetDir)&quot;" />
</Target>
```

对于生成后事件，请使用名称 `PostBuild` 并将属性 `AfterTargets` 设置为 `PostBuildEvent`。

```xml
<Target Name="PostBuild" AfterTargets="PostBuildEvent">
   <Exec Command="echo Output written to $(TargetDir)" />
</Target>
```

> [!NOTE]
> 对这些项目文件进行了更改以支持 SDK 样式的项目。 如果要将项目文件从旧格式手动迁移到 SDK 样式的格式，则应删除 `PreBuildEvent` 和 `PostBuildEvent` 属性，并将其替换为 `PreBuild` 和 `PostBuild` 目标，如前面的代码所示。 若要了解如何判断你的项目是否为 SDK 样式的项目，请参阅[检查项目格式](/nuget/resources/check-project-format)。

## <a name="see-also"></a>请参阅

- [如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [如何：指定生成事件 (C#)](../../ide/how-to-specify-build-events-csharp.md)
- [项目属性引用](../../ide/reference/project-properties-reference.md)
- [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)
