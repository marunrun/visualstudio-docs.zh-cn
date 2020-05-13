---
title: DownloadFile 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#DownloadFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- DownloadFile task [MSBuild]
- MSBuild, DownloadFile task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 81a9c3b1c22277261276ced1940f1f2e83d11882
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634248"
---
# <a name="downloadfile-task"></a>DownloadFile 任务

使用超文本传输协议 (HTTP) 下载指定文件。

>[!NOTE]
>DownloadFile 任务仅在 MSBuild 15.8 及更高版本中提供。

## <a name="parameters"></a>参数

下表描述了 `DownloadFile` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`DestinationFileName`|可选的 <xref:Microsoft.Build.Framework.ITaskItem> 参数<br /><br /> 要用于所下载文件的名称。  默认情况下，文件名派生自 `SourceUrl` 或者远程服务器。|
|`DestinationFolder`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定文件要下载到的目的文件夹。  如果不存在，则创建一个文件夹。|
|`DownloadedFile`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定已下载的文件。|
|`Retries`|可选 `Int32` 参数。<br /><br /> 指定之前的所有尝试都失败后，尝试下载的次数。 默认为零。|
|`RetryDelayMilliseconds`|可选 `Int32` 参数。<br /><br /> 指定任意必要重试之间的延迟（以毫秒为单位）。 默认为 5000。|
|`SkipUnchangedFiles`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则跳过下载未更改文件。 默认为 `true`。 根据远程服务器，如果文件的大小和上次修改时间相同，则 `DownloadFile` 任务认为文件保持不变。 <br /><br />**注意：** 并非指示文件最后修改日期的所有 HTTP 服务器都导致再次下载文件。|
|`SourceUrl`|必选 `String` 参数。<br /><br /> 指定要下载的 URL。|

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

以下示例在生成项目前下载文件并将其包含在 `Content` 项中。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
      <MyUrl>https://raw.githubusercontent.com/Microsoft/msbuild/master/LICENSE</MyUrl>
    </PropertyGroup>

    <Target Name="DownloadContentFiles" BeforeTargets="Build">
        <DownloadFile
            SourceUrl="$(MyUrl)"
            DestinationFolder="$(MSBuildProjectDirectory)">
        <Output TaskParameter="DownloadedFile" ItemName="Content" />
      </DownloadFile>
    </Target>

</Project>
```

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
