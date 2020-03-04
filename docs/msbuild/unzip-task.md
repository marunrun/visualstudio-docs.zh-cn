---
title: Unzip 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Unzip
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Unzip task [MSBuild]
- MSBuild, Unzip task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d331fda05e8655be0536a1e83d8309ae8c060b1f
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77631505"
---
# <a name="unzip-task"></a>Unzip 任务

将 .zip 存档解压缩到指定位置。 

>[!NOTE]
>仅在 MSBuild 15.8 及更高版本中提供 `Unzip` 任务。

## <a name="parameters"></a>参数

 下表描述了 `Unzip` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`DestinationFolder`|<xref:Microsoft.Build.Framework.ITaskItem> 参数（必选）<br /><br /> 指定文件要解压到的目的文件夹。|
|`OverwriteReadOnlyFiles`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则覆盖只读文件。 默认为 `false`。|
|`SkipUnchangedFiles`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则跳过未更改的解压缩文件。 默认为 `true`。 如果文件的大小和上次修改时间相同，则 `Unzip` 任务认为文件保持不变。|
|`SourceFiles`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个或多个文件进行解压缩。 指定多个文件时，它们将按顺序解压缩到同一文件夹中。|

## <a name="remarks"></a>备注

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

 以下示例将解压缩存档并覆盖所有只读文件。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <Target Name="UnzipArchive" BeforeTargets="Build">
        <Unzip
            SourceFiles="MyArchive.zip"
            DestinationFolder="$(OutputPath)\unzipped"
            OverwriteReadOnlyFiles="true"
        />
    </Target>

</Project>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
