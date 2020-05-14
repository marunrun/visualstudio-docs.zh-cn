---
title: GetFrameworkSdkPath 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GetFrameworkSdkPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFrameworkSdkPath task [MSBuild]
- MSBuild, GetFrameworkSdkPath task
ms.assetid: 2ef82b98-02b6-40cf-a9b5-f0e882fb5064
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d021bdb485846749ea2c7e9dfe483e09738fda46
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633988"
---
# <a name="getframeworksdkpath-task"></a>GetFrameworkSdkPath 任务

检索 Windows 软件开发工具包 (SDK) 的路径。
## <a name="task-parameters"></a>任务参数

下表描述了 `GetFrameworkSdkPath` 任务的参数。
下表描述了 `GetFrameworkSdkPath` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`FrameworkSdkVersion20Path`|可选的 `String` 只读输出参数。<br /><br /> 如果存在，则返回 .NET SDK 2.0 版的路径。 否则返回 `String.Empty`。|
|`FrameworkSdkVersion35Path`|可选的 `String` 只读输出参数。<br /><br /> 如果存在，则返回 .NET SDK 3.5 版的路径。 否则返回 `String.Empty`。|
|`FrameworkSdkVersion40Path`|可选的 `String` 只读输出参数。<br /><br /> 如果存在，则返回 .NET SDK 4.0 版的路径。 否则返回 `String.Empty`。|
|`Path`|可选 `String` 输出参数。<br /><br /> 如果存在任何版本，则包含最新 .NET SDK 的路径。 否则返回 `String.Empty`。|

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

以下示例使用 `GetFrameworkSdkPath` 任务将指向 Windows SDK 的路径存储在 `SdkPath` 属性中。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="GetPath">
        <GetFrameworkSdkPath>
            <Output
                TaskParameter="Path"
                PropertyName="SdkPath" />
        </GetFrameworkSdkPath>
        <Message Text="$(SdkPath)"/>
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
