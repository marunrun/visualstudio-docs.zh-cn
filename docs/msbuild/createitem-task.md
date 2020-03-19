---
title: CreateItem 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#CreateItem
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CreateItem task [MSBuild]
- MSBuild, CreateItem task
ms.assetid: c4311f38-979e-4324-b524-9e8c1cbdc41a
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4364e6c3f637fdf2c3e02a52d3163e5cdd8a5861
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634326"
---
# <a name="createitem-task"></a>CreateItem 任务

使用输入项填充项集合。 这会使项从一个列表复制到另一个列表。

> [!NOTE]
> 此任务已弃用。 从 .NET Framework 3.5 开始，项目组可放置在[目标](../msbuild/target-element-msbuild.md)元素内。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="attributes"></a>特性

 下表描述了 `CreateItem` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`AdditionalMetadata`|可选的 `String` 数组参数。<br /><br /> 指定要附加到输出项的其他元数据。  使用以下语法指定项的元数据名称和值：<br /><br /> *MetadataName* `=` *MetadataValue*<br /><br /> 应该使用分号将多个元数据名称/值对隔开。 如果名称或值包含分号或其他任何特殊字符，则应对这些字符进行转义。 有关详细信息，请参阅[如何：对 MSBuild 中的特殊字符进行转义](../msbuild/how-to-escape-special-characters-in-msbuild.md)。|
|`Exclude`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定要从输出项集合中排除的项。 此参数可包含通配符规范。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)和[如何：从生成中排除文件](../msbuild/how-to-exclude-files-from-the-build.md)。|
|`Include`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要包含在输出项集合中的项。 此参数可包含通配符规范。|
|`PreserveExistingMetadata`|可选 `Boolean` 参数。<br /><br /> 如果为 `True`，则仅应用其他元数据（如果尚不存在）。|

## <a name="remarks"></a>备注

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

 以下代码示例会从项集合 `MySourceItemsWithMetadata` 创建一个名为 `MySourceItems` 的新项集合。 `CreateItem` 任务会使用 `MySourceItems` 项中的项填充新的项集合。 然后它会将一个名为 `MyMetadata` 的其他元数据条目（值为 `Hello`）添加到新集合中的每个项。

 任务执行后，`MySourceItemsWithMetadata` 项集合包含项 file1.resx 和 file2.resx，这两者都具有  *的元数据条目*  `MyMetadata`。 `MySourceItems` 项集合保持不变。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MySourceItems Include="file1.resx;file2.resx" />
    </ItemGroup>

    <Target Name="NewItems">
        <CreateItem
            Include="@(MySourceItems)"
            AdditionalMetadata="MyMetadata=Hello">
           <Output
               TaskParameter="Include"
               ItemName="MySourceItemsWithMetadata"/>
        </CreateItem>

    </Target>

</Project>
```

 下表对任务执行后输出项的值进行了描述。 项元数据显示在项后的括号中。

|项集合|内容|
|---------------------|--------------|
|`MySourceItemsWithMetadata`|*file1.resx* (`MyMetadata="Hello"`)<br /><br /> *file2.resx* (`MyMetadata="Hello"`)|

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
