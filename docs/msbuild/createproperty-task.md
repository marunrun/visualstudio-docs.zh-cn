---
title: CreateProperty 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#CreateProperty
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CreateProperty task [MSBuild]
- MSBuild, CreateProperty task
ms.assetid: fbc31a88-62d4-43d2-b739-68ef3fac38f5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 155e8e6b57cc388e8c2981297be8b26ef5444c1b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634313"
---
# <a name="createproperty-task"></a>CreateProperty 任务

使用传入的值填充属性。 通过该操作可以将值从一个属性或字符串复制到另一个属性或字符串。

## <a name="attributes"></a>特性

下表描述了 `CreateProperty` 任务的参数。

| 参数 | 描述 |
|------------------| - |
| `Value` | 可选 `String` 输出参数。<br /><br /> 指定要复制到新属性的值。 |
| `ValueSetByTask` | 可选 `String` 输出参数。<br /><br /> 包含与 `Value` 参数相同的值。 在由于输出是最新的而跳过封闭目标的情况下，仅当需要避免由 MSBuild 设置输出属性时，使用此参数。 |

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

以下示例在 `CreateProperty` 任务中通过合并 `SourceFilename` 和 `SourceFileExtension` 属性的值创建 `NewFile` 属性。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <SourceFilename>Module1</SourceFilename>
        <SourceFileExtension>vb</SourceFileExtension>
    </PropertyGroup>

    <Target Name="CreateProperties">

        <CreateProperty
            Value="$(SourceFilename).$(SourceFileExtension)">
            <Output
                TaskParameter="Value"
                PropertyName="NewFile" />
        </CreateProperty>

    </Target>

</Project>
```

运行项目后，`NewFile` 属性的值为 Module1.vb  。

## <a name="see-also"></a>请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
