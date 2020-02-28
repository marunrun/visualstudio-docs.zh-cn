---
title: Delete 任务 | Microsoft Docs
ms.date: 11/04/2016
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
ms.openlocfilehash: 69f6be4c80519b023d3f11c28f3d5f5b2bf8f8e1
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557966"
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
以下示例删除文件 MyApp.pdb。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <AppName>MyApp</AppName>
    </PropertyGroup>

    <Target Name="DeleteFiles">
        <Delete Files="$(AppName).pdb" />
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
