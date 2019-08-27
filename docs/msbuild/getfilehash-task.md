---
title: GetFileHash 任务 | Microsoft Docs
ms.date: 01/28/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFileHash task [MSBuild]
- MSBuild, GetFileHash task
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ab5da58b125f86627d54547bd9f6f7cddc16c4de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977498"
---
# <a name="getfilehash-task"></a>GetFileHash 任务

计算文件或文件集的内容的校验和。

此任务已添加到版本 15.8 中，但需要一种用于 16.0 以下 MSBuild 版本的[变通方法](https://github.com/Microsoft/msbuild/pull/3999#issuecomment-458193272)。

## <a name="task-parameters"></a>任务参数

 下表描述了 `GetFileHash` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`Files`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br />要进行哈希处理的文件。|
|`Items`|<xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br />`Files` 输入以及文件哈希的其他元数据集。|
|`Hash`|`String` 输出参数。<br /><br />文件的哈希。 在仅传入一个项目时才设置此输出。|
|`Algorithm`|可选 `String` 参数。<br /><br />算法。 允许的值：`SHA256`、`SHA384`、`SHA512`。 默认值 = `SHA256`。|
|`MetadataName`|可选 `String` 参数。<br /><br />每个项目中存储哈希的元数据名称。 默认为 `FileHash`。|
|`HashEncoding`|可选 `String` 参数。<br /><br />用于生成哈希的编码。 默认为 `hex`。 允许的值 = `hex`、`base64`。|

## <a name="example"></a>示例

以下示例使用 `GetFileHash` 任务确定并打印 `FilesToHash` 项的校验和。

```xml
<Project>
  <ItemGroup>
    <FilesToHash Include="$(MSBuildThisFileDirectory)\*" />
  </ItemGroup>
  <Target Name="GetHash">
    <GetFileHash Files="@(FilesToHash)">
      <Output
          TaskParameter="Items"
          ItemName="FilesWithHashes" />
    </GetFileHash>

    <Message Importance="High"
             Text="@(FilesWithHashes->'%(Identity): %(FileHash)')" />
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)

- [任务参考](../msbuild/msbuild-task-reference.md)