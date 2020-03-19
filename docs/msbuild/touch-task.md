---
title: Touch 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Touch
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Touch task
- Touch task [MSBuild]
ms.assetid: 8a978645-1393-4904-ae69-42afabd8c109
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 873783196a3eebdaca9cc4278b091e084c1488b0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631648"
---
# <a name="touch-task"></a>Touch 任务

设置文件的访问和修改时间。

## <a name="parameters"></a>参数

 下表描述了 `Touch` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`AlwaysCreate`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，将创建任何尚未存在的文件。|
|`Files`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要改动的文件集合。|
|`ForceTouch`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则即使在文件为只读时也强制改动文件。|
|`Time`|可选 `String` 参数。<br /><br /> 指定当前时间以外的时间。 格式必须为 <xref:System.DateTime.Parse%2A> 方法可接受的格式。|
|`TouchedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含成功改动的项的集合。|

## <a name="remarks"></a>备注

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

 以下示例使用 `Touch` 任务更改在 `Files` 项集合中指定的文件的访问和修改时间，并将成功改动的文件列表放入 `FilesTouched` 项集合。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

<ItemGroup>
    <Files Include="File1.cs;File2.cs;File3.cs" />
</ItemGroup>

    <Target Name="TouchFiles">
        <Touch
            Files="@(Files)">
            <Output
                TaskParameter="TouchedFiles"
                ItemName="FilesTouched"/>
    </Touch>
</Target>
</Project>
```

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
