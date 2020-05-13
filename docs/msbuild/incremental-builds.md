---
title: 增量生成 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, incremental builds
ms.assetid: 325e28c7-4838-4e3f-b672-4586adc7500c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7283d67710a3b5b319b2d25a1c5d6535fed83b9
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633715"
---
# <a name="incremental-builds"></a>增量生成

增量生成是经过优化的生成。优化后，如果目标具有的输出文件相对于其相应的输入文件保持为最新，则系统不会执行该目标。 目标元素可同时具有 `Inputs` 属性（指示目标要预期为输入的项）和 `Outputs` 属性（指示目标要生成为输出的项）。 MSBuild 尝试在这些属性的值之间找到一对一映射。 如果存在一对一映射，MSBuild 比较每个输入项的时间戳和其对应的输出项的时间戳。 不具有一对一映射的输出文件则与所有输入文件进行对比。 如果某项的输出文件的时间戳与该项的一个或多个输入文件相同，或与之相比较新，则将该项视为最新。

> [!NOTE]
> 当 MSBuild 评估输入文件时，只考虑当前执行中列表的内容。 自上次生成后的列表更改不会自动让目标到期。

如果所有输出项均为最新，MSBuild 就跳过目标。 目标的这种增量生成可以显著提高生成速度  。 如果只有部分文件保持为最新，MSBuild 会执行目标，但跳过最新的项，从而使所有项均保持为最新。 此进程称为“部分增量生成”  。

项转换通常会生成一对一映射。 有关详细信息，请参阅[转换](../msbuild/msbuild-transforms.md)。

 请看下列代码。

```xml
<Target Name="Backup" Inputs="@(Compile)"
    Outputs="@(Compile->'$(BackupFolder)%(Identity).bak')">
    <Copy SourceFiles="@(Compile)" DestinationFiles=
        "@(Compile->'$(BackupFolder)%(Identity).bak')" />
</Target>
```

由 `Compile` 项目类型表示的文件集会被复制到备份目录。 备份文件的文件扩展名为 .bak  。 如果运行备份目标后未删除或修改由 `Compile` 项目类型表示的文件或相应的备份文件，则后续生成中将跳过备份目标。

## <a name="output-inference"></a>输出推理

MSBuild 通过比较目标的 `Inputs` 和 `Outputs` 属性来确定是否执行该目标。 理想情况下，无论是否执行相关目标，增量生成完成后存在的文件集应保持不变。 由任务创建或修改的属性和项会影响生成，因此即使跳过会造成影响的目标，MSBuild 也必须推断这些属性或项的值。 此进程称为“输出推理”  。

共有三种情况：

- 目标具有计算结果为 `Condition` 的 `false` 属性。 这种情况不运行目标且不影响生成。

- 目标具有过时的输出，将运行目标，让这些输出保持为最新。

- 目标没有过时的输出，将跳过目标。 MSBuild 会像已运行目标一样，计算目标并更改项和属性。

要支持增量编译，任务必须确保所有 `TaskParameter` 元素的 `Output` 属性值与某个任务输入参数相等。 下面是一些可能的恶意活动：

```xml
<CreateProperty Value="123">
    <Output PropertyName="Easy" TaskParameter="Value" />
</CreateProperty>
```

无论是执行还是跳过目标，此代码都将创建值为“123”的 Easy 属性。

从 MSBuild 3.5 开始，将对目标中的项和属性组自动执行输出推理。 目标中无需 `CreateItem` 任务，应避免该任务。 此外，目标中只能将 `CreateProperty` 任务用于确认是否执行了目标。

在 MSBuild 3.5 之前，可以使用 [CreateItem](../msbuild/createitem-task.md) 任务。

## <a name="determine-whether-a-target-has-been-run"></a>确认是否运行了某个目标

因输出推理，必须向目标添加 `CreateProperty` 任务，以检查属性和项，从而确定是否执行了该目标。 向目标添加 `CreateProperty` 任务，并为其提供 `Output` 元素，该元素的 `TaskParameter` 为 “ValueSetByTask”。

```xml
<CreateProperty Value="true">
    <Output TaskParameter="ValueSetByTask" PropertyName="CompileRan" />
</CreateProperty>
```

该代码会创建 CompileRan 属性并为其赋予值 `true`，但仅当执行了目标时才如此操作。 如果跳过目标，则不会创建 CompileRan。

## <a name="see-also"></a>另请参阅

- [目标](../msbuild/msbuild-targets.md)
